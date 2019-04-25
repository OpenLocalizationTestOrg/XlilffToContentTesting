---
ms.openlocfilehash: 9f7c43e37647c39bcb9d619127a3a879c655b3d1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Since the model is deployed as a web service that exposes a REST API, it can be tested with many tools. Azure Machine Learning SDK has a built-in testing tool that can work with the deployed web service, like below:

```python
import json
test_sample = json.dumps({'data': [
    [1,2,3,4,5,6,7,8,9,10], 
    [10,9,8,7,6,5,4,3,2,1]
]})
test_sample = bytes(test_sample,encoding = 'utf8')
prediction = service.run(input_data = test_sample)
print(prediction)
```

The key part of the code is the `service.run` call, which sends a JSON formatted document to the deployed web service and the result is displayed.