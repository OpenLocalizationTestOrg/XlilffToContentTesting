---
ms.openlocfilehash: f88acd405e60420fb019b3de1678cf107a9456d1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Now that you've learned about what kinds of queries you can create, let's use the Data Explorer in the Azure portal to retrieve and filter your product data.

In your Data Explorer window, by default, the query on the **Document** tab is set to `SELECT * FROM c` as shown in the following image. This default query retrieves and displays all documents in the collection.

![Default query in Data Explorer is SELECT * FROM c](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a>Create a new query

1. In Data Explorer, click **New SQL Query**. The default query on the new  **Query 1** tab is again `SELECT * from c`, which will return all documents in the collection. 

1. Click **Execute Query**. This query returns all results in the database.

    ![Change the default query by adding ORDER BY c._ts DESC and clicking Apply Filter](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. Now, let's run some of the queries discussed in the previous unit. On the query tab, delete `SELECT * from c`, copy and paste the following query, and then click **Execute Query**:

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    The results return the product whose `id` is 1.

    ![Query for an id of 1](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. Delete the previous query, copy and paste the following query, and click **Execute Query**. This query returns the price, description, and product ID for all products, ordered by price, in ascending order.
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a>Summary

You've now completed some basic queries on your data in Azure Cosmos DB. 