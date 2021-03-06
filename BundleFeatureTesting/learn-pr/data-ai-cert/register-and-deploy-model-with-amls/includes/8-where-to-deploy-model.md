---
ms.openlocfilehash: 58a4551d054c19ac55d387910060f8858214e127
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
Once a model has been trained and you are ready to make it available to your applications and services, you need to deploy it. Deploying a model allows it to receive data from a client, process the data with the trained model, and return results back to the client.

The Azure Machine Learning Service provides several places you can deploy your trained model using the Azure Machine Learning SDK, including:

| Location | Type | Description |
|----------|------|-------------|
| [Azure Container Instances (ACI)](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where#aci) | Testing | This is a single container instance managed by Azure Container Instances service. It has fast deployment speed (usually less than 5 minutes) and is an ideal environment for development and testing purpose. |
| [Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where#aks) | Real-time interface | This is a set of containers managed by Azure Kubernetes Service. It provides high-scale production deployments, auto-scale, and a front end to handle ingress and egress requests. It usually takes around 20 minutes to set up, but this is a one-time setup and is ideal for production purpose deployment. |
| [Azure Machine Learning Compute](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where#azuremlcompute) | Batch interface | Run batch prediction on serverless compute. Supports normal and low-priority VMs created and managed by the Azure Machine Learning service. |
| [Azure IoT Edge](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where#iotedge) | IoT module (Preview) | An Azure IoT Edge device is a Linux or Windows-based device that runs the Azure IoT Edge runtime. Azure Machine Learning supports deploying machine learning models to IoT Edge devices as IoT Edge modules. Once the model is deployed to IoT Edge devices, the model can be used in the edge device directly without connect to the cloud, which reduces the data transfer amount and reduces the response time. |
| [Field-programmable gate array (FPGA)](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where#fpga) | Web service (Preview) | FPGAs contain an array of programmable logic blocks, and a hierarchy of reconfigurable interconnects. Compared to CPU and GPUs, FPGAs provide a combination of programmability and performance. The hardware can be programmed so that it can provide model inference with hardware (which is usually much faster than software), and the hardware updates to a different set of models, which provides flexibility. Azure Machine Learning supports deploying models to use FPGAs on Azure. |
