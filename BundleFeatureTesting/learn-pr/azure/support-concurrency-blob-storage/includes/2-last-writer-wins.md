---
ms.openlocfilehash: 5c84ea49dba0c8efd0f5b68e13c5d722b4c90e9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Cloud-based storage gives organizations the flexibility to work on files globally. Using economies of scale, large amounts of storage is available at a fraction of the cost of traditional storage. Companies have to handle files being accessed concurrently when writing applications that use it.

Your company's authoring app stores data in Blob Storage. The app was written when there was only one or two reporters in the team. The newsroom has dramatically increased in size, and there are now issues with work being overwritten and lost.

Here, you'll learn about the issues you can face with concurrency when using Blob storage.

## <a name="last-writer-wins"></a>Last writer wins

![text](../media/last-writer-wins.png)

Last writer wins is the name given to the approach when no consideration has been given to concurrency. As the name implies, whoever makes changes most recently overwrites previous changes. The results of operations are unpredictable and can lead to data loss. When the last writer wins, there's no control over who reads or writes data. The last person to save their changes to a file has them reflected in that data. Anything that has happened to the storage before is overwritten. For example, a user may start editing a document, while editing, a second user edits the same document and commits their changes. Then the first user saves their changes. Because they're starting from a copy of the document without the 2nd user's changes, those edits are overritten and lost.

Even though there can be data lost, last writer wins can be a valid strategy in situations where having the latest data is most important. Previous versions of the data have little to no value. A stock market ticker is a good example, as the ticker app just needs to show the most recent values for a stock.

## <a name="blob-storage-concurrency"></a>Blob Storage Concurrency

Multiple users accessing data at the same time will liekly cause concurrency issues when using Azure blob storage. To solve these problems, Blob storage supports two different approaches to resolving concurrency. An app can choose to resolve concurrency *optimistically*, or *pessimistically*. We'll explain these terms later in the module.