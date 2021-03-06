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
# <a name="azure-redis-cache-libraries-for-python"></a>Bibliotecas do Cache Redis do Azure para Python

## <a name="overview"></a>Visão geral

O Cache Redis do Azure se baseia no popular projeto Redis de software livre. Ele oferece acesso a uma instância do Redis segura e dedicada, gerenciada pela Microsoft e acessível desde os seus aplicativos do Azure.

O Redis é um repositório de chave-valor avançado, no qual as chaves podem conter estruturas de dados como cadeias de caracteres, hashes, listas, conjuntos e conjuntos classificados. O Redis dá suporte a um conjunto de operações atômicas nesses tipos de dados.

Saiba mais sobre o [Cache Redis do Azure](https://docs.microsoft.com/azure/redis-cache/).

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar recursos do Redis na sua assinatura com a API de gerenciamento do Redis.

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a>Exemplo

O exemplo a seguir cria um novo cache Redis:

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/redis/management)

