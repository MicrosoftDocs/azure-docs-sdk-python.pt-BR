---
title: Bibliotecas de Grade de Eventos do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, Grade de Eventos
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: bfaa1908295eb77531e399f1337acdeee512005f
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276830"
---
# <a name="event-grid-libraries-for-python"></a>Bibliotecas da Grade de Eventos para Python


A Grade de Eventos do Azure é um serviço de roteamento de eventos inteligente totalmente gerenciado que permite um consumo de eventos uniforme usando um modelo do tipo publicar-assinar.

[Saiba mais](/azure/event-grid/overview) sobre a Grade de Eventos do Azure e começar a usar o [tutorial de eventos do armazenamento de Blobs do Azure](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="publish-sdk"></a>Publicar SDK

Autentique, crie, manipule e publique tópicos usando a Grade de Eventos do Azure para publicação de SDK.

### <a name="installation"></a>Instalação 

Instale o pacote com [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-eventgrid
```

### <a name="example"></a>Exemplo 

O código a seguir publica um evento para um tópico. Você pode recuperar a chave do tópico e o ponto de extremidade por meio do Portal do Azure ou através da CLI do Azure:

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>SDK de Gerenciamento

Crie, atualize ou exclua instâncias da Grade de Eventos, tópicos e assinaturas com o SDK de gerenciamento.

### <a name="installation"></a>Instalação 

Instale o pacote com [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Exemplo

O exemplo a seguir cria um tópico personalizado e assina um ponto de extremidade para o tópico. Em seguida, o código envia um evento para o tópico através de HTTPS.
O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele. Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**. Copie a URL do compartimento, pois você precisará dela para assinar o tópico.

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>Saiba mais

[Receber eventos usando o SDK de Grade de Eventos](/azure/event-grid/receive-events)
