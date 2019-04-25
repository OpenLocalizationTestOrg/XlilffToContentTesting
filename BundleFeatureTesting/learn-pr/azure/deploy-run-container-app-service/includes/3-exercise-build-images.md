---
ms.openlocfilehash: e45ff592e4a71d512d03613ef9621efe5b1d2517
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Azure Container Registry provides storage for Docker images in the cloud.

In the example scenario, the team needs to create a registry to store the images for their web apps.

In this unit, you'll use the Azure portal to create a new registry in Azure Container Registry. You'll build a Docker image from the source code for a web app and upload it to a repository in your registry. Finally, you'll examine the contents of the registry and the repository.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-registry-in-azure-container-registry"></a>Create a registry in Azure Container Registry

1. Sign in to the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) by using your Microsoft Learn account.

1. Choose **Create a resource**, select **Containers**, and then select **Container Registry**.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    ![Screenshot that shows the New blade in Azure portal showing the Container options available in Azure Marketplace](../media/3-search-container-registry-annotated.png)

1. Specify the values in the following table for each of the properties, and then select **Create**:

    | Property       | Value                                                                |
    |----------------|----------------------------------------------------------------------|
    | Name           | Enter a unique name and make a note of it for later.                 |
    | Subscription   | **Concierge Subscription**                                           |
    | Resource Group | Use the existing resource group <rgn>[Sandbox resource group]</rgn>. |
    | Location       | Use the default location.                                            |
    | Admin user     | **Enable**                                                           |
    | SKU            | **Standard**                                                         |

1. Wait until the container registry has been created before you continue.

## <a name="build-a-docker-image-and-upload-it-to-azure-container-registry"></a>Build a Docker image and upload it to Azure Container Registry

1. In the Azure Cloud Shell window on the right, run the following command to download the source code for the sample web app. This web app is simple. It presents a single page that contains static text and a carousel control that rotates through a series of images.

    ```bash
    git clone https://github.com/MicrosoftDocs/mslearn-deploy-run-container-app-service.git
    ```

1. Move to the source folder:

    ```bash
    cd mslearn-deploy-run-container-app-service
    ```

1. Run the following command. This command sends the folder's contents to Azure Container Registry, which uses the instructions in the Docker file to build the image and store it. Replace `<container_registry_name>` with the name of the registry you created earlier. Take care not to leave out the `.` character at the end of the command.

    ```bash
    az acr build --registry <container_registry_name> --image webimage .
    ```

    The Docker file contains the step-by-step instructions for building a Docker image from the source code for the web app. Azure Container Registry runs these steps. The build process generates several messages as it proceeds. It should finish after a couple of minutes without any errors or warnings.

## <a name="examine-the-container-registry"></a>Examine the container registry

1. Switch back to [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) and navigate to the Overview page for your container registry.

2. Under **Services**, select **Repositories**. You'll see a repository named `webimage`.

3. Select the `webimage` repository. It contains an image with the `latest` tag. This is the Docker image for the sample web app.

    ![Screenshot that shows the repositories and images uploaded to Azure Container Registry](../media/3-azure-container-repositories.png)

 The Docker image that contains your web app is now available in your registry for deployment to App Service.