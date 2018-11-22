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
# <a name="azure-iot-hub-libraries-for-python"></a>Bibliotecas do Hub IoT do Azure para Python

## <a name="management-apipythonapioverviewazureiotmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/iot/management)

```bash
pip install azure-mgmt-iothub
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

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

## <a name="create-an-iothub"></a>Criar um Hub IoT
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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/iot/management)