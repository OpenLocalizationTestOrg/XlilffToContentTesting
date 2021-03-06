---
ms.openlocfilehash: 4f1ab11ae07182018f05cb5327a626858bc1a5ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Now that we have an image that contains our trained model, we can use Azure Container Instances to deploy the trained model as a web service. There are two steps involved:

1. Define the deployment configuration. For example, the following code defines a container that uses 1 CPU and 1 GB of memory:

```python
from azureml.core.webservice import AciWebservice
aciconfig = AciWebservice.deploy_configuration(cpu_cores = 1, 
                                          memory_gb = 1, 
                                          tags = {"data": "mnist", "type": "classification"}, 
                                           description = 'Handwriting recognition')
```

1. To deploy the image created in the previous unit, you can use code similar to the code below:

```python
from azureml.core.webservice import Webservice
service_name = 'aci-mnist-13'
service = Webservice.deploy_from_image(deployment_config = aciconfig,
                                            image = image,
                                            name = service_name,
                                            workspace = ws)
service.wait_for_deployment(show_output = True)
```

It takes around 3-4 minutes for the web service to deploy. Once it's deployed, we can call it from a client application.