---
ms.openlocfilehash: e0ddb24bc0c561b0f4ec6c5e26e399c547ae7c27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
You work at a company that tracks professional sports statistics and provides an API to query results. It helps fans track and review games and scores, both live and historical. Users can also request team statistics using a natural language search, such as, "How many times has John Smith hit a home run against a left-handed pitcher?"

During times of peak demand, such as during playoffs, response time of your service slows down because the back-end service doesn't have the capacity to meet demand. You want to improve performance for your users and reduce the workload on your back-end and data storage services. Your metrics show that 50% to 80% of the data returned is for read-only or recently requested values. Implementing a cache of commonly used data could improve performance and reduce latency.

## <a name="learning-objectives"></a>Learning objectives

In this module, you will:

- Describe what a Redis cache is and how you can use it for your business needs
- Create a design and plan to use a Redis cache
- Provision a Redis cache in Azure
- Connect an application to the cache

## <a name="prerequisites"></a>Prerequisites

- Experience with app development
- Experience using data in apps