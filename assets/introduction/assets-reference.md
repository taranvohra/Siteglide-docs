# 👀 Assets Reference

### Linking to Assets

#### HTML - Stylesheets:

`<link rel="stylesheet" type="text/css" href="{{ 'css/styles.css' | asset_url }}" />`

#### HTML - JavaScript files:

`<script src="{{ 'js/myfile.js' | asset_url }}"></script>`

#### HTML - Images:

`{{ 'images/SG-Logo-White.svg' | asset_url }}`

#### WebApp Asset Field:

`{{ this['my_field'] | asset_url }}`

#### CSS - Relative Paths:

`background-image: url('../images/SG-Logo-White.svg');`

#### Vanity URL to Asset - Slower Performance:

`{{ 'images/SG-Logo-White.svg' | asset_path }}`

`Or`

`/assets/images/SG-Logo-White.svg`

