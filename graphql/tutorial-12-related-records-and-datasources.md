
# Introduction

In this tutorial we're going to show you how you can use a single query to get not only results in a single table, but at the same time return related results from another table.

For example:

*   Products may be related to categories- and each category may be related to some help articles.

*   Blog Articles may each be related to an Author, and that Author may have a relationship with some Secure Zones.

Using related\_records is powerful because:

*   It allows you to build more complex applications - giving you complete control over getting the data you need.

*   It's flexible - if you've stored enough data, you can define relationships in your query without changing any settings.

*   Combining multiple queries into one will give you much better performance than any other way of getting this data, e.g. nesting Siteglide include tags inside each other.

## Glossary of Terms

Here are a few of the terms you may come across in this topic:

| Term                                         | Definition                                                                                                                                                                                                                                                                                                                                                                                        |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| relational database                          | A relational database describes a database comprised of tables, where there may be predefined relationships between records in different tables. platformOS's database is a kind of relational database.                                                                                                                                                                                          |
| join                                         | In many query languages e.g. SQL, a join defines how two tables are linked together. In platformOS, a join on property is used to define which field should be used to find other related\_records.                                                                                                                                                                                               |
| tables                                       | In platformOS, as in many other databases, a table is a set of data which contains records of a certain type, with a certain set of properties.                                                                                                                                                                                                                                                   |
| records                                      | In platformOS, as in many other databases, a record is a single entry of data in a database.                                                                                                                                                                                                                                                                                                      |
| related\_records                             | In platformOS, records which share a relationship. It can be single\:single, many\:many or single\:many. This is effectively the same concept as a datasource.                                                                                                                                                                                                                                    |
| datasource                                   | In Siteglide, a datasource is where there is a relationship between records in the same table or in a different table, and data can be "sourced" from that other table. It can be single\:single, many\:many or single\:many. This is effectively the same concept as platformOS's related\_records.                                                                                              |
| datasource and datasource\_multi field types | In Siteglide, some fields can be given the datasource and datasource\_multi field types: [Field Types](<../Siteglide Developer Documentation/Field Types.md>) These are designed to store IDs of other records to make joining easy. However, you can also in GraphQL join other types of fields.                                                                                                 |
| foreign                                      | In platformOS, a foreign property refers to a property outside of the current record. The foreign property is matched with the join on property in order to fetch related records which share a relationship.                                                                                                                                                                                     |
| data graph                                   | In computing a data graph describes the relationships between different nodes of data. Think of a node like a city and the relationships like roads. &#xA;&#xA;One of the reasons GraphQL is called GraphQL is that it is trying to give queries an intuitive graph-like structure- we define the relationships in the query itself, and the results return with the same relationship structure. |

# Building your first query using Related Records

The great thing about related records being as flexible as they are is that there are a lot of examples we could choose from. Our first example though will try to keep things simple by fetching Blog posts with their associated authors.

# Step 1) Write your query to fetch Blog Posts

We've already covered how to write a records query and filter it so it contains only blog posts. Here's an example:

```graphql
query blogsWithAuthors {
  records(
    per_page: 20,
    filter: {
      table: {
        value: "module_3"
      }
    }
  ) {
    results {
      id
      properties
    }
  }
}
```

## Step 2) Find out which fields match across the two tables

Since these two modules - the Blog and Authors Module - are both created by Siteglide, they already store the information needed to join them inside their properties. We only need to look at the existing properties in detail to get the information we need to build our query.&#x20;

There are several ways to do this. One of the easiest to do on an everyday basis is to use [Introducing Siteglide CLI](<../Siteglide Developer Documentation/Introducing Siteglide CLI.md>) to `pull` your site, then to look in marketplace\_builder/form\_configurations:

> ├───forms
> │       form_1.liquid
> │       form_2.liquid
> │       form_3.liquid
> │
> ├───modules
> │   │   module_17.liquid
> │   │   module_3.liquid
> │   │   module_6.liquid
> │   │
> │   └───module_14
>

For this exercise, we'd be looking at `module_3` for blog and `module_6 `for authors.

In Blog, scroll down or use ctrl-f to search for `author` The form configuration will contain both the human-friendly name and the Siteglide ID for each field:

> module_field_3_4:
>       name: Author
>       type: datasource
>       live: true
>       hidden: false
>       order: 0
>       editable: true
>       datasource_id: module_6
>       required: false
>       validation: {}

