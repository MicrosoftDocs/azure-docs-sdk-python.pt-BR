---
title: Bibliotecas de DNS do Azure para Python
description: Referência para bibliotecas de DNS do Azure para Python
keywords: Azure, Python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 294373469b1792821253ae46ab51fa0c06a74ffa
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551559"
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="cd9b3-104">Bibliotecas de DNS do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="cd9b3-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="cd9b3-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cd9b3-105">Overview</span></span>

<span data-ttu-id="cd9b3-106">O [DNS do Azure](/azure/dns/dns-overview) é um serviço de hospedagem para domínios DNS que fornece resolução de DNS usando a infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd9b3-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="cd9b3-107">Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando o portal do Azure](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="cd9b3-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[<span data-ttu-id="cd9b3-108">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cd9b3-108">Management API</span></span>](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a><span data-ttu-id="cd9b3-109">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cd9b3-109">Create the management client</span></span>

<span data-ttu-id="cd9b3-110">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="cd9b3-110">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="cd9b3-111">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="cd9b3-111">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="cd9b3-112">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="cd9b3-112">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python 
from azure.mgmt.dns import DnsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

dns_client = DnsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="create-dns-zone"></a><span data-ttu-id="cd9b3-113">Criar zona DNS</span><span class="sxs-lookup"><span data-stu-id="cd9b3-113">Create DNS zone</span></span>
```python
# The only valid value is 'global', otherwise you will get a:
# The subscription is not registered for the resource type 'dnszones' in the location 'westus'.
zone = dns_client.zones.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    {
        'location': 'global'
    }
)
```
    
## <a name="create-a-record-set"></a><span data-ttu-id="cd9b3-114">Criar um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="cd9b3-114">Create a Record Set</span></span>
```python
record_set = dns_client.record_sets.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    'MyRecordSet',
    'A',
    {
            "ttl": 300,
            "arecords": [
                {
                "ipv4_address": "1.2.3.4"
                },
                {
                "ipv4_address": "1.2.3.5"
                }
            ]
    }
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd9b3-115">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="cd9b3-115">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/management)
