---
ms.openlocfilehash: d85b30186c7cb9d58c90e455d1df7649f97610d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
## <a name="get-an-access-key"></a>Get an access key

If you haven't done so already, run the following command in Azure Cloud Shell to store the API access key in a variable called `key`. We'll use this variable in subsequent calls.

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--query key1 -o tsv)
```
