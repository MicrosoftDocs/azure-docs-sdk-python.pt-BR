---
title: Bibliotecas de Grade de Eventos do Azure para Python
description: 
keywords: Azure, Python, SDK, API, Grade de Eventos
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: 81c4e74b00ac59c789c5a0b83eaa10652ec6d8ac
ms.sourcegitcommit: db4608e494cb4340649bce98ba9fb4504d3686bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2017
---
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Barramento de Serviço para Python

## <a name="overview"></a>Visão geral
A Grade de Eventos do Azure é um serviço de roteamento de eventos inteligente totalmente gerenciado que permite um consumo de eventos uniforme usando um modelo do tipo publicar-assinar.

## <a name="management-api"></a>API de gerenciamento
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Exemplo
O exemplo a seguir cria um tópico personalizado, assina o tópico e aciona o evento para exibir o resultado. O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele. Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**. Copie a URL do compartimento, pois você precisará dela para assinar o tópico.

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
Navegue até a URL de RequestBin criada anteriormente para ver os eventos que acabamos de enviar.

Limpar recursos
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/eventgrid/managementlibrary)

