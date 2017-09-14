---
title: Bibliotecas de Rede do Azure para Python
description: "Referência para bibliotecas de Rede do Azure para Python"
keywords: Azure, Python, SDK, API, Rede
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: ed6ddfe4d1f4d860952369a75e10166a1f22c483
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-network-libraries-for-python"></a><span data-ttu-id="620e1-104">Bibliotecas de Rede do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="620e1-104">Azure Network libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="620e1-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="620e1-105">Overview</span></span>

<span data-ttu-id="620e1-106">A [Rede Virtual do Azure](/azure/virtual-network/virtual-networks-overview) permite a você conectar-se aos recursos do Azure e também conectá-los à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="620e1-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows you to connect Azure resources, and also connect them to your on-premises network.</span></span>

<span data-ttu-id="620e1-107">Para começar a usar a Rede Virtual do Azure, consulte [Criar sua primeira rede virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="620e1-107">To get started with Azure Virtual Network, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-apis"></a><span data-ttu-id="620e1-108">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="620e1-108">Management APIs</span></span>

<span data-ttu-id="620e1-109">Inspecionar, gerenciar e configurar redes virtuais do Azure com as APIs de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="620e1-109">Inspect, manage, and configure Azure virtual networks with the management APIs.</span></span>

<span data-ttu-id="620e1-110">Diferentemente de outras APIs de Python do Azure, as APIs de rede são explicitamente divididas em versões em pacotes separados.</span><span class="sxs-lookup"><span data-stu-id="620e1-110">Unlike other Azure python APIs, the networking APIs are explicitly versioned into separage packages.</span></span> <span data-ttu-id="620e1-111">Você não precisa importá-las individualmente, pois as informações do pacote são especificadas no construtor do cliente.</span><span class="sxs-lookup"><span data-stu-id="620e1-111">You do not need to import them individually since the package information is specified in the client constructor.</span></span>

<span data-ttu-id="620e1-112">Instalar o pacote de gerenciamento com PIP.</span><span class="sxs-lookup"><span data-stu-id="620e1-112">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-network
```

### <a name="example"></a><span data-ttu-id="620e1-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="620e1-113">Example</span></span>

<span data-ttu-id="620e1-114">Criar uma rede virtual e uma sub-rede associado.</span><span class="sxs-lookup"><span data-stu-id="620e1-114">Create a virtual network and an associated subnet.</span></span>

```python
from azure.mgmt.network import NetworkManagementClient

GROUP_NAME = 'resource-group'
VNET_NAME = 'your-vnet-identifier'
LOCATION = 'region'
SUBNET_NAME = 'your-subnet-identifier'

network_client = NetworkManagementClient(credentials, 'your-subscription-id')

async_vnet_creation = network_client.virtual_networks.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    {
        'location': LOCATION,
        'address_space': {
            'address_prefixes': ['10.0.0.0/16']
        }
    }
)
async_vnet_creation.wait()

# Create Subnet
async_subnet_creation = network_client.subnets.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    SUBNET_NAME,
    {'address_prefix': '10.0.0.0/24'}
)
subnet_info = async_subnet_creation.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="620e1-115">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="620e1-115">Explore the Management APIs</span></span>](/python/api/overview/azure/network/managementlibrary)

### <a name="samples"></a><span data-ttu-id="620e1-116">Exemplos</span><span class="sxs-lookup"><span data-stu-id="620e1-116">Samples</span></span>

* <span data-ttu-id="620e1-117">[Introdução ao Azure Resource Manager para balanceadores de carga no Python][1]</span><span class="sxs-lookup"><span data-stu-id="620e1-117">[Getting started with Azure Resource Manager for load balancers in Python][1]</span></span>

<span data-ttu-id="620e1-118">Veja a [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) de exemplos da Rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="620e1-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) of Azure Virtual Network samples.</span></span>

[1]: [https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/]
