---
title: "Bibliotecas de Comércio do Azure para Python"
description: "Referência para bibliotecas de Comércio do Azure para Python"
keywords: "Azure, Python, SDK, API, Comércio"
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 77008eb76c3a925d9c7e63fe9360ea5b25da49de
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/24/2018
---
# <a name="azure-commerce-libraries-for-python"></a>Bibliotecas de Comércio do Azure para Python

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[API de Gerenciamento](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a>Criar o cliente de comércio

O código a seguir cria uma instância do cliente de gerenciamento.

Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.

```python
from azure.mgmt.commerce import UsageManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

commerce_client = UsageManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="get-rate-card"></a>Obter cartão de avaliação

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a>Obter o uso

```python
from datetime import date, timedelta

# Takes onky dates in full ISO8601 with 'T00:00:00Z'
# Return an iterator like object: https://docs.python.org/3/library/stdtypes.html#iterator-types
usage_iterator = commerce_client.usage_aggregates.list(
    str(date.today() - timedelta(days=1))+'T00:00:00Z',
    str(date.today())+'T00:00:00Z'
)
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/commerce/management)