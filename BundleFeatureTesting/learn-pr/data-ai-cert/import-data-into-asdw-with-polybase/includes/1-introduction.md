---
ms.openlocfilehash: 2a91107ed1899e6d03985913e24e20fbbf1d044e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
One of the key benefits of using Azure SQL Data Warehouse is the fast loading of data. Importing data is a manual process that requires an understanding of PolyBase and the necessary steps to transfer data. After you understand this process, loading terabytes or petabytes of data can take minutes instead of hours.

Suppose you want to resolve a long-running data load that's delaying the daily population of an on-premises data warehouse within Contoso. You decide that the best approach to solve this problem is to create a data warehouse and use PolyBase to perform data loads. Your goal is to explore and understand the steps required so that you can explain them to the rest of the data team at Contoso.

## <a name="learning-objectives"></a>Learning objectives

In this module, you:

- Explore how PolyBase works.
- Upload text data to Azure Blob storage.
- Collect the security keys for Azure Blob storage.
- Create a data warehouse.
- Import data from Blob storage to the data warehouse.
