# 📋 Searching by Location

### Installation

Our GeoJSON update for WebApps will work with both newly created WebApps, and WebApps that have been updated after the release of this update.

To apply the update to an existing WebApp, simply go to the WebApp Builder view, and click 'Save'.

***

### Editing the WebApp item

Webapp items have 2 new fields by default:

* `location` - GeoJSON - Stores the location value of your item as coordinates - \[long, lat]
* `address` - Text - Stores the human-readable address value of your item

To set these values in Siteglide you will see the new 'Location' tab on the WebApp item edit view. Here you have 2 choices:

1. Search for an address and then select it from the results dropdown - _Recommended_
2. Manually enter the Address and Longitude/Latitude values for your item

***

### Querying the data

Our new Location Search feature relies on 2 URL parameters to work:

1. `longlat` - LongLat - The coordinate value of the center point for the search - long,lat
2. `distance` - Int - The number of kilometres from the center point

Example - `/map?longlat=-1.2660643,51.3926564&distance=18`

To display results from these parameters you will need the new `use_location_search` parameter on your WebApp include:

`use_location_search` - 'true' or 'false' - default: 'false'

Example - `{%- include 'webapp', id: '1', use_location_search: 'true' -%}`

_Note - Location Search \`(use_location_search`) and Text Search`(use_search\`) will **not** work together at the same time\_

## Example

Example code to search a WebApp by location, and output the results on a map or in a list.

### Introduction

In this example we'll show you how to add a location search to a Page, and then output the results of that search both in a list and on a map. Items will display in the result set when they are within the radius of a chosen location. One example of how you can use this is as a Store Locator for a franchise of Shops.

### 1 - Add an HTML Form and JavaScript to take User input to decide starting position and search radius

Two different options are provided in this example:

#### Current location (using browser default functionality) and desired search radius

Add HTML and JavaScript

:::codeblocktabs

```html
<div class="container text-center">
  <h1 class="mb-3 h2 sg-h2">Search for Stores within your area</h1>
  <div class="row">
    <div class="col-12">
      <form class="sg-form">
        <i class="fas fa-crosshairs fa-2x mb-2"></i>
        <h3 style="margin-bottom: 5rem;">Current Location</h3>
        <div class="text-start form-group sg-form-group">
          <label for="current_locations_distance">Change search distance (km)</label>
          <input class="form-control sg-form-control mb-3" type="number" id="current_locations_distance" value="{{context.params.distance | default: 20}}" />
        </div>
        <div class="row">
          <div class="col-12 d-flex justify-content-end">
            <button class="btn btn-primary sg-btn sg-btn-primary btn-lg sg-btn-lg" onclick="getMyLocation()">Find stores near me <i class="fas fa-arrow-right"></i></button>
          </div>
        </div>
      </form>
    </div>
  </div>
</div>
```

```javascript
<script>
	function getMyLocation() {
		event.preventDefault();
		if(navigator.geolocation){
			navigator.geolocation.getCurrentPosition(showMyPosition);
		}else{
			alert("Geolocation is not supported by this browser.");
		}
		function showMyPosition(position){
			var distance = document.querySelector('#current_locations_distance').value ? document.querySelector('#current_locations_distance').value : 10;
			window.location.replace(window.location.origin+"/store-locations?longlat="+position.coords.longitude+","+position.coords.latitude+"&distance="+distance);
		}
	}
