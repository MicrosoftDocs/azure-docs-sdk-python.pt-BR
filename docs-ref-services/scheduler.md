---
title: Bibliotecas do Agendador do Azure para Python
description: "Referência para bibliotecas do Agendador do Azure para Python"
keywords: Azure, Python, SDK, API, Agendador
author: lisawong19
ms.author: liwong
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3d2691ae1ba84c41f25de2b099aacefaa92152ed
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/24/2018
---
# <a name="azure-scheduler-libraries-for-python"></a><span data-ttu-id="95b8f-104">Bibliotecas do Agendador do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="95b8f-104">Azure Scheduler libraries for python</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="95b8f-105">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="95b8f-105">Install the libraries</span></span>

## <a name="management"></a><span data-ttu-id="95b8f-106">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="95b8f-106">Management</span></span>

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a><span data-ttu-id="95b8f-107">Exemplo</span><span class="sxs-lookup"><span data-stu-id="95b8f-107">Example</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="95b8f-108">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="95b8f-108">Create the management client</span></span>

<span data-ttu-id="95b8f-109">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="95b8f-109">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="95b8f-110">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="95b8f-110">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="95b8f-111">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="95b8f-111">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a><span data-ttu-id="95b8f-112">Criar uma coleção de trabalhos</span><span class="sxs-lookup"><span data-stu-id="95b8f-112">Create a job collection</span></span>

<span data-ttu-id="95b8f-113">O código a seguir cria uma coleção de trabalho em um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="95b8f-113">The following code creates a job collection under an existing resource group.</span></span>
<span data-ttu-id="95b8f-114">Para criar ou gerenciar grupos de recursos, consulte [Gerenciamento de recursos](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="95b8f-114">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="95b8f-115">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="95b8f-115">Explore the Management APIs</span></span>](/python/api/overview/azure/scheduler/management)