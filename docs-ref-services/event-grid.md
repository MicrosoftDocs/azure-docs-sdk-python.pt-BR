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
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="34e02-103">Bibliotecas da Grade de Eventos para Python</span><span class="sxs-lookup"><span data-stu-id="34e02-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="34e02-104">A Grade de Eventos do Azure é um serviço de roteamento de eventos inteligente totalmente gerenciado que permite um consumo de eventos uniforme usando um modelo do tipo publicar-assinar.</span><span class="sxs-lookup"><span data-stu-id="34e02-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="34e02-105">[Saiba mais](/azure/event-grid/overview) sobre a Grade de Eventos do Azure e começar a usar o [tutorial de eventos do armazenamento de Blobs do Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="34e02-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="34e02-106">Publicar SDK</span><span class="sxs-lookup"><span data-stu-id="34e02-106">Publish SDK</span></span>

<span data-ttu-id="34e02-107">Autentique, crie, manipule e publique tópicos usando a Grade de Eventos do Azure para publicação de SDK.</span><span class="sxs-lookup"><span data-stu-id="34e02-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="34e02-108">Instalação</span><span class="sxs-lookup"><span data-stu-id="34e02-108">Installation</span></span> 

<span data-ttu-id="34e02-109">Instale o pacote com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="34e02-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="34e02-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="34e02-110">Example</span></span> 

<span data-ttu-id="34e02-111">O código a seguir publica um evento para um tópico.</span><span class="sxs-lookup"><span data-stu-id="34e02-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="34e02-112">Você pode recuperar a chave do tópico e o ponto de extremidade por meio do Portal do Azure ou através da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="34e02-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

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
> [<span data-ttu-id="34e02-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="34e02-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="34e02-114">SDK de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="34e02-114">Management SDK</span></span>

<span data-ttu-id="34e02-115">Crie, atualize ou exclua instâncias da Grade de Eventos, tópicos e assinaturas com o SDK de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="34e02-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="34e02-116">Instalação</span><span class="sxs-lookup"><span data-stu-id="34e02-116">Installation</span></span> 

<span data-ttu-id="34e02-117">Instale o pacote com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="34e02-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="34e02-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="34e02-118">Example</span></span>

<span data-ttu-id="34e02-119">O exemplo a seguir cria um tópico personalizado e assina um ponto de extremidade para o tópico.</span><span class="sxs-lookup"><span data-stu-id="34e02-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="34e02-120">Em seguida, o código envia um evento para o tópico através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="34e02-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="34e02-121">O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele.</span><span class="sxs-lookup"><span data-stu-id="34e02-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="34e02-122">Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="34e02-122">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="34e02-123">Copie a URL do compartimento, pois você precisará dela para assinar o tópico.</span><span class="sxs-lookup"><span data-stu-id="34e02-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="34e02-124">Navegue até a URL de RequestBin criada anteriormente para ver os eventos que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="34e02-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="34e02-125">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="34e02-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="34e02-126">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="34e02-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="34e02-127">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="34e02-127">Learn more</span></span>

[<span data-ttu-id="34e02-128">Receber eventos usando o SDK de Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="34e02-128">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)
