---
title: Bibliotecas de Hubs de Notificação do Azure para Python
description: Referência para bibliotecas de Hubs de Notificação do Azure para Python
keywords: Azure, Python, SDK, API, Hubs de Notificação
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3a9cc087d315ee2a274d3ef00623b304280017e5
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277238"
---
# <a name="azure-notification-hubs-libraries-for-python"></a><span data-ttu-id="0f804-104">Bibliotecas de Hubs de Notificação do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="0f804-104">Azure Notification Hubs libraries for python</span></span>

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[<span data-ttu-id="0f804-105">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f804-105">Management API</span></span>](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a><span data-ttu-id="0f804-106">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f804-106">Create the management client</span></span>

<span data-ttu-id="0f804-107">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0f804-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="0f804-108">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="0f804-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="0f804-109">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="0f804-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

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

## <a name="check-namespace-availability"></a><span data-ttu-id="0f804-110">Verificar a disponibilidade do namespace</span><span class="sxs-lookup"><span data-stu-id="0f804-110">Check namespace availability</span></span>

<span data-ttu-id="0f804-111">O seguinte código verifica a disponibilidade do namespace de um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="0f804-111">The following code check namespace availability of a notification hub.</span></span>
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
> [<span data-ttu-id="0f804-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f804-112">Explore the Management APIs</span></span>](/python/api/overview/azure/notificationhubs/management)
