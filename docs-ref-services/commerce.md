---
title: Bibliotecas de Comércio do Azure para Python
description: Referência para bibliotecas de Comércio do Azure para Python
keywords: Azure, Python, SDK, API, Comércio
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 27b826c1f11aca0d8c49c4e8eab4277b857eea37
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277228"
---
# <a name="azure-commerce-libraries-for-python"></a><span data-ttu-id="c256c-104">Bibliotecas de Comércio do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="c256c-104">Azure Commerce libraries for python</span></span>

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[<span data-ttu-id="c256c-105">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c256c-105">Management API</span></span>](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a><span data-ttu-id="c256c-106">Criar o cliente de comércio</span><span class="sxs-lookup"><span data-stu-id="c256c-106">Create the commerce client</span></span>

<span data-ttu-id="c256c-107">O código a seguir cria uma instância do cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c256c-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="c256c-108">Será preciso fornecer sua ``subscription_id``, que pode ser recuperada de [sua lista de assinatura](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="c256c-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="c256c-109">Consulte [Autenticação de gerenciamento de recursos](/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre o tratamento da autenticação do Azure Active Directory com o SDK do Python e sobre a criação de uma instância ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="c256c-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

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

## <a name="get-rate-card"></a><span data-ttu-id="c256c-110">Obter cartão de avaliação</span><span class="sxs-lookup"><span data-stu-id="c256c-110">Get rate card</span></span>

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a><span data-ttu-id="c256c-111">Obter o uso</span><span class="sxs-lookup"><span data-stu-id="c256c-111">Get Usage</span></span>

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
> [<span data-ttu-id="c256c-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c256c-112">Explore the Management APIs</span></span>](/python/api/overview/azure/commerce/management)