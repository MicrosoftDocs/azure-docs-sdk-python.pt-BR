---
title: Bibliotecas do Azure DevTest Labs para Python
description: Referência para bibliotecas do Azure DevTest Labs para Python
keywords: Azure, Python, SDK, API, DevTest Labs
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3da9210dd14c19d591539656fb7229f4d3346ea9
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376887"
---
# <a name="azure-devtest-labs-libraries-for-python"></a>Bibliotecas do Azure DevTest Labs para Python

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

```python
from azure.mgmt.devtestlabs import DevTestLabsClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

devtestlabs_client = DevTestLabsClient(
    credentials,
    subscription_id
)
```

## <a name="create-lab"></a>Criar Laboratório

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/devtestlabs/management)
