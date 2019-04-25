---
ms.openlocfilehash: 286830831644536ea0bbb8380299bf3eb9fd1573
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
When you have a successful or business-critical web app, you need to update it to respond to business changes, user demands, or security issues. But you can't allow service interruptions.

Suppose you work for a company that runs a popular social media web platform. The user interface for this platform is set up as an ASP.NET Core MVC web app that's hosted in Azure App Service. You regularly update the app's source code and roll out the updates to production. These updates occasionally cause problems when testers fail to catch bugs. Also, service is briefly interrupted when you roll out an update, and then responsiveness is slow while the code is deployed and compiled.

You want a way to deploy a new version of the app without downtime or a service interruption. You also want to be able to rapidly roll back a new deployment to the previous version if it causes problems.

## <a name="learning-objectives"></a>Learning objectives

In this module, you will:

- Create a deployment slot as a staging environment in App Service.
- Use git to deploy a new version of a web app to a slot.
- Configure which app settings are swapped and which are not swapped when you deploy a slot.
- Swap slots to deploy a web app or roll back a deployment.

## <a name="prerequisites"></a>Prerequisites

- Basic experience deploying apps to App Service