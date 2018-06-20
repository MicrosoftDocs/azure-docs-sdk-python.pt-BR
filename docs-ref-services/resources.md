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
ms.openlocfilehash: d924a8aea18d9b59ec8c78d85dce8fe0ce7c8d6c
ms.sourcegitcommit: d521a7350216461eb2fa68152c4975f55152f831
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/06/2017
ms.locfileid: "26327984"
---
# <a name="azure-resources-libraries-for-python"></a>Bibliotecas de recursos do Azure para Python

## <a name="overview"></a>Visão geral 
Implantar, monitorar e gerenciar recursos em grupos com o [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de Gerenciamento
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
