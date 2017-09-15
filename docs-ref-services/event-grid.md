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
ms.openlocfilehash: a50a203a0733f25f2a88d6f4a43c6bddc388d3e7
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2017
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="19e66-103">Bibliotecas da Grade de Eventos para Python</span><span class="sxs-lookup"><span data-stu-id="19e66-103">Event Grid libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="19e66-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="19e66-104">Overview</span></span>
<span data-ttu-id="19e66-105">A Grade de Eventos do Azure é um serviço de roteamento de eventos inteligente totalmente gerenciado que permite um consumo de eventos uniforme usando um modelo do tipo publicar-assinar.</span><span class="sxs-lookup"><span data-stu-id="19e66-105">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

## <a name="management-api"></a><span data-ttu-id="19e66-106">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="19e66-106">Management API</span></span>
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="19e66-107">Exemplo</span><span class="sxs-lookup"><span data-stu-id="19e66-107">Example</span></span>
<span data-ttu-id="19e66-108">O exemplo a seguir cria um tópico personalizado, assina o tópico e aciona o evento para exibir o resultado.</span><span class="sxs-lookup"><span data-stu-id="19e66-108">The following creates a custom topic, subscribes to the topic, and triggers the event to view the result.</span></span> <span data-ttu-id="19e66-109">O RequestBin é uma ferramenta de terceiros de software livre que permite criar um ponto de extremidade e exibir as solicitações enviadas a ele.</span><span class="sxs-lookup"><span data-stu-id="19e66-109">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="19e66-110">Vá para [RequestBin](https://requestb.in/)e clique em **Criar um RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="19e66-110">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="19e66-111">Copie a URL do compartimento, pois você precisará dela para assinar o tópico.</span><span class="sxs-lookup"><span data-stu-id="19e66-111">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="19e66-112">Navegue até a URL de RequestBin criada anteriormente para ver os eventos que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="19e66-112">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="19e66-113">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="19e66-113">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="19e66-114">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="19e66-114">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/managementlibrary)

