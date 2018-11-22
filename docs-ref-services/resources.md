---
title: Bibliotecas de recursos do Azure para Python
description: Referência para bibliotecas de recursos do Azure para Python
keywords: Azure, Python, SDK, API, Recursos
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f331a88ceac73449c9c1aff7bccbbaff4c4ba7be
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277373"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="86e79-104">Bibliotecas de recursos do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="86e79-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="86e79-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="86e79-105">Overview</span></span> 
<span data-ttu-id="86e79-106">Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="86e79-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="86e79-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="86e79-107">Management API</span></span>
<span data-ttu-id="86e79-108">Use a API de gerenciamento para criar grupos de recursos e implantar recursos de modelos.</span><span class="sxs-lookup"><span data-stu-id="86e79-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="86e79-109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="86e79-109">Example</span></span> 
<span data-ttu-id="86e79-110">Criar um novo grupo de recursos na região Leste dos EUA do Azure.</span><span class="sxs-lookup"><span data-stu-id="86e79-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="86e79-111">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="86e79-111">Explore the Management APIs</span></span>](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a><span data-ttu-id="86e79-112">Exemplos</span><span class="sxs-lookup"><span data-stu-id="86e79-112">Samples</span></span>
[<span data-ttu-id="86e79-113">Gerenciar recursos e grupos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="86e79-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="86e79-114">Exibir a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) de amostras do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86e79-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
