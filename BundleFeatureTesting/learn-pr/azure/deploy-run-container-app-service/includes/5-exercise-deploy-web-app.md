---
ms.openlocfilehash: 324c0d7ec938de85eabc38ca7e35e1c4235caf6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Azure App Service provides the hosting environment for an Azure-based web app. You can configure App Service to retrieve the image for the web app from a repository in Azure Container Registry. 

In the example scenario, the team has uploaded the image for the web app to Azure Container Registry and is now ready to deploy the web app.

In this unit, you'll create a new web app by using the Docker image stored in Azure Container Registry. You'll use App Service with a predefined App Service plan to host the web app.

## <a name="create-a-web-app"></a>Create a web app

1. Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true).

1. Select **Create a resource** > **Web** > **Web App**.

    ![Screenshot that shows the Azure Marketplace with Web App selected](../media/5-search-web-app-annotated.png)

1. Specify these settings:

    | Property         | Value                                                                |
    |------------------|----------------------------------------------------------------------|
    | Name             | Enter a unique name and make a note of it for later.                 |
    | Subscription     | **Concierge Subscription**                                           |
    | Resource Group   | Use the existing resource group <rgn>[Sandbox resource group]</rgn>. |
    | OS               | **Linux**                                                            |
    | Publish          | **Docker Image**                                                     |
    | App Service plan | Use the default.                                                     |

1. Select **Configure container**.

1. In the **Configure Container** window, select the **Single Container** tab. For the image source, select **Azure Container Registry**, and then enter these settings:

    | Property     | Value                 |
    |--------------|-----------------------|
    | Registry     | Select your registry. |
    | Image        | `webimage`          |
    | Tag          | `latest`            |
    | Startup File | Leave this empty.     |

1. Select **Apply**, and then on the **Web App** page, select **Create**. Wait until the web app has been deployed before you continue.

## <a name="test-the-web-app"></a>Test the web app

1. Use the **All resources** view in the Azure portal to go to the Overview page of the web app you just created. Select the **Browse** button to open the site in a new browser tab.

1. After the cold-start delay while your app's Docker image loads and starts, you'll see a page like this:

    ![Screenshot of the sample web app](../media/5-sample-web-app.png)

1. Select the arrows in the carousel control at the top of the page to rotate through three pages of content.

App Service is now hosting the app from your Docker image.