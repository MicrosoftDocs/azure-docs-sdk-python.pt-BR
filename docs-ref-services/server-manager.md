---
title: Bibliotecas do Gerenciador do Servidor do Azure para Python
description: "Referência para bibliotecas do Gerenciador do Servidor do Azure para Python"
keywords: Azure, Python, SDK, API, Gerenciador do Servidor
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 480513a76683c97fdac8d2a65b38fde0fffb6dcd
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-server-manager-libraries-for-python"></a>Bibliotecas do Gerenciador do Servidor do Azure para Python

## <a name="management-apipythonapioverviewazureservermanagermanagement"></a>[API de Gerenciamento](/python/api/overview/azure/servermanager/management)

```bash
pip install azure-mgmt-servermanager
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de sua [lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

```python
from azure.mgmt.servermanager import ServerManagement
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

servermanager_client = ServerManagement(
    credentials,
    subscription_id
)
``` 

## <a name="create-gateway"></a>Criar gateway
```python
gateway_async = servermanager_client.gateway.create(
    'MyResourceGroup',
    'MyGateway',
    'centralus'
)
gateway = gateway_async.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/servermanager/management)