---
ms.openlocfilehash: a049261d43500b0b10e0babbfe6228814d70d955
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In this module, you learned how to use the Azure portal to build and run a performance test for your web apps. You examined the results and used the information to help you configure and customize tests in Azure DevOps. 

Using the Azure portal for initial testing and the Azure DevOps Portal for more detailed and configurable testing is a powerful combination for identifying potential performance issues. It will help you create high-performing web apps to provide better experiences for your users.

## <a name="cleanup"></a>Cleanup

Run this command to remove the resource group, app service, storage account, and all related resources.

```azurecli
az group delete --resource-group ContosoRentalsRG
```