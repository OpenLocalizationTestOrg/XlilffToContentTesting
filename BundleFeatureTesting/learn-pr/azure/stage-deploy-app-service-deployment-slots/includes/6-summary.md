---
ms.openlocfilehash: 748ba7b3fadb68294540702feb0e6a0de426c8a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
In this module, you learned how to use deployment slots in Azure App Service. You used slots to test and stage new versions of your app, and you swapped those deployment slots. You can swap slots both to deploy a tested app to production and to roll back a deployed app when unexpected problems arise.

When you consider using deployment slots, remember that Azure warms up an app before a swap, and traffic redirection is instantaneous. The result is that your app is deployed without service interruptions or performance drops.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="learn-more"></a>Learn more

- [Set up staging environments in App Service](https://docs.microsoft.com/azure/app-service/deploy-staging-slots).
- [Learn about Azure subscriptions, service limits, quotas, and constraints](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- [Find out more about App Service static IP restrictions](https://docs.microsoft.com/azure/app-service/app-service-ip-restrictions).