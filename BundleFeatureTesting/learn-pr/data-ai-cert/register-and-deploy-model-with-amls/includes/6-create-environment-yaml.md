---
ms.openlocfilehash: 2ecb12501676c7f77ea4c48a744c024fc3a9f73d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
The second step is to make sure the dependencies are included in the image. Azure Machine Learning does that by creating a conda dependency file:

```python
from azureml.core.conda_dependencies import CondaDependencies 
myenv = CondaDependencies.create(conda_packages=['numpy','scikit-learn'])
with open("myenv.yml","w") as f:
    f.write(myenv.serialize_to_string())
```