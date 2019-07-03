---
title: Bibliotecas do Azure DevTest Labs para Python
description: Referência para bibliotecas do Azure DevTest Labs para Python
keywords: Azure, Python, SDK, API, DevTest Labs
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f232a24dfba610b3fdf505b63788aecc7b8fa9f9
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534280"
---
# <a name="azure-devtest-labs-libraries-for-python"></a><span data-ttu-id="e4c42-104">Bibliotecas do Azure DevTest Labs para Python</span><span class="sxs-lookup"><span data-stu-id="e4c42-104">Azure DevTest Labs libraries for python</span></span>

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[<span data-ttu-id="e4c42-105">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e4c42-105">Management API</span></span>](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a><span data-ttu-id="e4c42-106">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e4c42-106">Create the management client</span></span>

<span data-ttu-id="e4c42-107">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="e4c42-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="e4c42-108">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="e4c42-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="e4c42-109">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="e4c42-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

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

## <a name="create-lab"></a><span data-ttu-id="e4c42-110">Criar Laboratório</span><span class="sxs-lookup"><span data-stu-id="e4c42-110">Create lab</span></span>

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4c42-111">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e4c42-111">Explore the Management APIs</span></span>](/python/api/overview/azure/devtestlabs/management)
