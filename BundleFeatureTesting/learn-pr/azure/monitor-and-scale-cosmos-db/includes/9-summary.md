---
ms.openlocfilehash: f481f3a8858480b471f04f801d4b5810307fecaa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---

You now have the knowledge and tools to model, measure, and monitor the efficiency of your Cosmos DB collections. 

We've optimized the Orders collection for the online retail scenario. This database can now scale according to the needs of the business. You can apply these methods to your own scenario to make the most of the Cosmos DB capacity you've allocated.

## <a name="clean-up"></a>Clean up

It's important that you clean up any unused collections. You're charged for the configured capacity not how much of the database is used. For this module, we make these resources available to you free of charge. But you should get into the habit of deleting resources when you're done with them.

1. Open the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).

2. Search for sandbox resource group: <rgn>Sandbox Resource Group</rgn>.

3. Select your Cosmos DB account.

4. Go to **Data Explorer**.

5. To delete the mslearn database, select the ellipse **...** next to the database name.

1. Select **Delete**.

1. Enter the name of the database that you want to delete.

If you want to delete each collection individually, you select the ellipse **...**  next to the collection and select **Delete**.

## <a name="resources"></a>Resources

To learn more about Cosmos DB, see the following resources:

- [Cosmos DB documentation](https://docs.microsoft.com/azure/cosmos-db/): This is the official Microsoft Documentation for Cosmos DB.
- [Cosmos DB calculator](https://www.documentdb.com/capacityplanner#): Calculates Request Units for different workloads which is useful for estimating the volume of your JSON payload.
- [Cosmos DB benchmark code](https://github.com/Azure/azure-cosmos-dotnet-v2/tree/master/samples/documentdb-benchmark): The utility code, that you used in this module, is based on this code.
