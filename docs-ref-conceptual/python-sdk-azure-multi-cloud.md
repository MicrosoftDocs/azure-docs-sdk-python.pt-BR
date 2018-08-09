---
title: Uso de várias nuvens
description: no Azure em todas as regiões
author: lmazuel
ms.author: lmazuel
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: a4d006e6244bf6fb1151e32583e8bc3a642d4663
ms.sourcegitcommit: 8a9e4295359a4f47b21908541e2460c333e94a0a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39624972"
---
# <a name="multi-cloud---use-azure-on-all-regions"></a><span data-ttu-id="9455e-103">Uso de várias nuvens no Azure em todas as regiões</span><span class="sxs-lookup"><span data-stu-id="9455e-103">Multi-cloud - use Azure on all regions</span></span>

<span data-ttu-id="9455e-104">É possível usar o SDK do Azure para Python para conectar-se a todas as regiões em que o Azure [está disponível](https://azure.microsoft.com/regions/services).</span><span class="sxs-lookup"><span data-stu-id="9455e-104">You can use the Azure SDK for Python to connect to all regions where Azure is [available](https://azure.microsoft.com/regions/services).</span></span>

<span data-ttu-id="9455e-105">Por padrão, o SDK do Azure para Python está configurado para se conectar ao Azure público.</span><span class="sxs-lookup"><span data-stu-id="9455e-105">By default, the Azure SDK for Python is configured to connect to public Azure.</span></span>

## <a name="using-predeclared-cloud-definition"></a><span data-ttu-id="9455e-106">Usando definições de nuvem declaradas previamente</span><span class="sxs-lookup"><span data-stu-id="9455e-106">Using predeclared cloud definition</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9455e-107">O pacote `msrestazure` deve ser superior ou igual a 0.4.11 para esta seção.</span><span class="sxs-lookup"><span data-stu-id="9455e-107">The `msrestazure` package must be superior or equals to 0.4.11 for this section.</span></span>

<span data-ttu-id="9455e-108">Você pode usar o módulo `azure_cloud` do `msrestazure`</span><span class="sxs-lookup"><span data-stu-id="9455e-108">You can use the `azure_cloud` module of `msrestazure`</span></span>

```python
from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=AZURE_CHINA_CLOUD
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager
)
``` 
  
<span data-ttu-id="9455e-109">As definições de nuvem disponíveis são</span><span class="sxs-lookup"><span data-stu-id="9455e-109">Available cloud definition are</span></span>
  - <span data-ttu-id="9455e-110">AZURE_PUBLIC_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9455e-110">AZURE_PUBLIC_CLOUD</span></span>
  - <span data-ttu-id="9455e-111">AZURE_CHINA_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9455e-111">AZURE_CHINA_CLOUD</span></span>
  - <span data-ttu-id="9455e-112">AZURE_US_GOV_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9455e-112">AZURE_US_GOV_CLOUD</span></span>
  - <span data-ttu-id="9455e-113">AZURE_GERMAN_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9455e-113">AZURE_GERMAN_CLOUD</span></span>

## <a name="using-your-own-cloud-definition-eg-azure-stack"></a><span data-ttu-id="9455e-114">Usando sua própria definição de nuvem (por exemplo, Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="9455e-114">Using your own cloud definition (e.g. Azure Stack)</span></span>
<span data-ttu-id="9455e-115">O ARM tem um ponto de extremidade de metadados para ajudá-lo:</span><span class="sxs-lookup"><span data-stu-id="9455e-115">ARM has a metadata endpoint to help you:</span></span>

```python
from msrestazure.azure_cloud import get_cloud_from_metadata_endpoint
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

mystack_cloud = get_cloud_from_metadata_endpoint("https://myazurestack-arm-endpoint.com")
credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=mystack_cloud
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=mystack_cloud.endpoints.resource_manager
)
```
## <a name="using-adal"></a><span data-ttu-id="9455e-116">Usando o ADAL</span><span class="sxs-lookup"><span data-stu-id="9455e-116">Using ADAL</span></span>

<span data-ttu-id="9455e-117">Para se conectar a outra região, algumas coisas precisam ser consideradas:</span><span class="sxs-lookup"><span data-stu-id="9455e-117">To connect to another region, a few things have to be considered:</span></span>

- <span data-ttu-id="9455e-118">Qual é o ponto de extremidade no qual se solicita um token (autenticação)?</span><span class="sxs-lookup"><span data-stu-id="9455e-118">What is the endpoint where to ask for a token (authentication)?</span></span>
- <span data-ttu-id="9455e-119">Qual é o ponto de extremidade no qual vou usar esse token (uso)?</span><span class="sxs-lookup"><span data-stu-id="9455e-119">What is the endpoint where I will use this token (usage)?</span></span>

<span data-ttu-id="9455e-120">Este é um exemplo genérico:</span><span class="sxs-lookup"><span data-stu-id="9455e-120">This is a generic example:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Public Azure - default values
authentication_endpoint = 'https://login.microsoftonline.com/'
azure_endpoint = 'https://management.azure.com/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-government"></a><span data-ttu-id="9455e-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="9455e-121">Azure Government</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Government
authentication_endpoint = 'https://login.microsoftonline.us/'
azure_endpoint = 'https://management.usgovcloudapi.net/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-germany"></a><span data-ttu-id="9455e-122">Azure Alemanha</span><span class="sxs-lookup"><span data-stu-id="9455e-122">Azure Germany</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure Germany
authentication_endpoint = 'https://login.microsoftonline.de/'
azure_endpoint = 'https://management.microsoftazure.de/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-china"></a><span data-ttu-id="9455e-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="9455e-123">Azure China</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure China
authentication_endpoint = 'https://login.chinacloudapi.cn/'
azure_endpoint = 'https://management.chinacloudapi.cn/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```
