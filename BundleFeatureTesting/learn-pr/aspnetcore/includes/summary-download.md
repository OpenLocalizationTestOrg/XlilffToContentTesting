---
ms.openlocfilehash: 14eb2858fff61cf8905f399302a257aef76acfbc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
## <a name="download-project-files"></a>Download project files

Use the following command to package and download your project files:

```bash
pushd ~/contoso-pets/src && \
    zip -r ~/contoso-pets.zip . && \
    popd && \
    download ~/contoso-pets.zip
```