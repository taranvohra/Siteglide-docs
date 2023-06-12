Create an array of a Category's children and check whether they exist.

# Introduction

In this tutorial, I'll explain how you can check whether a Category has children. We'll do this by creating an array of all the Category's children and checking whether the size of this is greater than 0, if so then children exist.

## Prerequisites

*   You've created a [Category](https://help.siteglide.com/article/123-categories-getting-started) and added child Categories

*   You've understood some of [Liquid's](https://developers.siteglide.com/how-do-i-learn-more-about-liquid) syntax

# Create an array of the Category's children

Firstly, let's assign an array that will store all of the Category's children- after we've done this we'll loop over all the Categories and check whether they should be added to the array: `{% assign this_category_children = "[]" | parse_json %}`

# Loop over all the Categories

Now let's use a FOR loop to cycle through all the Categories on the Site, at each index we'll check whether the current Category's parent is equal to the Category we're viewing in the detail view.

Note: `category.last` is used to get the last item in an array- we use this here to remove the Category items from the arrays they're stored in (which contains a simple list number, followed by the Category item).

Now let's look at our loop:

```html
{% assign this_category_children = "[]" | parse_json %}
{%- for category in context.exports.categories.items -%}
  {%- assign this = category.last -%}
  {%- if this.parent == category_id -%}
    {%- assign this_category_children = this_category_children | add_to_array: this.id %}
  {%- endif -%}
{%- endfor -%}
```

Within the for loop we're checking two variables:&#x20;

*   `this.parent` - this will contain the parent ID of the current Category in our loop

*   `category_id` - this will always be the same in the for loop above and contains the ID of the Category being outputted in the detailed view.

Now look at the fourth line of code in the example above, you'll notice these two variables are checked against each other, if they are equal then the Category item in our loop will be appended to the `this_category_children` array.

So once this loop has finished `this_category_children` will contain all of the children within the Category we're outputting on our detail layout. You could use the .size of our newly created array to determine if there are children, this could be done using a simple IF statement:

```html
{%- if this_category_children.size > 0 -%}
  OUTPUT CHILDREN
{%- else -%}
  DO SOMETHING ELSE
{%- endif -%}
```

