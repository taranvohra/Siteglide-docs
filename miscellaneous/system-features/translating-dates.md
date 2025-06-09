---
title: FAQ - How can I translate and format dates?
slug: dAqr-
createdAt: 2021-02-17T16:24:52.000Z
updatedAt: 2023-03-03T08:09:58.000Z
---

# Translating Dates

A demo of how you can convert dates from English to a different language

## Answer:

We can use Liquid to format our "raw" date integer to a formatted date. However, this doesn't give the option to select a different language when outputting the date. Here is one example of how you can do this using Liquid:

### Translate the Months:

First, we will need to create an object of Months converted from English to whichever language you'd like:

```liquid
{% raw %}
{% parse_json month_map %}  { 

  "fre": {

    "January": "Januar",

    "February": "Février", 

    "March": "Mars",

    "April": "Avril",

    "May": "Mai",

    "June": "Juin",

    "July": "Juillet",

    "August": "Août",

    "September": "Septembre",

    "October": "Octobre",

    "November": "Novembre",

    "December": "Décembre"

  },

  "ger": {

    "January": "Januar"

  }


}  {% endparse_json %}
{% endraw %}





```

Now we have an object called "months" storing all the translated Months, simply change "FRE" and the translation to whichever language you'd like.

### Search the Months

Now we've translated the Months we'll need to check which one needs to be outputted. Firstly assign a variable with the Month you'd like to translate, I'd like to do so with my items "release\_date":\`

\`

We use the "date" filter here to format the "raw" date integer to a humanized date. This follows Ruby's STRF format, read [here](https://apidock.com/ruby/DateTime/strftime) for more info on formatting dates.

We'll use "%B", as this will store the Month as a String.

Now specify which language in "month\_map" you're using, I've chosen French:

```liquid
{% raw %}
{% parse_json month_map %}  { 

  "fre": {

    "January": "Januar",

    "February": "Février", 

    "March": "Mars",

    "April": "Avril",

    "May": "Mai",

    "June": "Juin",

    "July": "Juillet",

    "August": "Août",

    "September": "Septembre",

    "October": "Octobre",

    "November": "Novembre",

    "December": "Décembre"

  },

  "ger": {

    "January": "Januar"

  }


}  {% endparse_json %}
{% endraw %}

```

Next, we'll use these two variables to search the "month\_map" and return the translated Month:

```liquid
{% raw %}
{% assign translated_month = month_map[language][current_month] %}
{% endraw %}

```

### Format the translated Month and store in a variable:

Now we've found the translated Month we'll need to format it into a complete date, and then store this so it can be outputted:

```liquid
{% raw %}
{% assign date = this['release_date'] | date: "%d" %}
{% assign year = this['release_date'] | date: "%y" %}
{% assign date_complete = date | append: " " | append: translated_month  %}
{% assign date_complete = date_complete | append: " " | append: year %}
{% endraw %}   
```

We assign the Date and Year, formatting them into integer dates using the "date" filter, then we append the finished date to the variable "date\_complete", you can output this like so: `{{date_complete}}`
