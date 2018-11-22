---
title: Bibliotecas do Hub IoT do Azure para Python
description: Referência para bibliotecas do Hub IoT do Azure para Python
keywords: Azure, Python, SDK, API, Hub IoT
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 0864c83eba43f97a606ae817f1a0ec2dd1ea787a
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52279239"
---
# <a name="azure-iot-hub-libraries-for-python"></a><span data-ttu-id="6c739-104">Bibliotecas do Hub IoT do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="6c739-104">Azure IoT Hub libraries for python</span></span>

## <a name="management-apipythonapioverviewazureiotmanagement"></a>[<span data-ttu-id="6c739-105">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6c739-105">Management API</span></span>](/python/api/overview/azure/iot/management)

```bash
pip install azure-mgmt-iothub
```

## <a name="create-the-management-client"></a><span data-ttu-id="6c739-106">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6c739-106">Create the management client</span></span>

<span data-ttu-id="6c739-107">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6c739-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="6c739-108">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="6c739-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="6c739-109">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="6c739-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.iothub import IotHubClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

iothub_client = IotHubClient(
    credentials,
    subscription_id
)
```

## <a name="create-an-iothub"></a><span data-ttu-id="6c739-110">Criar um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="6c739-110">Create an IoTHub</span></span>
```python
async_iot_hub = iothub_client.iot_hub_resource.create_or_update(
    'MyResourceGroup',
    'MyIoTHubAccount',
    {
        'location': 'westus',
        'subscriptionid': subscription_id,
        'resourcegroup': 'MyResourceGroup',
        'sku': {
            'name': 'S1',
            'capacity': 2
        },
        'properties': {
            'enable_file_upload_notifications': False,
            'operations_monitoring_properties': {
            'events': {
                "C2DCommands": "Error",
                "DeviceTelemetry": "Error",
                "DeviceIdentityOperations": "Error",
                "Connections": "Information"
            }
            },
            "features": "None",
        }
    }
)
iothub = async_iot_hub.result() # Blocking wait for creation
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c739-111">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6c739-111">Explore the Management APIs</span></span>](/python/api/overview/azure/iot/management)