Great! It's a datasource field, which is pefect, because it will already be set up to contain IDs of Author records related to each Blog record. We don't need to look at the Author record now to know that the `module_field_3_4` property of the Blog and the `id` of the Author should match. Sometimes, you'll need to look at both.&#x20;

Since this is a GraphQL tutorial- here's an alternative way to check the form-configurations- using a query (see how we use filter to look for only the Blog and Author configurations)!

```graphql
query findBlogAndAuthorProperties {
  admin_forms(filter: {name: {value_in: ["module_3","module_6"]}}) {
    results {
      fields
    }
  }
}
```

In the Siteglide Admin, we can check that some of the Blogs already have authors set in the `datasource` field, in this case this Blog item has an Author ID of `100 `in the field:

![](../../assets/evgRNmT8_vPrVj3LFkRMj_image.png)

## Step 3) Add related\_records inside results

To start with, look inside results in explorer: `related_record` and `related_records` appear as possible results. By including these special objects inside the results object, we can define a branching tree of related results.

![](../../assets/XS1E-AqyXEMjjg9DITVoo_image.png)

The two options are similar but have one key difference:

*   related\_record - Use this to define a 1:1 or a many:1 relationship. It will return a single record as an object. This may give you better performance, if you know for example there's only one author.

*   related\_records - Use this to define a 1\:many or a many\:many relationship. It will return multiple records as an array.

The main reason to pay attention to which you choose is that it will change the way you structure your Liquid to access the data- remember if there is an array in the data you may need to loop over it in order to access it.

For now, let's use related\_record, as we have a `datasource `field to join with, and only one Author per Blog `record`:

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      related_record() {
        
      }
    }
  }
}

```

## Step 4) Rename the related\_record

Remember, we use a string with no spaces and a colon to "rename" things in GraphQL. It's a good idea to rename this related\_record to describe what it will return. In this case, it describes a single author.

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      author: related_record() {
        
      }
    }
  }
}

```

&#x20;This will make it easier to understand the results and allow you to add other `related_records `in future (it won't let you if names clash).&#x20;

## Step 5) Set the join\_on\_property

As mentioned in the glossary, the `join_on_property `is used to define the property in the *current* result record which will be used to match with a related record. In step 3 we worked out it was `module_field_3_4`.&#x20;

*   We don't need to write the value of the module\_field\_3\_4 field, just the Siteglide field ID.&#x20;

*   you also don't need to add `properties` before the field ID, as you may when filtering a query; here, platformOS works this out automatically

*   this goes inside the curly brackets as an argument

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      author: related_record(
        join_on_property: "module_field_3_4"
      ) {
        
      }
    }
  }
}

```

## Step 6 - Set the Foreign Property

The foreign property is the counterpart to the join\_on\_property, but it refers to the property in the record we are looking for, in this case the Author record is the record, and the property is `id`.

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      author: related_record(
        join_on_property: "module_field_3_4",
        foreign_property: "id"
      ) {
        
      }
    }
  }
}

```

Note the syntax is the same, even though `module_field_3_4 `is a custom property and `id` is a core property in platformOS.

## Step 7 - Set the Table

`table` here is a filter, despite not being inside a filter object. It must be set to describe the table we should look in for these related records. In this case, the ID of the Authors module: `module_6`

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      author: related_record(
        join_on_property: "module_field_3_4",
        foreign_property: "id",
        table: "module_6"
      ) {
        
      }
    }
  }
}

