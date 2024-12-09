# 👀 Assets Reference

### Linking to Assets

#### HTML - Stylesheets:

`<link rel="stylesheet" type="text/css" href="{{ 'css/styles.css' | asset_url }}" />`

 =>

`https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/css/styles.css?updated=1733383736255`

#### HTML - JavaScript files:

`<script src="{{ 'js/myfile.js' | asset_url }}"></script>`

 =>

`https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/js/myfile.js?updated=1733383736255`

#### HTML - Images:

`{{ 'images/SG-Logo-White.svg' | asset_url }}`

 =>

`https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/images/SG-Logo-White.svg?updated=1733383736255`

#### WebApp Asset Field:

After uploading an image to a WebApp file/image field using the Siteglide Admin's file manager, or using a front-end form, the actual value stored in the database will be something like the format: `images/hero/hero01.jpg` which will point to a file at the location: `marketplace_builder/assets/images/hero/hero01.jpg`.

```liquid
{% raw %}
{{ this['my_field'] | asset_url }}
{% endraw %}
```
 =>

`https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/images/hero/hero01.jpg?updated=1733383736255`

#### CSS - Relative Paths:

{% hint style="warning" %}
Siteglide's CDN uses the "updated" parameter to prioritise fast caching of the image for better performance. The problem with the relative link from CSS is you aren't able to add that parameter dynamically, meaning you may get an older version of the image from the cache. This will not be a problem if the image is never updated, or when it is updated, its filename is changed to a new unique one.
{% endhint %}

`background-image: url('../images/SG-Logo-White.svg');`

#### Background Images

The easiest way to add CSS background images reliably is actually with an inline style attribute in HTML. This is because it allows you to use the `asset_url` Liquid filter:

##### Liquid

```liquid
{% raw %}
<div class="bg-image" style="background-image: url('{{"images/example.jpg" | asset_url}}')"></div>
{% endraw %}
```

Which renders to:

```html
<div class="bg-image" style="background-image: url('https://cdn.staging.oregon.platform-os.com/instances/xxxxxx/assets/js/myfile.js?updated=1733383736255')"></div>
```

##### CSS

Other background property rules can be added as normal in CSS.

```css
.bg-image {
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

#### Vanity URL to Asset - Slower Performance:

`{{ 'images/SG-Logo-White.svg' | asset_path }}` => `/assets/images/SG-Logo-White.svg`

Or

`/assets/images/SG-Logo-White.svg`

