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
ms.openlocfilehash: 47252ca3b2f5c6087277bac3735025f0dbabbdd8
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-network-libraries-for-python"></a>Bibliotecas de Rede do Azure para Python

## <a name="overview"></a>Visão geral

A [Rede Virtual do Azure](/azure/virtual-network/virtual-networks-overview) permite a você conectar-se aos recursos do Azure e também conectá-los à sua rede local.

Para começar a usar a Rede Virtual do Azure, consulte [Criar sua primeira rede virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-apis"></a>APIs de gerenciamento

Inspecionar, gerenciar e configurar redes virtuais do Azure com as APIs de gerenciamento.

Diferentemente de outras APIs de Python do Azure, as APIs de rede são explicitamente divididas em versões em pacotes separados. Você não precisa importá-las individualmente, pois as informações do pacote são especificadas no construtor do cliente.

Instalar o pacote de gerenciamento com PIP.

```bash
pip install azure-mgmt-network
```

### <a name="example"></a>Exemplo

Criar uma rede virtual e uma sub-rede associado.

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/network/management)

### <a name="samples"></a>Exemplos

* [Introdução ao Azure Resource Manager para os balanceadores de carga no Python](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

Veja a [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) de exemplos da Rede Virtual do Azure.
