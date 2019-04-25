---
ms.openlocfilehash: 507490840350dc7949fd473e8db8735e40191d32
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Using the two documents you added to the database as the target of our queries, let's walk through some query basics. Azure Cosmos DB uses SQL queries, just like SQL Server, to perform query operations. All properties are automatically indexed by default, so all data in the database is instantly available to query.

## <a name="sql-query-basics"></a>SQL query basics
Every SQL query consists of a SELECT clause and optional FROM and WHERE clauses. In addition, you can add other clauses like ORDER BY and JOIN to get the information you need.

A SQL query has the following format:

```sql
SELECT <select_list>
[FROM <optional_from_specification>]
[WHERE <optional_filter_condition>]
[ORDER BY <optional_sort_specification>]
[JOIN <optional_join_specification>]
```

## <a name="select-clause"></a>SELECT clause

The SELECT clause determines the type of values that will be produced when the query is executed. A value of `SELECT *` indicates that the entire JSON document is returned.

**Query**

```sql
SELECT *
FROM Products p
WHERE p.id ="1"
```

**Returns**

```json
[
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
                "width": 6,
                "height": 8,
                "depth": 1
            }
        },
        "_rid": "iAEeANrzNAAJAAAAAAAAAA==",
        "_self": "dbs/iAEeAA==/colls/iAEeANrzNAA=/docs/iAEeANrzNAAJAAAAAAAAAA==/",
        "_etag": "\"00003a02-0000-0000-0000-5b9208440000\"",
        "_attachments": "attachments/",
        "_ts": 1536297028
    }
]
```

Or, you can limit the output to include only certain properties by including a list of properties in the SELECT clause. In the following query, only the ID, manufacturer, and product description are returned.

**Query**

```sql
SELECT
    p.id,
    p.manufacturer,
    p.description
FROM Products p
WHERE p.id ="1"
```

**Returns**

```json
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a>FROM clause

The FROM clause specifies the data source upon which the query operates. You can make the whole collection the source of the query or you can specify a subset of the collection instead. The FROM clause is optional unless the source is filtered or projected later in the query.

A query such as `SELECT * FROM Products` indicates that the entire Products collection is the source over which to enumerate the query.

A collection can be aliased, such as `SELECT p.id FROM Products AS p` or simply `SELECT p.id FROM Products p`, where `p` is the equivalent of `Products`. `AS` is an optional keyword to alias the identifier.

Once aliased, the original source cannot be bound. For example, `SELECT Products.id FROM Products p` is syntactically invalid because the identifier "Products" cannot be resolved anymore.

All properties that need to be referenced must be fully qualified. In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings. Therefore, `SELECT id FROM Products p` is syntactically invalid because the property `id` is not bound.

### <a name="subdocuments-in-a-from-clause"></a>Subdocuments in a FROM clause
The source can also be reduced to a smaller subset. For instance, to enumerate only a subtree in each document, the subroot could then become the source, as shown in the following example:

**Query**

```sql
SELECT *
FROM Products.shipping
```

**Results**

```json
[
    {
        "weight": 1,
        "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
        }
    },
    {
        "weight": 2,
        "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
        }
    }
]
```

Although the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example. Any valid JSON value (that's not undefined) that can be found in the source is considered for inclusion in the result of the query. If some products don’t have a `shipping.weight` value, they are excluded in the query result.

**Query**

```sql
SELECT *
FROM Products.shipping.weight
```

**Results**

```json
[
    1,
    2
]
```

## <a name="where-clause"></a>WHERE clause
The WHERE clause specifies the conditions that the JSON documents provided by the source must satisfy in order to be included as part of the result. Any JSON document must evaluate the specified conditions to **true** to be considered for the result. The WHERE clause is optional.

The following query requests documents that contain an ID whose value is 1:

**Query**

```sql
SELECT p.description
FROM Products p
WHERE p.id = "1"
```

**Results**

```json
[
    {
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="order-by-clause"></a>ORDER BY clause

The ORDER BY clause enables you to order the results in ascending or descending order.

The following ORDER BY query returns the price, description, and product ID for all products, ordered by price, in ascending order:

**Query**

```sql
SELECT p.price, p.description, p.productId
FROM Products p
ORDER BY p.price ASC
```

**Results**

```json
[
    {
        "price": "14.99",
        "description": "Quick dry crew neck t-shirt",
        "productId": "33218896"
    },
    {
        "price": "49.99",
        "description": "Black wool pea-coat",
        "productId": "33218897"
    }
]
```

## <a name="join-clause"></a>JOIN clause

The JOIN clause enables you to perform inner joins with the document and the document subroots. So in the product database, for example, you can join the documents with the shipping data.

In the following query, the product IDs are returned for each product that has a shipping method. If you added a third product that didn't have a shipping property, the result would be the same because the third item would be excluded for not having a shipping property.

**Query**

```sql
SELECT p.productId
FROM Products p
JOIN p.shipping
```

**Results**

```json
[
    {
        "productId": "33218896"
    },
    {
        "productId": "33218897"
    }
]
```

## <a name="geospatial-queries"></a>Geospatial queries

Geospatial queries enable you to perform spatial queries using GeoJSON Points. Using the coordinates in the database, you can calculate the distance between two points and determine whether a Point, Polygon, or LineString is within another Point, Polygon, or LineString.

For product catalog data, this would enable your users to enter their location information and determine whether there were any stores within a 50-mile radius that have the item they're looking for.

## <a name="summary"></a>Summary

Being able to quickly query all your data after adding it to Azure Cosmos DB and using familiar SQL query techniques can help you and your customers to explore and gain insights into your stored data.