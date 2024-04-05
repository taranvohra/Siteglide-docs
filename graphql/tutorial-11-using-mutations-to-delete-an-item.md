
# Introduction

In this article we'll look at how to delete a record with a GraphQL mutation, but first of all, let's look at what deleting a record means (and how to undo it!).

# What is Soft Deletion?

When we delete records with GraphQL, they are soft-deleted by default.&#x20;

If you accidentally delete data, it may have been "soft deleted", and you may be able to recover it if you act quickly.

Think of soft-deletion as being a bit like a recycle bin:

*   &#x20;Records are given a deleted\_at property with a date in 30 days time in [platformOS's datetime format](https://documentation.platformos.com/developer-guide/properties/properties) (ISO 8601)

*   When the date is reached, the record will be permanently deleted.

*   They are removed from the results of all queries by default (this includes all Siteglide tags)

*   You can get ordinary `records`queries to display soft-deleted records (only), see below:

```graphql
query seeDeletedRecords {
  records(
    per_page: 20,
    filter: {
      deleted_at: {
        exists: true
      }
    },
    sort: {
      deleted_at: {
        order: ASC
      }
    }
  ) {
    results {
      id
      deleted_at
    }
  }
}
```

The results will be the same as in a normal query; it's helpful to add deleted\_at to the results so you can see when they will be permanently deleted:

```graphql
{
  "data": {
    "record_delete": {
      "id": "3",
      "deleted_at": "2024-01-02T15:15:55.666Z"
    }
  }
}
```

## Recovering Soft Deleted Records

If a record has been soft-deleted by mistake, and has not yet been permanently deleted, you can recover it by setting the deleted\_at property to null. Make sure to use the query above to find the ID of the record you want to recover and pass it in as a variable to the mutation below.

```graphql
mutation recoverSoftDeletedRecord($id: ID!) {
  record_update(id: $id, record: {deleted_at: "null"}) {
    id
    deleted_at
  }
}
```

After changing `deleted_at` to null, the record becomes an ordinary record. It appears in queries and is no longer scheduled to be deleted. The mutation results should confirm that `deleted_at` is no longer set:

```graphql
{
  "data": {
    "record_update": {
      "id": "3",
      "deleted_at": null
    }
  }
}
```

If you want to extend the amount of time the record stays in soft-deleted state, you can change the deleted\_at property to set the deletion date to be further in the future (but this is an advanced method we won't cover here).

# Deleting a Record

![Building a record_delete mutation in explorer](../../assets/RpUauUIHHJsnz0a2sUhqt_image.png)

## Step 1) Find the ID of the Record you wish to Delete

Use another query to find the ID.

## Step 2) Add the mutation keyword and a name

```graphql
mutation deleteRecord {

}
```

## Step 3) Add the records\_delete mutation type

```graphql
mutation deleteRecord {
  record_delete() {}
}
```

## Step 4) Add the id of the record you wish to delete, with a variable if you like

```graphql
mutation deleteRecord($id: ID!) {
  record_delete(
    id: $id
  ) {}
}
```

## Step 5) Add a result to confirm the mutation's success

```graphql
mutation deleteRecord($id: ID!) {
  record_delete(
    id: $id
  ) {
    id
    deleted_at
  }
}
```

A successful deletion may look like this:

```graphql
{
  "data": {
    "record_delete": {
      "id": "3",
      "deleted_at": "2024-01-02T15:15:55.666Z"
    }
  }
}
```

# Summary and Further Learning

You've now learned how to perform all four CRUD operations using GraphQL:

1.  Create

2.  Read (query)

3.  Update

4.  Delete

If you wish to programatically create, update or delete multiple records at once, it may be more efficient to use the following mutation types instead of looping:

*   records\_create\_all

*   records\_update\_all

*   records\_delete\_all

Be very careful with those and make sure you test with data which is backed up. We recommend using `any_table: false` as a precaution.

In these mutation types, you use a `filter` to determine which records should be affected instead of only passing `id`. You need to add `count `to the results.

# Next Time

Next time we'll look at how you can use a query to access data from multiple relational database tables, or in other words, view data from Siteglide datasources.