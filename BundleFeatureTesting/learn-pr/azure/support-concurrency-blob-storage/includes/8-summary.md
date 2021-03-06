---
ms.openlocfilehash: 854e0c84ac141677d225c966cbf27403729aeee6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In this module you've learned about three different concurrency strategies to address issues with multiple people trying to update data in blob storage:

1. Last writer wins
1. Optimistic with ETags
1. Pessimistic with leases

Both optimistic and pessimistic approaches to concurrency are declared in the code used to update content in Blob storage. If concurrency isn't addressed the last person to write to the file wins.

In this lesson, we've gone over code examples for each of the three approaches.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>Additional resources

The documentation provides more information on the APIs as well as tutorials and samples. Here are a few useful links to explore further:

- [Managing Concurrency in Microsoft Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-concurrency)
- [Specifying Conditional Headers for Blob Service Operations](https://docs.microsoft.com/rest/api/storageservices/specifying-conditional-headers-for-blob-service-operations)
- [Lease Blob](https://docs.microsoft.com/rest/api/storageservices/lease-blob)