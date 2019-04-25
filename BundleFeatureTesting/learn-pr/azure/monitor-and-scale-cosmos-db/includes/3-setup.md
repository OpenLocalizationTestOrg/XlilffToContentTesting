---
ms.openlocfilehash: 2e7d388462acf85faac888800693548786d11ad3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In this unit, you'll create a Cosmos DB account and use a console application to populate the database.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-your-database-account"></a>Create your database account

A database account is a container for multiple Cosmos DB databases.

1. Add a unique name for your database account. The database account name must be unique across all Cosmos DB instances. Use the command below to generate a random database account name, using the **Bash** `$RANDOM` variable, and store it in an environment variable to use later.

    ```bash
    export COSMOS_NAME=cosmos$RANDOM
    ```

1. Create a Cosmos DB account using the following command:

    ```bash
    az cosmosdb create --resource-group <rgn>Sandbox Resource Group</rgn> --name $COSMOS_NAME
    ```

The database account can take 4-5 minutes to provision. Keep reading while the account is being created.

## <a name="cosmos-db-concepts-resources-partitioning-and-indexing"></a>Cosmos DB concepts: resources, partitioning, and indexing

### <a name="cosmos-db-resources"></a>Cosmos DB resources

A Cosmos DB account is a container for one or more _databases_. A Cosmos DB database is a container for one or more _collections_. A collection contains _documents_. A document is an unstructured set of key value pairs, read and written in JSON format.

### <a name="partitioning-in-cosmos-db"></a>Partitioning in Cosmos DB

 _Partitioning_ is the distribution and grouping of your data across the underlying resources. Documents are grouped in a partition based on the value of the partition key. You specify the partition key when you create the collection. To understand the partition key concept better, let's review the property and values in the following JSON example document.

 [!code-json[](../code/Order.json)]

Any of these properties, or a combination of them, can be a partition key. For example, where you defined the partition key as a combination of the properties **Category** and **Merchant**, any documents that have matching values for **Category** and **Merchant** are grouped in the same partition.

An effective partitioning strategy distributes data and access evenly across partitions, and across time. Querying documents from within the same partition is less expensive than across partitions.

You choose how to partition your data at design time. The partitioning configuration can't be changed after a collection is provisioned.

We examine partitioning concepts and examples in detail in Units 4 and 5.

### <a name="indexing-in-cosmos-db"></a>Indexing in Cosmos DB

An index is a catalog of document properties and their values. It includes links to documents that contain properties equal to each property value. Indexing makes searching a collection more efficient. But the search efficiency is balanced with the resources required to insert or change a document. When a document is inserted or changed, Cosmos DB has to update the index. The optimal indexing strategy for your collection depends on your workload.

Unlike partitioning, you can change indexing at run-time.

We look at indexing in Units 6 and 7.

## <a name="set-environment-variables-for-endpoint-and-keys"></a>Set environment variables for endpoint and keys

1. After the database is created, run the following command to store its endpoint in an environment variable.

    ```bash
    export ENDPOINT=$(az cosmosdb list --resource-group <rgn>Sandbox Resource Group</rgn> \
            --output tsv --query [0].documentEndpoint)
    ```

1. Run the following command to store the access key in an environment variable.

    ```bash
    export KEY=$(az cosmosdb list-keys --resource-group <rgn>Sandbox Resource Group</rgn>  \
            --name $COSMOS_NAME --output tsv --query primaryMasterKey)
    ```

## <a name="create-your-database-and-collections"></a>Create your database and collections

1. Create a database called `mslearn` in your CosmosDB account. We only need one database for these exercises.

    ```bash
    az cosmosdb database create --resource-group <rgn>Sandbox Resource Group</rgn> \
            --name $COSMOS_NAME --db-name mslearn
    ```

1. Create the first collection.

    We're going to create three collections to compare different partitioning strategies, and workloads.

    We allocate a smaller capacity to this collection to demonstrate overloading it. The partition key for this collection is the unique identifier of the order. In this case, the partition isn't important as the collection is smaller than a single partition.

    ```bash
    az cosmosdb collection create --resource-group <rgn>Sandbox Resource Group</rgn> \
            --name $COSMOS_NAME --db-name mslearn --collection Small \
            --partition-key-path /id --throughput 400
    ```

1. Create the second collection.

    This collection uses an Order Item's product **category** as the partition key. We explore the consequences of this choice as we go through the exercises in this module.

    ```bash
    az cosmosdb collection create --resource-group <rgn>Sandbox Resource Group</rgn> \
            --name $COSMOS_NAME --db-name mslearn --collection HotPartition \
            --partition-key-path /Item/Category --throughput 7000
    ```

1. Create a third collection.

    This collection partitions the documents by the Order Item's unique product **identifier**.

    ```bash
    az cosmosdb collection create --resource-group <rgn>Sandbox Resource Group</rgn> \
            --name $COSMOS_NAME --db-name mslearn --collection Orders \
            --partition-key-path /Item/id --throughput 7000
    ```

## <a name="populate-your-collections"></a>Populate your collections

We use an open-source C# console application to populate your collections. This application generates random order documents and inserts them into your collections. We also use this application in later units to query the collections.

1. Clone the console application repository from GitHub. Run the following command in the sandbox environment.

    ```bash
    git clone https://github.com/MicrosoftDocs/mslearn-monitor-azure-cosmos-db
    ```

1. Change into the application's directory.

    ```bash
    cd mslearn-monitor-azure-cosmos-db/ExerciseCosmosDB
    ```

1. Check your environment variables. The console application needs the environment variables to connect to the database. If your cloud shell times out, then you need to set these and the `COSMOS_NAME` variable again. You can reset the `COSMOS_NAME` value by running the following command.

    ```bash
    export COSMOS_NAME=$(az cosmosdb list --output tsv --query [0].name)
    ```

    You can reset your `ENDPOINT` and `KEY` variables by running the following commands.

    ```bash
    export ENDPOINT=$(az cosmosdb list --resource-group <rgn>Sandbox Resource Group</rgn> \
            --output tsv --query [0].documentEndpoint)
    ```

    ```bash
    export KEY=$(az cosmosdb list-keys --resource-group <rgn>Sandbox Resource Group</rgn>  \
            --name $COSMOS_NAME --output tsv --query primaryMasterKey)
    ```

1. Populate the `Small` collection.

    ```bash
    dotnet run -- -c Small -o InsertDocument -n 4000 -p 10
    ```

    Again, the application takes a few minutes to run, as we need to populate the database with enough data that we can discern metrics for different partitioning and indexing strategies. To populate this collection, the console application is running with the following options:

    Option|Value|Description
    ------|-----|-----------
    -c|Small|The name of the collection to use
    -o|InsertDocument|The name of the task to run
    -n|2000|The number of times to run
    -p|10|The degree of parallelism to use. That's the number of threads used to do the experiment. The higher this number, the greater the demand on the collection.

    The first time you run the application, it shows a welcome message.

    You can see the other options for this application by running `dotnet run -- --help`.

    While the console application runs, you see one line printed per second that shows the status and Request Units needed for the database writes.

1. Populate the `HotPartition` collection.

    ```bash
    dotnet run -- -c HotPartition -o InsertDocument -n 20000 -p 10
    ```

1. Populate the `Orders` collection.

    ```bash
    dotnet run -- -c Orders -o InsertDocument -n 20000 -p 10
    ```
