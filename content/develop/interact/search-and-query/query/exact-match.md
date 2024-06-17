---
categories:
- docs
- develop
- stack
- oss
- rs
- rc
- oss
- kubernetes
- clients
description: Perform simple exact match queries
linkTitle: Exact match
title: Exact match queries
weight: 1
---

An exact match query allows you to select all documents where a field matches a specific value. 

You can use exact match queries on several field types. The query syntax varies depending on the type. 

The examples in this article use a schema with the following fields:

| Field name | Field type |
| ---------- | ---------- |
| `description`| `TEXT` |
| `condition` | `TAG` |
| `price` | `NUMERIC` |

You can find more details about creating the index and loading the demo data in the [quick start guide]({{< relref "/develop/get-started/document-database" >}}).

## Numeric field

To perform an exact match query on a numeric field, you need to construct a range query with the same start and end value:

```
FT.SEARCH index "@field:[value value]"

or

FT.SEARCH index "@field:[value]" DIALECT 5

or

FT.SEARCH index "@field==value" DIALECT 5
```

See [DIALECT 5]({{< relref "/develop/interact/search-and-query/advanced-concepts/dialects" >}}#dialect-5) for more information.

As described in the [article about range queries]({{< relref "/develop/interact/search-and-query/query/range" >}}), you can also use the `FILTER` argument:

```
FT.SEARCH index "*" FILTER field start end
```

The following examples show you how to query for bicycles with a price of exactly 270 USD:

```
FT.SEARCH idx:bicycle "@price:[270 270]"
```

```
FT.SEARCH idx:bicycle "@price:[270]"
```

```
FT.SEARCH idx:bicycle "@price==270"
```

```
FT.SEARCH idx:bicycle "*" FILTER price 270 270
```


## Tag field

A tag is a short sequence of text, for example, "new" or "Los Angeles". 

{{% alert title="Important" color="warning" %}}
If you need to query for short texts, use a tag query instead of a full-text query. Tag fields are more space-efficient for storing index entries and often lead to lower query complexity for exact match queries.
{{% /alert  %}}

You can construct a tag query for a single tag in the following way:

```
FT.SEARCH index "@field:{tag}"
```

{{% alert title="Note" color="warning" %}}
The curly brackets are mandatory for tag queries.
{{% /alert  %}}

This short example shows you how to query for new bicycles:

```
FT.SEARCH idx:bicycle "@condition:{new}"
```

The following characters must be escaped to be used in an exact match query involving tags:

`$` - used to define a variable such as `$params`.

`{}` - used to define `TAG` query attributes.

`\` - used to indicate that the succeeding character should be handled as literal.

`|` - used for the logical OR operator.

## Full-text field

A detailed explanation of full-text queries is available in the [full-text queries documentation]({{< relref "/develop/interact/search-and-query/query/full-text" >}}). You can also query for an exact match of a phrase within a text field:

```
FT.SEARCH index "@field:\"phrase\""
```

{{% alert title="Important" color="warning" %}}
The phrase must be wrapped by escaped double quotes for an exact match query.

You can't use a phrase that starts with a [stop word]({{< relref "/develop/interact/search-and-query/advanced-concepts/stopwords" >}}).
{{% /alert  %}}

Here is an example for finding all bicycles that have a description containing the exact text 'rough terrain':

```
FT.SEARCH idx:bicycle "@description:\"rough terrain\""
```