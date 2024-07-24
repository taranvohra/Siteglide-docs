---
title: Menu Builder
slug: WFI7-
createdAt: 2021-02-16T14:17:17.000Z
updatedAt: 2023-04-11T09:58:24.000Z
---

Create a nested Menu Structure using the Pages you've built and customise its layout

[Menu Builder](https://help.siteglide.com/article/156-menus-getting-started) automatically displays existing pages on the left-hand side for you to add to the menu, which is on the right hand side. To add menu items that link to WebApp items, or to external links; add an existing page and click on the link icon to edit the fields. You can fully customise all fields from here.

## Syntax

```liquid
{% raw %}
{%- include 'menu'
    id:'6560'
    layout: 'default'
    name: 'Main Navigation' 
-%}
{% endraw %}
```

## Parameters

*   `id` - the Menu's ID

*   `layout` - default is /default/ - 'layout' values are relative to the folder: layouts/modules/menu (module\_2)/\[layout name]

*   `name` - name of the Menu

## Liquid Tags

| **Field Name**             | **Liquid Tag**                                                                                                                                                                         | **Description**                                                                                                                                                                 |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Current Level Menu Items   | {% include 'modules/siteglide\_menu/get/get\_items', item\_layout: 'item' -%}                                                                                                          | outputs all top level menu items with li. Should be used in wrapper.liquid                                                                                                      |
| Current Level Name         | {{ this\['link\_name'] }}                                                                                                                                                              | outputs Menu item name. Should be used in item.liquid                                                                                                                           |
| Current Level URL          | {{ this\['link\_url'] }}                                                                                                                                                               | URL of the item                                                                                                                                                                 |
| Current Level custom class | {{this\['link\_class']}}                                                                                                                                                               | Class field contents for current item                                                                                                                                           |
| Sub Levels Menu Items      |  {% assign \_next\_level = \_level \| plus: 1 -%} {% include 'modules/siteglide\_menu/get/get\_items', level: \_next\_level, parent\_id: this\['forced\_id'], item\_layout: 'item' -%} | outputs all sub level menu items with the current layout applied. Should be used in item.liquid. This essentially creates a loop until it reaches the bottom level of your menu |
| Mark As Parent             | {{ this\['is\_parent'] }}                                                                                                                                                              | an invisible field used to define if an item has sub-items or not. If item has sub items it's value will be: true if an item does not have sub items it's value will be: false  |

## Layout Files

Menu Builder Module layouts are stored in the following folder structure, which you can view via Code Editor: `layouts/modules/Menu (module_2)/`

Within this module folder you will find the following layout folders:

*   `default/` - the layout folder
    *   `item.liquid` - menu item file

    *   `wrapper.liquid` - menu item wrapper file

### Example - wrapper.liquid

The wrapper file is used to wrap the menu item output and should contain the liquid for outputting the menu items. You can wrap your menu with any content you'd like, such as a plain \<ul> tag, or a section wrapper with a title.

```liquid
{% raw %}
<ul>
	{% include 'modules/siteglide_menu/get/get_items'
		item_layout: 'item' 
	-%}
</ul>
{% endraw %}
```

### Example - item.liquid

The item file is the chosen output for our items. In this example we've got two cases being used.

```liquid
{% raw %}
{% if this['is_parent'] -%}
  <li>
    <a href="{{this['link_url']}}">{{this['link_name']}}</a>
    {% comment %} Wrap children in ul, set the next level, and then get the children {% endcomment %}
    <ul>
      {% assign _next_level = _level | plus: 1 -%}
      {% include 'modules/siteglide_menu/get/get_items'
         level: _next_level
         parent_id: this['forced_id']
         item_layout: 'item' 
      -%}
    </ul>
  </li>
  {% comment %} Else just output the item by itself {% endcomment %}
{% else -%}	
  <li>
    <a href="{{this['link_url']}}">{{this['link_name']}}</a>
  </li>
{% endif -%}
{% endraw %}
```

**1. The item is a parent, so has sub items.**

*   This means we output the item, and then increment the 'level' value in order to output this item's sub-items.

*   In this case, we use the same item output for every level. You may want a different file for each level. To do that, on line 8 you should set the item\_layout as 'level2' for example. Then you should create a new copy of this 'item' file called 'level2' and put your new layout for the second level there. Alternatively, you can target each level in an {% if -%} statement, but we suggest using new files to separate the layouts more easily.

*   Since we use this same layout for every level, it loops until the bottom level, where the item is no longer a parent.

**2. The item has no sub-items**

*   This means we simply output the item, and nothing else.
