---
title: Bibliotecas do Azure Data Factory para Python
description: Referência para bibliotecas do Azure Data Factory para Python
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 05/10/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 05d93f7d1838c110c3ba77f7abd3967f7870774b
ms.sourcegitcommit: d65549030a0edb50d75482f79aac0962d1dacb57
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34759040"
---
# <a name="azure-data-factory-libraries-for-python"></a>Bibliotecas do Azure Data Factory para Python

Compor armazenamento de dados, movimento e serviços de processamento em pipelines de dados simplificados com o [Azure Data Factory](/azure/data-factory/)

[Saiba mais](/azure/data-factory/introduction) sobre o Data Factory e comece com o [Início Rápido - Criar um data factory e pipeline usando o Python](/azure/data-factory/quickstart-create-data-factory-python). 

## <a name="management-module"></a>Módulo de gerenciamento

Crie e gerencie instâncias do Data Factory em sua assinatura com o módulo de gerenciamento.

### <a name="installation"></a>Instalação

Instale o pacote com [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a>Exemplo 

Crie um Data Factory em sua assinatura na região Leste dos EUA.

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
import time

#Create a data factory
subscription_id = '<Specify your Azure Subscription ID>'
credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
adf_client = DataFactoryManagementClient(credentials, subscription_id)

rg_params = {'location':'eastus'}
df_params = {'location':'eastus'}  

df_resource = Factory(location='eastus')
df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
print_item(df)
while df.provisioning_state != 'Succeeded':
    df = adf_client.factories.get(rg_name, df_name)
    time.sleep(1)
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/datafactory/management)