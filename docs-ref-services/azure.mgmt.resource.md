---
title: Bibliotecas de Recursos do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, Recursos
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534375"
---
# <a name="azure-resources-libraries-for-python"></a>Bibliotecas de Recursos do Azure para Python 

## <a name="overview"></a>Visão geral 
Gerenciar recursos do Azure nos grupos de recursos.

| Pacote  |  DESCRIÇÃO |
|---|---|
|[azure.mgmt.resource.features][1]|O Controle de Exposição de Recurso do Azure (AFEC) fornece um mecanismo para os provedores de recursos controlar a exposição de recurso aos usuários.|
|[azure.mgmt.resource.links][2]|Os recursos do Azure podem ser vinculados para formarem a relações lógicas. Você pode estabelecer links entre recursos que pertencem a grupos de recursos diferentes.|
|[azure.mgmt.resource.locks][3]|Os recursos do Azure podem ser bloqueados para impedir que outros usuários na sua organização excluam ou modifiquem os recursos.|
|[azure.mgmt.resource.managedapplications][4]|Aplicativos gerenciados de ARM (dispositivos).|
|[azure.mgmt.resource.policy][5]|Para gerenciar e controlar o acesso aos recursos, você pode definir políticas personalizadas e atribuí-las a um escopo.|
|[azure.mgmt.resource.resources][6]| Fornece operações para trabalhar com recursos e grupos de recursos.|
|[azure.mgmt.resource.subscriptions][7]|Todos os grupos de recursos e recursos existem em assinaturas. Essa operação permite obter informações sobre suas assinaturas e locatários.|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a>Instalar as bibliotecas 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a>Exemplo
Abaixo está um exemplo de como criar um grupo de recursos. 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos. 