```

## Step 8 - Results

We've already defined which results we want for Blog items, and that we want to return a related author per blog item, but we also need to define which authors properties should be returned.&#x20;

We could return the whole properties object, but where possible it's worth being extra efficient when working with relationships. There is more work for the query to do, and it may run more slowly. Maybe we just need the author's name and an image (I use the information we looked at in step 2 to find the module\_6 image field ID)?

The results go in the new object under `related_record` after the arguments; no `results `key is needed:

```graphql
query blogsWithAuthors {
  records(per_page: 20, filter: {table: {value: "module_3"}}) {
    results {
      id
      properties
      author: related_record(
        join_on_property: "module_field_3_4",
        foreign_property: "id",
        table: "module_6"
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}

```

That's the query itself done!

## Step 9 - Working with the Results

The results in JSON may look like the below (we've minimised Blog properties which aren't useful to the example):

> {
>   "data": {
>     "records": {
>       "results": [
>         {
>           "id": "97",
>           "properties": {...},
>           \# note - this record 97 did NOT have a match with an author. Maybe the Author has been deleted or maybe the ID has not been stored in the field we're joining on.
>
>           "author": null 
>         },
>         {
>           "id": "8",
>           "properties": {...},
>           \# note this blog item with ID of 8 DID match with an author- the author's fields we asked for are below!
>           "author": { 
>             "name": "Jese Leos",
>             "image": "https://cdn.staging.oregon.platform-os.com/instances/10093/assets/jese-leos.png"
>           }
>         },
>         {
>           "id": "10",
>           "properties": {...},
>           "author": {
>             "name": "Karen Nelson",
>             "image": "https://cdn.staging.oregon.platform-os.com/instances/10093/assets/karen-nelson.png"
>           }
>         }
>       ]
>     }
>   }
> }

As always, when outputting in Liquid, you can use dot notation (see [Liquid Dot Notation](<../Siteglide Developer Documentation/Liquid Dot Notation.md>) or [Tutorial 5 - Using Liquid to run GraphQL queries on your Site](docId:2Sc1gj360B5yVDj22V4pK)) to access the results, until you get to an array. Since we only asked for a single author, we can use dot notation inside the blog record to access the author. We still need to loop over the blog results as always:

```liquid
{% graphql blogs_with_authors = "blogsWithAuthors" %}
{% for blog in blogs_with_authors.records.results %}
  <h2>{{blog.properties.module_field_3_1}}</h2>
  <div>
    By: {{blog.author.name}}
    <img src="{{blog.author.image | asset_url}}">
  </div>
{% endfor %}
```

# A many:1 alternative

What if you need this to fetch information the other way around, e.g. you are on a page which displays information about an author and you wish to display a list of the Author's Blog Posts? An additional aspect to this is that this is a 1\:many relationship- it's no problem- we'll use `related_records` plural instead of `related_record` to return an array instead of an object.

Starting with the query above, lets make some changes:

## Step 1) Change the initial query to fetch Authors first and rename:

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      author: related_record(
        join_on_property: "module_field_3_4",
        foreign_property: "id",
        table: "module_6"
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}
```

## Step 2) Change join on property to Author's ID

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      author: related_record(
        join_on_property: "id", #edit join
        foreign_property: "id",
        table: "module_6"
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}
```

## Step 3) Change foreign property to Blog's property which contains Author's ID

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      author: related_record(
        join_on_property: "id",#edit join
        foreign_property: "module_field_3_4", # edit foreign
        table: "module_6"
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}
```

## Step 4) Change related table to Blog

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      author: related_record(
        join_on_property: "id",#edit join
        foreign_property: "module_field_3_4", # edit foreign
        table: "module_3" # edit table
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}
```

## Step 5) Change related\_record to related\_records and rename

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      articles: related_records(
        join_on_property: "id",#edit join
        foreign_property: "module_field_3_4", # edit foreign
        table: "module_3" # edit table
      ) {
        name: property(name: "name")
        image: property(name: "module_field_6_4")
      }
    }
  }
}
```

## Step 6) Change Results

```graphql
query AuthorsAndTheirArticles { #renamed
  records(per_page: 20, filter: {table: {value: "module_6"}}) { #change table
    results {
      id
      properties
      articles: related_records(
        join_on_property: "id",#edit join
        foreign_property: "module_field_3_4", # edit foreign
        table: "module_3" # edit table
      ) {
        title: property(name: "module_field_3_1")
        slug: property(name: "slug")
      }
    }
  }
}
```

## Step 7) Liquid example

```liquid
{% graphql authors_and_their_articles = "AuthorsAndTheirArticles" %}
{% for author in authors_and_their_articles.records.results %}
  <h2>{{author.properties.name}}</h2>
  <div>
    Articles Published:
    <ul>
      {% for article in author.articles %}
        <li>
          <a href="/siteglide-blogs/{{article.slug}}>{{article.title}}</a>
        </li>
      {% endfor %}
    </ul>
  </div>
{% endfor %}
```

# Further Learning

Next, you could experiment with some of these options:

*   using filters to further filter related records e.g. Authors with Blog posts which are enabled

*   using `related_users` an alternative to `related_records `which fetches CRM users with a relationship to your record. You don't need to specify a table, but join and foreign properties work the same.

*   Additional nesting. Inside your related\_records results, you can define related\_records again. This allows you to build a complex results tree containing as many layers of related results as you like, for example adding to our example above- you could return the categories of each Blog the Author had published- and display a list of category names. 