</script>
```

:::

### 2 - Output the results on the Page in a simple list

Use a Layout of your choice.

```
{% raw %}
{%- include 'webapp', id: '1', use_location_search: 'true', layout: 'default' -%}
{% endraw %}
```

### 3 - Output the results on a map

This relies on there being a layout named 'json'. See the contents of 'json' in the 2nd block of code.

Add HTML + Liquid

The Liquid makes sure the map is only outputted after the Page has been refreshed by the JavaScript and the correct parameters are available in the URL for filtering the results.

```liquid
{% raw %}
{%- if context.params.distance and context.params.longlat -%}
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.css" integrity="sha512-1xoFisiGdy9nvho8EgXuXvnpR5GAMSjFwp40gSRE3NwdUdIMIKuPa7bqoUhLD0O/5tPNhteAsE5XyyMi5reQVA==" crossorigin="anonymous" />
	<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.js" integrity="sha512-SeiQaaDh73yrb56sTW/RgVdi/mMqNeM2oBwubFHagc5BkixSpP1fvqF47mKzPGWYSSy4RwbBunrJBQ4Co8fRWA==" crossorigin="anonymous"></script>
	<div id="map" class="map" style="height:400px;width:100%"></div>
	<span id="map_content" style="display:none">
    {%- include 'webapp'
      id: '1'
      use_location_search: 'true'
      type: 'list'
    -%}
  </span>
{%- endif -%}
{% endraw %}
```

Add JavaScript

The following function is triggered by the script from step 1, only after it has finished loading- this occurs because the function's name is referenced in the URL parameter fetching the Script. The code must be placed above the \<script> tag from step 1.

```javascript
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.css" integrity="sha512-1xoFisiGdy9nvho8EgXuXvnpR5GAMSjFwp40gSRE3NwdUdIMIKuPa7bqoUhLD0O/5tPNhteAsE5XyyMi5reQVA==" crossorigin="anonymous" />
	<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.js" integrity="sha512-SeiQaaDh73yrb56sTW/RgVdi/mMqNeM2oBwubFHagc5BkixSpP1fvqF47mKzPGWYSSy4RwbBunrJBQ4Co8fRWA==" crossorigin="anonymous"></script>
	<script>
  var distance = {{context.params.distance | default: 10 }};
  var center = "{{context.params.longlat}}".split(',');

  var map = L.map('map').setView([parseFloat(center[1]), parseFloat(center[0])], 8);

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  L.circle([parseFloat(center[1]), parseFloat(center[0])], {radius: distance*1000}).addTo(map);

  var locations = "{"+document.querySelector('#map_content').innerText.trim().slice(0, -1)+"}";
  locations = JSON.parse(locations);
  Object.keys(locations).forEach(function(k){
    L.marker([locations[k].latlong.coordinates[1], locations[k].latlong.coordinates[0]]).addTo(map).bindPopup(locations[k].name);
  });
</script>
```

Layout 'json':

```json
"{{this.id}}": {
  "name": "{{this.name}}",
  "latlong": {{this.location | json}}, 
  "address": "{{this.address}}"
},
```

***

### Full example

```liquid
{% raw %}
<div class="container text-center">
  <h1 class="mb-3 h2 sg-h2">Search for Stores within your area</h1>
  <div class="row">
    <div class="col-12">
      <form class="sg-form">
        <i class="fas fa-crosshairs fa-2x mb-2"></i>
        <h3 style="margin-bottom: 5rem;">Current Location</h3>
        <div class="text-start form-group sg-form-group">
          <label for="current_locations_distance">Change search distance (km)</label>
          <input class="form-control sg-form-control mb-3" type="number" id="current_locations_distance" value="{{context.params.distance | default: 20}}" />
        </div>
        <div class="row">
          <div class="col-12 d-flex justify-content-end">
            <button class="btn btn-primary sg-btn sg-btn-primary btn-lg sg-btn-lg" onclick="getMyLocation()">Find stores near me <i class="fas fa-arrow-right"></i></button>
          </div>
        </div>
      </form>
    </div>
  </div>
</div>
<script>
	function getMyLocation() {
		event.preventDefault();
		if(navigator.geolocation){
			navigator.geolocation.getCurrentPosition(showMyPosition);
		}else{
			alert("Geolocation is not supported by this browser.");
		}
		function showMyPosition(position){
			var distance = document.querySelector('#current_locations_distance').value ? document.querySelector('#current_locations_distance').value : 10;
			window.location.replace(window.location.origin+"/store-locations?longlat="+position.coords.longitude+","+position.coords.latitude+"&distance="+distance);
		}
	}
</script>

{%- if context.params.distance and context.params.longlat -%}
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.css" integrity="sha512-1xoFisiGdy9nvho8EgXuXvnpR5GAMSjFwp40gSRE3NwdUdIMIKuPa7bqoUhLD0O/5tPNhteAsE5XyyMi5reQVA==" crossorigin="anonymous" />
	<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/leaflet.min.js" integrity="sha512-SeiQaaDh73yrb56sTW/RgVdi/mMqNeM2oBwubFHagc5BkixSpP1fvqF47mKzPGWYSSy4RwbBunrJBQ4Co8fRWA==" crossorigin="anonymous"></script>
	<div id="map" class="map" style="height:400px;width:100%"></div>
	<span id="map_content" style="display:none">{%- include 'webapp', id: '1', use_location_search: 'true', type: 'list' -%}</span>
	<script>
		var distance = {{context.params.distance | default: 10 }};
		var center = "{{context.params.longlat}}".split(',');
		var map = L.map('map').setView([parseFloat(center[1]), parseFloat(center[0])], 8);
		L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
			attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
		}).addTo(map);
		L.circle([parseFloat(center[1]), parseFloat(center[0])], {radius: distance*1000}).addTo(map);
		var locations = "{"+document.querySelector('#map_content').innerText.trim().slice(0, -1)+"}";
		locations = JSON.parse(locations);
		Object.keys(locations).forEach(function(k){
			L.marker([locations[k].latlong.coordinates[1], locations[k].latlong.coordinates[0]]).addTo(map).bindPopup(locations[k].name);
		});
	</script>
{%- endif -%}
```
{% endraw %}