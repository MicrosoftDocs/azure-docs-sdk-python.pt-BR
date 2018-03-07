---
title: Bibliotecas de DNS do Azure para Python
description: "Referência para bibliotecas de DNS do Azure para Python"
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
---
# <a name="azure-dns-libraries-for-python"></a>Bibliotecas de DNS do Azure para Python

## <a name="overview"></a>Visão geral

O [DNS do Azure](/azure/dns/dns-overview) é um serviço de hospedagem para domínios DNS que fornece resolução de DNS usando a infraestrutura do Azure.

Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando o portal do Azure](/azure/dns/dns-getstarted-portal).

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a>Criar o cliente de gerenciamento

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

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

## <a name="create-dns-zone"></a>Criar zona DNS
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
    
## <a name="create-a-record-set"></a>Criar um conjunto de registros
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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/dns/management)
