---
ms.openlocfilehash: d0c22eca5453ccac3e412d6e1bfb49d185ce30cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Like most application frameworks, you can run your MEAN stack application in many different environments. You can run your application on a physical computer in your server room, on a virtual machine, or in containers.

Here you'll run your application on a VM running on Azure. MEAN supports many different operating systems. For learning purposes, here you'll use Ubuntu Linux.

## <a name="create-an-ubuntu-linux-vm"></a>Create an Ubuntu Linux VM

[!include[](../../../includes/azure-sandbox-activate.md)]

Normally, you create a _resource group_ before you create other resources on Azure. A resource group is a container that holds the resources that are related for an Azure solution. For this exercise, the Azure sandbox provides a resource group for you. However, when you are working in your own Azure subscription, you would use the following command to create a resource group in a location near you.

```azurecli
az group create \
  --name <resource-group-name> \
  --location <resource-group-location>
```

1. From Cloud Shell, run the `az vm create` command to create an Ubuntu VM.

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack \
      --image Canonical:UbuntuServer:16.04-LTS:latest \
      --admin-username azureuser \
      --generate-ssh-keys
    ```

    The command takes about two minutes to complete. When the command finishes, you'll see output similar to this.

    ```json
    {
      "fqdns": "",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/MeanStack",
      "location": "eastus",
      "macAddress": "00-0D-3A-1E-1B-3B",
      "powerState": "VM running",
      "privateIpAddress": "10.0.0.5",
      "publicIpAddress": "104.211.9.245",
      "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
      "zones": ""
    }
    ```

    The VM's name is "MeanStack". You'll use this name in future commands to identify the VM you want to work with.

1. Open port 80 on the VM to allow incoming HTTP traffic to the web application you'll later create.

    ```azurecli
    az vm open-port \
      --port 80 \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name MeanStack
    ```

1. Create an SSH connection to your VM.

    Although the output from the `az vm create` command displays your VM's public IP address, you may find it useful to store the address in a Bash variable.

    Start by running `az vm show`. This command saves the IP address in a Bash variable named `ipaddress`.

    ```azurecli
    ipaddress=$(az vm show \
      --name MeanStack \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --show-details \
      --query [publicIps] \
      --output tsv)
    ```

    Connect to your VM like this.

    ```bash
    ssh azureuser@$ipaddress
    ```

    When prompted, answer "yes" to save the VM's identity locally so future connections are trusted.

    Keep your SSH connection open. You'll use it to configure software in the next parts.

## <a name="summary"></a>Summary

With your Ubuntu VM ready to go, you're ready to install each component of the MEAN stack. You'll start by installing MongoDB.
