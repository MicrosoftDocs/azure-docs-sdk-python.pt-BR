---
title: Bibliotecas de Hubs de Notificação do Azure para Python
description: Referência para bibliotecas de Hubs de Notificação do Azure para Python
keywords: Azure, Python, SDK, API, Hubs de Notificação
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f600b28c347cdbffc16342da25a72e4de8e83c5f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534241"
---
# <a name="azure-notification-hubs-libraries-for-python"></a>Bibliotecas de Hubs de Notificação do Azure para Python

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

```python
from azure.mgmt.notificationhubs import NotificationHubsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

redis_client = NotificationHubsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-namespace-availability"></a>Verificar a disponibilidade do namespace

O seguinte código verifica a disponibilidade do namespace de um hub de notificação.

```python
from azure.mgmt.notificationhubs.models import CheckAvailabilityParameters

account_name = 'mynotificationhub'
output = notificationhubs_client.namespaces.check_availability(
    azure.mgmt.notificationhubs.models.CheckAvailabilityParameters(
        name = account_name
    )
)
# output is a CheckAvailibilityResource instance
print(output.is_availiable) # Yes, it's 'availiable', it's a typo in the REST API
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/notificationhubs/management)
