# Events - Map List View

The Map Layout is a List Layout which demonstrates how you can use the Google Maps API to visualise Events from the Siteglide database.

![](https://downloads.intercomcdn.com/i/o/203125841/156aa59682bf991accbb5832/image.png)

## Prerequisites

* You've Installed the Events Module
* You've added Events in the Admin
* You've [added a Location to at least one Event](https://help.siteglide.com/article/131-modules-getting-started#2-adding-a-location)

## Introduction

The Map Layout is a List Layout which demonstrates how you can use the Google Maps API to visualise Events from the Siteglide database. In order to use this Layout, you'll need to [create an account with Google](https://developers.google.com/maps/documentation/javascript/get-api-key) and follow the instructions to generate an API key.

We've tried to expose just enough of the JavaScript to allow you to customise your Layout, while keeping as much Liquid as possible tucked away to keep things simple. Despite this, you will need to refer to the [Google Maps API docs](https://developers.google.com/maps/documentation/javascript/get-api-key) for any advanced customisation work you'd like to carry out.

## Outputting the Map Layout on a Page

The Events Module Map Layout is an example of a List Layout. Like all List Layouts, you can output the Events Module Map Layout in any Liquid File, including Pages, Templates and Layouts. However, it also requires JavaScript to function properly, so it will not be supported inside an Email e.g. Autoresponder or Workflow.

To output the map, output the List Layout as normal, and choose a Map Layout in the `layout` parameter.

```liquid
{%- include 'module'
    id: '12'
    layout: 'design_system/1/map'
    per_page: '5000'
    show_pagination: 'false' 
-%}


```

There are a few parameters which work particularly well on the Map Layout, because we will want to disable Pagination and show all enabled and released Events at once:

* `per_page: 5000` - Makes sure the first Page shows all Events that are enabled and released
* `show_pagination: 'false'` - Hides Pagination Controls

You can use filtering Parameters as normal to filter Events and only show some on the Map.

* `category_ids` - Add a comma-seperated string of Category IDs to display
* `item_ids` - Add a comma-seperated string of Item IDs to display

You can also use URL parameters to carry out advanced filtering.

## How does the Map Layout Convert Event Locations to a JavaScript array?

You'll notice in the `wrapper.liquid` file that the ordinary Liquid which fetches the `item.liquid` files is outputted inside a JavaScript `<script>` element. This is very important as it allows the Liquid data to be converted to the JavaScript array that Google Maps needs.

```javascript
//---Events Module Map View Options--- 
//--- The Events Module Items should be loaded into a JavaScript Array- 
//--- this allows them to be used by Google Maps. Changing the format in the item.liquid 
//--- file may cause errors.
var locations = [	
	

<div data-gb-custom-block data-tag="-" data-0='modules/siteglide_system/get/get_items' data-1=', item_layout: ' data-2='item'></div>
];

```

The `item.liquid` file should be left in the format of a JSON object, but you may choose to add more variables:

```liquid
{	
    id: "{{this.id}}",
	lat: {{this.properties.module_field_12_7 | split: ',' | first | times: 1 | default: "invalid" }},
	lng: {{this.properties.module_field_12_7 | split: ',' | last | times: 1 | default: "invalid" }},
	name: {{this.properties.name | json }},
	address: {{this.properties.module_field_12_6 | json }},	
    slug: {{this.full_slug | json }},	
    event_start: "{{this.properties.module_field_12_2 | date: "%d/%m/%Y %H:%M T%z"}}",	
    event_end: "{{this.properties.module_field_12_3 | date: "%d/%m/%Y %H:%M T%z"}}",	
    valid: "{% raw %}
{% if this.properties.module_field_12_7 == blank %}invalid{% else %}valid{% endif %}"
}{% unless forloop.last %},{% endunless %}
{% endraw %}
```

Here, we also use Liquid Logic to check for Events with no location data set and exclude them from the List.

## Clustering

We've added [Marker Clustering](https://developers.google.com/maps/documentation/javascript/marker-clustering) to the Map- which is useful if you're displaying multiple Events in the same area. Each time the map is moved, or zoomed in or out, an Event Triggers which will re-draw the markers.

The following behaviour was chosen by us for convenience and demonstration purposes, but can be changed by following the Google documentation.

If any markers are too close to each other, they will be "clustered" under a clustering marker, which will display a number for the number of Events in that location:

![](https://downloads.intercomcdn.com/i/o/203124873/6cfa1a2c995d75ba6d1562b6/image.png)

Clicking on the clustering marker will zoom in by an increment of 1, unless the User is at maximum zoom. As soon as we have zoomed in enough to display more of the markers without causing confusion, we will do so:

![](https://downloads.intercomcdn.com/i/o/203125088/f1e69150b898efc233334f60/image.png)

If we reach maximum zoom and some Events are still clustered (perhaps at the same location), the next click on the clustering marker will reveal an "infowindow" containing details on all Events at that location:

![](https://downloads.intercomcdn.com/i/o/203125404/117159b8479150d8c5d07eea/image.png)

## Customising the Map

We've split the JavaScript for the Map Layout into two files:

* `wrapper.liquid` - Here we define the variables which form the key "settings" needed to to set up the Map the way you want it
* `assets/js/modules/module_12/default_map.js` - This contains the rest of the code needed to make the map functional. For advanced developers who wish to edit using the Google Maps API docs, you can edit this file.

### Customising the Options

These options are all explained by comments in the `wrapper.liquid` JavaScript. Make sure to follow each line except the last with a comma:

* `map_selector: "#map"` - The Selector for the Element into which you want to render the map.
* `zoom: 3` - Sets the initial zoom on the Map. 1 is minimum and 22 is maximum.
* `center: false` - Sets the initial center of the Map. Should be in format {lat: Float, lng: Float} or false. If false, we will find the mid-point between all event locations and center there.
* `show_info_windows: true` - Info Windows give the event information as a modal when you click an event marker.
* `markers.animation:` - Select an animation option from the Google Maps Documentation. String e.g. `"DROP"`.
* `show_summary: false` - Shows a summary of the Events visible on the current Map Viewport.
* `summary_selector: "#mapSummary"` - Selector for Element which will contain any summary. String

### Customising the Event Detail Popups (infowindows)

To do this, you'll need to carefully edit the `default_map.js` file. You'll need to understand how to concatenate Strings and Variables in JavaScript to construct a larger String containing HTML code.

We keep the infowindows for markers and clusters separate. This is because they use different variables, and because it allows you to be more flexible.

#### 1 - Define infowindow HTML for markers

Find the comment in the code: `//Define infowindow for markers`

Next, you'll need to edit the variable here. It's value should be an HTML String containing the content you'd like for the infowindow. You can move the variables around however you like, as long as the syntax remains correct!

```javascript
content: '<h2>'+locations[i].name+'</h2><a href="'+locations[i].slug+'">View Details</a><br><br><p>'+locations[i].address+'</p><p>Starts: '+locations[i].event_start+'<br>Ends: '+locations[i].event_end+'</p>'
```

#### 2 - Define infowindow HTML for cluster markers

Find the comment in the code: `//--Cluster Markers--- Add a marker clusterer to manage the markers.`

Next, you'll need to edit the variable here:

```javascript
infoWindowContent = infoWindowContent + '<h2>'+c.markers_[i].event_data.name+'</h2><a href="'+c.markers_[i].event_data.slug+'">View Details</a><br><br><p>'+c.markers_[i].event_data.address+'</p><p>Starts: '+c.markers_[i].event_data.event_start+'<br>Ends: '+c.markers_[i].event_data.event_end+'</p><br><br>'
```

This is slightly more complicated, because the JavaScript will loop over this and display it for each Event inside the cluster at this level of zoom.

#### 3 - Edit the CSS

As normal, you can use custom CSS to edit the styling of any of the infowindows. Use any classes you added in the previous two steps to target them.

### Customising the Map - Advanced- Following Google's Documentation

Beyond this- you'll have to refer to the [Google Maps API documentation](https://developers.google.com/maps/documentation/javascript/get-api-key) to guide you. Good luck!

You'll be able to make changes in:

* The Page
* `item.liquid` and `wrapper.liquid` file
* `default_map.js` file

If you'd like to see the core functionality of the Events Module expanded, please make a suggestion on the Roadmap and we'll consider it for a future release.
