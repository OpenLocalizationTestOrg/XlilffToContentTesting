---
ms.openlocfilehash: 6ee62a804e9b2395648cf896ba3f8be376392786
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In this module, you learned how to create an Azure Stream Analytics job, set up an input, write a transformation query, and set up an output. You used Azure Storage as your source and destination, and you created a transformation query to produce some basic results. You also learned how to start a Stream Analytics job and view the job results.

## <a name="clean-up"></a>Clean up

To avoid unnecessary charges, you'll want to delete all the resources you created for this module. That includes the two storage accounts and the Stream Analytics job. You can delete these accounts individually, but it's easier to delete the resource group **mslearn-streamanalytics**: 

1. Use the search field to find the resource group. 
1. Select the group, and then select **Delete resource group**. 

    ![Screenshot showing how to delete the resource group in the Azure portal](../media/10-cleanup.png)

Because you're deleting a whole set of resources together, Azure prompts you to confirm that you want to do this.

## <a name="learn-more"></a>Learn more

To learn more about creating Stream Analytics jobs and queries, use these resources:

* [Supported output sinks for Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-define-outputs)
* [Stream Analytics query language](https://docs.microsoft.com/stream-analytics-query/stream-analytics-query-language-reference)