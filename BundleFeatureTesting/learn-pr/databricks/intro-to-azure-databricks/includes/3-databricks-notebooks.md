---
ms.openlocfilehash: 67e8a8278c48ca26413e8f727da7685cda43c959
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---

After creating your Databricks workspace, it's time to create your first notebook and Spark cluster.

## <a name="what-is-apache-spark-notebook"></a>What is Apache Spark notebook?

A notebook is a collection of cells. These cells are run to execute code, to render formatted text, or to display graphical visualizations.

## <a name="what-is-a-cluster"></a>What is a cluster?

The notebooks are backed by clusters, or networked computers, that work together to process your data. The first step is to create a cluster.

## <a name="create-a-cluster"></a>Create a cluster

1. In the left-hand menu of your Databricks workspace, select **Clusters**.
1. Select **Create Cluster** to add a new cluster.

    ![The create cluster page](../media/create-a-cluster.png)

1. Enter a name for your cluster. Use your name or initials to easily differentiate your cluster from your coworkers.
1. Select the **Databricks RuntimeVersion**. We recommend the latest runtime (4.0 or newer) and **Scala 2.11**.
1. Specify your cluster configuration.
    - For clusters that are created on a Community Edition, the default values are sufficient for the remaining fields.
    - For all other environments, refer to your company's policy on creating and using clusters.
1. Select **Create Cluster**.

> [!NOTE]
> Check with your local system administrator to see if there is a recommended default cluster at your company to use for the rest of the class. Making new cluster will incur costs.

## <a name="create-a-notebook"></a>Create a notebook

1. On the left-hand menu of your Databricks workspace, select **Home**.
1. Right-click on your home folder.
1. Select **Create**.
1. Select **Notebook**.

    ![The menu option to create a new notebook](../media/creating-a-notebook.png)

1. Name your notebook **First Notebook**.
1. Set the **Language** to **Python**.
1. Select the cluster to which to attach this notebook.

     > [!NOTE]
     > This option displays only when a cluster is currently running. You can still create your notebook and attach it to a cluster later.

1. Select **Create**.

Now that you've created your notebook, let's use it to run some code.

## <a name="attach-and-detach-your-notebook"></a>Attach and detach your notebook

To use your notebook to run a code, you must attach it to a cluster. You can also detach your notebook from a cluster and attach it to another depending upon your organization's requirements.

![The options that are available when a notebook is attached to a cluster](../media/attach-detach-cluster.png)

If your notebook is attached to a cluster, you can:

- Detach your notebook from the cluster
- Restart the cluster
- Attach to another cluster
- Open the Spark UI
- View the log files of the driver
