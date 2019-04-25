---
ms.openlocfilehash: 8bedd1f75955fc4d36e1a96a6b28c9e3c3b08977
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Let's say you're a systems administrator at a growing financial services company. Analysts create financial models to help recommend the best investment options to investors.

These financial models are run on virtual machines running on Azure. A model can take between a few minutes and several hours to run. You typically create a new virtual machine to run each new model, then delete it after the analyst collects the results.

The financial services business moves quickly. You find yourself constantly deploying and deleting cloud resources. You initially created resources through the Azure portal, and now you use the Azure CLI and scripts to further automate things. Although you see certain patterns among your deployments, it still takes time to connect virtual machines to networking and storage components. At the end of each run, you need to delete only the components related to that run.

How can you keep up with the pace of your analysts? Azure Resource Manager templates are one way to further automate your deployments.

## <a name="learning-objectives"></a>Learning objectives

In this module, you will:

- Identify what Azure Resource Manager is, and what's in a Resource Manager template
- Deploy a VM using the Azure CLI and a prebuilt Resource Manager template
- Customize your Resource Manager template to configure a basic web server on your VM

## <a name="prerequisites"></a>Prerequisites

- Experience using Bash and the Azure CLI
- Experience working with Azure resources and resource groups