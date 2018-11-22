---
title: Bibliotecas de Autorização do Azure para Python
description: Referência para bibliotecas de Autorização do Azure para Python
keywords: Azure, Python, SDK, API, Autorização
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 8709bbd3cff448c7beb394621b163a4b3e3c3cd8
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276760"
---
# <a name="azure-authorization-libraries-for-python"></a>Bibliotecas de Autorização do Azure para Python

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a>Verificar as permissões de um grupo de recursos

O código a seguir verifica as permissões em um determinado grupo de recursos.
Para criar ou gerenciar grupos de recursos, consulte [Gerenciamento de recursos](/python/api/overview/azure/azure.mgmt.resource).

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/authorization/management)

