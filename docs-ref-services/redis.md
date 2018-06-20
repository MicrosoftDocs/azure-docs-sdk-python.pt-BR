---
title: Bibliotecas de Redis do Azure para Python
description: Documentação de referência para as bibliotecas de cliente de Python para Redis
keywords: Azure, Python, Redis, API, SDK, banco de dados, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: c2f8ebcbcbd7b71c1fa96e46a8148a3c0b88877f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479239"
---
# <a name="azure-redis-cache-libraries-for-python"></a><span data-ttu-id="06205-104">Bibliotecas do Cache Redis do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="06205-104">Azure Redis Cache libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="06205-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="06205-105">Overview</span></span>

<span data-ttu-id="06205-106">O Cache Redis do Azure se baseia no popular projeto Redis de software livre.</span><span class="sxs-lookup"><span data-stu-id="06205-106">Azure Redis Cache is based on the popular open source Redis project.</span></span> <span data-ttu-id="06205-107">Ele oferece acesso a uma instância do Redis segura e dedicada, gerenciada pela Microsoft e acessível desde os seus aplicativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="06205-107">It gives you access to a secure, dedicated Redis instance, managed by Microsoft and accessible from your Azure apps.</span></span>

<span data-ttu-id="06205-108">O Redis é um repositório de chave-valor avançado, no qual as chaves podem conter estruturas de dados como cadeias de caracteres, hashes, listas, conjuntos e conjuntos classificados.</span><span class="sxs-lookup"><span data-stu-id="06205-108">Redis is an advanced key-value store, where keys can contain data structures such as strings, hashes, lists, sets, and sorted sets.</span></span> <span data-ttu-id="06205-109">O Redis dá suporte a um conjunto de operações atômicas nesses tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="06205-109">Redis supports a set of atomic operations on these data types.</span></span>

<span data-ttu-id="06205-110">Saiba mais sobre o [Cache Redis do Azure](https://docs.microsoft.com/azure/redis-cache/).</span><span class="sxs-lookup"><span data-stu-id="06205-110">Learn more about [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span></span>

## <a name="management-api"></a><span data-ttu-id="06205-111">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="06205-111">Management API</span></span>

<span data-ttu-id="06205-112">Criar e gerenciar recursos do Redis na sua assinatura com a API de gerenciamento do Redis.</span><span class="sxs-lookup"><span data-stu-id="06205-112">Create and manage your Redis resources in your subscription with the Redis management API.</span></span>

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a><span data-ttu-id="06205-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="06205-113">Example</span></span>

<span data-ttu-id="06205-114">O exemplo a seguir cria um novo cache Redis:</span><span class="sxs-lookup"><span data-stu-id="06205-114">The following example creates a new Redis cache:</span></span>

```python
from azure.mgmt.redis import RedisManagementClient
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

redis_client = RedisManagementClient(
    credentials,
    subscription_id
)
group_name = 'myresourcegroup'
cache_name = 'mycachename'
redis_cache = redis_client.redis.create_or_update(
    group_name,
    cache_name,
    RedisCreateOrUpdateParameters(
        sku = Sku(name = 'Basic', family = 'C', capacity = '1'),
        location = "East US"
    )
)
# redis_cache is a RedisResourceWithAccessKey instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="06205-115">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="06205-115">Explore the Management APIs</span></span>](/python/api/overview/azure/redis/management)

