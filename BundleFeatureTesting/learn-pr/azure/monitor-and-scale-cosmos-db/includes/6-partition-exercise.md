---
ms.openlocfilehash: ec0f8c1cfad4f18ff8f6e5428d04dac0ce1afadc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In the previous unit, we learned how to design an efficient partitioning strategy. Recall that you can't change the partitioning strategy of your Cosmos DB collection after it's created. So, it's essential to understand how to partition the collection efficiently.

## <a name="measure-impact-of-partitions-on-throughput"></a>Measure impact of partitions on throughput

1. In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), go to your Cosmos DB account and select **Metrics**.
1.  Select the **Throughput** tab

1. Filter on the **mslearn** database.

    ![Screenshot that shows Throughput tab's database filter. ](../media/6-metrics-throughput-database-filter.png)

### <a name="review-unevenly-distributed-partitions-for-throughput"></a>Review unevenly distributed partitions for throughput

1. Filter on the **HotPartition** collection.

1. Review the results. You see that the collection is using two partitions with the 7000 RU/s divided between them.

1. On the **Number of requests** chart, find the time when you populated this collection. You should see a peak in requests at this time.

    ![Screenshot that shows the Cosmos DB requests over time chart](../media/6-request-peak.png)

1. Enter that time on the **Max consumed RU/s by each partition key range** chart and click **Apply**.

    ![Screenshot that shows the Cosmos DB uneven partition access distribution chart](../media/6-hot-partition-throughput.png)

    Notice the imbalance between the two partitions. Most of the requests are for the first partition, which is being over-used. The other partition is being under-used. The **HotPartition** collection isn't configured to efficiently use its total allocated request units, which is 7000 RU/s. The first partition is in danger of being throttled while the second has plenty of capacity available.

1. Select the blue column for first partition (Partition 0). With the partition selected, you see a list to the right of the chart that shows the partition key values that are dominating the partition. In this case, `Books` make up the largest logical partition.

### <a name="review-evenly-distributed-partitions-for-throughput"></a>Review evenly distributed partitions for throughput

1. Now filter on the **Orders** collection.

1. On the **Number of requests** chart, find the time you populated this collection.

1. Enter that time on the **Max consumed RU/s by each partition key range** chart and click **Apply**.

    ![Cosmos DB even partition throughput chart](../media/6-even-partitions-throughput.png)

    You see that the requests are balanced between the two partitions. The **Orders** collection has a more efficient partitioning scheme as it uses the available capacity.

    The line on the chart indicates the throughput limit of each partition. You see that we're well within our configured limit.

## <a name="measure-impact-of-partitions-on-storage"></a>Measure impact of partitions on storage

1. Select the **Storage** tab

1. Filter on the **mslearn** database.

    ![Screenshot that shows the Storage tab's database filter. ](../media/6-metrics-storage-database-filter.png)

### <a name="review-unevenly-distributed-partitions-for-storage"></a>Review unevenly distributed partitions for storage

1. Filter on the **Hot Partition** collection.

1. Review the **Data + Index storage consumed per partition key range** chart. You see the uneven distribution of data among the partitions. When you have uneven storage, one partition is going to receive more requests than others.

    ![Cosmos DB uneven partition storage chart](../media/6-hot-partition-storage.png)

1. Select the blue column for the largest partition. The dominant partition key values are shown to the right of the chart. In this case, the **Books** category is dominant.

### <a name="review-evenly-distributed-partitions-for-storage"></a>Review evenly distributed partitions for storage

1. Filter on the **Orders** database.

1. Review the **Data + Index storage consumed per partition key range** chart.

    ![Cosmos DB balanced partition storage chart](../media/6-balanced-partition-storage.png)

    You see that the storage across partitions is balanced. There's no significant consumption by any partition key value.
