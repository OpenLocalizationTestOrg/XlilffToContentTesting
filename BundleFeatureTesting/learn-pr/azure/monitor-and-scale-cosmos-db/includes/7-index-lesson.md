---
ms.openlocfilehash: 4370d6ebee5f1dc65590a83cf93f5ce95960f5e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
An index is extra information that sits alongside a collection to make querying more efficient. Queries use the index to locate documents.

The index is updated every time a document is updated or added to a collection. That update adds to the request units used for each write operation.

The right indexing strategy depends on the patterns of access to your collections. Read-intensive workloads call for a different indexing strategy from write-intensive ones. Unlike the partitioning configuration, you can change the Cosmos DB indexing configuration after a collection is provisioned. When your database is up and running, measure the performance of your index configuration and tune it.

By default, all document properties in a Cosmos DB are indexed.

## <a name="indexing-modes-consistent-lazy-none"></a>Indexing modes: consistent, lazy, none

The three indexing modes you can use with Cosmos DB are:

- **Consistent**: The index is updated synchronously every time a new document is written to the collection. New queries on the collection use the updated index right away. Query results are consistent with the updated documents in the collection.

- **Lazy**: The index is updated at a lower priority. The reads and writes from the collection take a higher priority. In lazy mode, writes are cheaper because the index isn't updated immediately. When the index is fully updated depends on the demands on the collection. Query results don't include the updated documents until the index is consistent with the collection.

- **None**:  No index is created. Queries are expensive on collections that aren't indexed. If you're using your Cosmos DB collection to read records directly rather than querying the collection, then it's possible to avoid the overhead of indexing.

## <a name="indexing-mode-for-the-orders-collection"></a>Indexing mode for the Orders collection

One scenario for the Orders collection workload is write-intensive:

- Orders are placed or updated at any time of the day
- Reports are generated less frequently for the quantity and type of items sold

In this case, you could choose to keep the indexing on all properties of the documents but set the indexing mode to **lazy**.

## <a name="changing-the-indexing-strategy"></a>Changing the indexing strategy

The index configuration can be changed at any time.

- If you add properties to the index configuration, Cosmos DB parses your collections, and updates the index. The index uses more storage.
- If you reduce the number of properties from the index, Cosmos DB removes this information from your index. The index uses less storage.

## <a name="adding-document-properties-to-the-index"></a>Adding document properties to the index

To include a document property in the index, you add its path to the index configuration. For example,

- To include the Customer Email property in the index, add `Customer/Email/?` to the `includedPaths` array.
- To exclude a property, add it to the `excludedPaths` array.

In the following example, the indexing mode is set to consistent, and some of the properties are indexed.

[!code-json[](../code/index-partial.json)]
