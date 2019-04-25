---
ms.openlocfilehash: 12e6fa7f2ef102aa854003eca8339c7516e6e387
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Databricks provides several built-in functions for presenting your data. It also integrates with data-visualization tools such as Power BI so that you can display your data in an easy to understand format.

## <a name="built-in-functions"></a>Built-in functions

Databricks provides the built-in `display` function for visualizations of your data. You can use this function directly with DataFrames and create the required results by using the `filter` and `select` expressions.

## <a name="visualize-data-with-power-bi"></a>Visualize data with Power BI

You can connect your Databricks cluster to Power BI to create visualizations for your data. After you've established a connection, you can use the Power BI application to pull your analysis data from your cluster and create reports in the required format.

## <a name="visualize-data-with-matplotlib"></a>Visualize data with Matplotlib

To expand your options for creating useful visualizations, Databricks supports the third-party Matplotlib library. You can display Matplotlib objects within a Python notebook in Databricks. Databricks saves plots as images in the FileStore. You can display the results as box plots or heat maps. Matplotlib also allows you to present your data in a grouped bar chart and provides many options for customizing the color and even the texture of chart elements.