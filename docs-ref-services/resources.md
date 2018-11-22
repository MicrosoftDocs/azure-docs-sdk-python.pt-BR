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
# <a name="azure-resources-libraries-for-python"></a>Bibliotecas de recursos do Azure para Python

## <a name="overview"></a>Visão geral 
Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de gerenciamento
Use a API de gerenciamento para criar grupos de recursos e implantar recursos de modelos.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>Exemplo 
Criar um novo grupo de recursos na região Leste dos EUA do Azure.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>Exemplos
[Gerenciar recursos e grupos de recursos do Azure](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

Exibir a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) de amostras do Azure Resource Manager.
