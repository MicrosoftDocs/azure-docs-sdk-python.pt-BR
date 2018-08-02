---
title: Bibliotecas de Barramento de Serviço para Python
description: Documentação de referência para as bibliotecas de gerenciamento e de cliente de Python para Barramento de Serviço
keywords: Azure, Python, SDK, API, sistema de mensagens, pubsub, pub-sub, agente de mensagens
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 02c172ff1a54d060c6af36a5a5daa5dcbff8795c
ms.sourcegitcommit: e35ec475d4b9d8061d0528a93aa8e1c4b7db6c0d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39418951"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="24115-104">Bibliotecas de Barramento de Serviço para Python</span><span class="sxs-lookup"><span data-stu-id="24115-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="24115-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="24115-105">Overview</span></span>

<span data-ttu-id="24115-106">O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável.</span><span class="sxs-lookup"><span data-stu-id="24115-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="24115-107">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="24115-107">Install the libraries</span></span>
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a><span data-ttu-id="24115-108">Filas do ServiceBus</span><span class="sxs-lookup"><span data-stu-id="24115-108">ServiceBus Queues</span></span>
<span data-ttu-id="24115-109">As Filas do ServiceBus são uma alternativa às Filas de Armazenamento que possam ser úteis em cenários em que são necessários recursos de mensagens mais avançados (tamanhos maiores de mensagem, classificação das mensagens, leituras destrutivas de única operação, entrega agendada) usando a entrega de estilo push (usando sondagem longa).</span><span class="sxs-lookup"><span data-stu-id="24115-109">ServiceBus Queues are an alternative to Storage Queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

<span data-ttu-id="24115-110">O serviço pode usar a autenticação de Assinatura de Acesso Compartilhado ou autenticação de ACS.</span><span class="sxs-lookup"><span data-stu-id="24115-110">The service can use Shared Access Signature authentication, or ACS authentication.</span></span>

<span data-ttu-id="24115-111">Os namespaces de barramento de serviço criados usando o portal do Azure depois de agosto de 2014 não oferecem mais suporte à autenticação de ACS.</span><span class="sxs-lookup"><span data-stu-id="24115-111">Service bus namespaces created using the Azure portal after August 2014 no longer support ACS authentication.</span></span> <span data-ttu-id="24115-112">É possível criar namespaces compatíveis do ACS com o SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="24115-112">You can create ACS compatible namespaces with the Azure SDK.</span></span>

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="24115-113">Autenticação de Assinatura de Acesso Compartilhado</span><span class="sxs-lookup"><span data-stu-id="24115-113">Shared Access Signature Authentication</span></span>

<span data-ttu-id="24115-114">Para usar a autenticação de Assinatura de Acesso Compartilhado, crie o barramento de serviço com:</span><span class="sxs-lookup"><span data-stu-id="24115-114">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a><span data-ttu-id="24115-115">Autenticação de ACS</span><span class="sxs-lookup"><span data-stu-id="24115-115">ACS Authentication</span></span>

<span data-ttu-id="24115-116">Para usar a autenticação de ACS, crie o serviço do barramento de serviço com:</span><span class="sxs-lookup"><span data-stu-id="24115-116">To use ACS authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a><span data-ttu-id="24115-117">Como enviar e receber mensagens</span><span class="sxs-lookup"><span data-stu-id="24115-117">Sending and Receiving Messages</span></span>

<span data-ttu-id="24115-118">O método **create\_queue** pode ser usado para garantir que exista uma fila:</span><span class="sxs-lookup"><span data-stu-id="24115-118">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="24115-119">O método **send\_queue\_message** pode, então, ser chamado para inserir a mensagem na fila:</span><span class="sxs-lookup"><span data-stu-id="24115-119">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="24115-120">O método **send\_queue\_message_batch** pode, então, ser chamado para enviar várias mensagens de uma vez:</span><span class="sxs-lookup"><span data-stu-id="24115-120">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="24115-121">Assim, é possível chamar o método **receive\_queue\_message** para remover a mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="24115-121">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a><span data-ttu-id="24115-122">Tópicos do ServiceBus</span><span class="sxs-lookup"><span data-stu-id="24115-122">ServiceBus Topics</span></span>

<span data-ttu-id="24115-123">Os tópicos do ServiceBus são uma abstração sobre as Filas do ServiceBus, que tornam os cenários de publicação/assinatura fáceis de implementar.</span><span class="sxs-lookup"><span data-stu-id="24115-123">ServiceBus topics are an abstraction on top of ServiceBus Queues that make pub/sub scenarios easy to implement.</span></span>

<span data-ttu-id="24115-124">O método **create\_topic** pode ser usado para criar um tópico no servidor:</span><span class="sxs-lookup"><span data-stu-id="24115-124">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="24115-125">O método **send\_topic\_message** pode ser usado para enviar uma mensagem para um tópico:</span><span class="sxs-lookup"><span data-stu-id="24115-125">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="24115-126">O método **send\_topic\_message_batch** pode ser usado para enviar várias mensagens de uma vez:</span><span class="sxs-lookup"><span data-stu-id="24115-126">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="24115-127">Leve em consideração que, no Python 3, uma mensagem str será codificada em utf-8 e você deve ter de gerenciar sua codificação por conta própria no Python 2.</span><span class="sxs-lookup"><span data-stu-id="24115-127">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="24115-128">Um cliente pode criar uma assinatura e começar a consumir mensagens chamando o método **create\_subscription** seguido do método **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="24115-128">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="24115-129">Observe que todas as mensagens enviadas antes da assinatura ser criada não serão recebidas.</span><span class="sxs-lookup"><span data-stu-id="24115-129">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a><span data-ttu-id="24115-130">Hub de evento</span><span class="sxs-lookup"><span data-stu-id="24115-130">Event Hub</span></span>

<span data-ttu-id="24115-131">Os Hubs de Eventos habilitam a coleção de fluxos de eventos com alta taxa de transferência em um conjunto diversificado de dispositivos e serviços.</span><span class="sxs-lookup"><span data-stu-id="24115-131">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="24115-132">O método **create\_event\_hub** pode ser usado para criar um hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="24115-132">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="24115-133">Para enviar um evento:</span><span class="sxs-lookup"><span data-stu-id="24115-133">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="24115-134">O conteúdo do evento é a mensagem de evento ou uma cadeia de caracteres codificada em JSON que contém várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="24115-134">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="24115-135">Recursos avançados</span><span class="sxs-lookup"><span data-stu-id="24115-135">Advanced features</span></span>

### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="24115-136">Propriedades do agente e propriedades de usuário</span><span class="sxs-lookup"><span data-stu-id="24115-136">Broker Properties and User Properties</span></span>

<span data-ttu-id="24115-137">Esta seção descreve como usar as propriedades do Agente e do Usuário definidas [aqui](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="24115-137">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
<span data-ttu-id="24115-138">É possível usar datetime, int, float ou booleano</span><span class="sxs-lookup"><span data-stu-id="24115-138">You can use datetime, int, float or boolean</span></span>

```python
props = {'hello': 'world',
            'number': 42,
            'active': True,
            'deceased': False,
            'large': 8555111000,
            'floating': 3.14,
            'dob': datetime(2011, 12, 14),
            'double_quote_message': 'This "should" work fine',
            'quote_message': "This 'should' work fine"}
sent_msg = Message(b'message with properties', custom_properties=props)
```
<span data-ttu-id="24115-139">Por questões de compatibilidade com a versão antiga dessa biblioteca, `broker_properties` também pode ser definido como uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="24115-139">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="24115-140">Se essa for a situação, você é o responsável por gravar uma cadeia de caracteres JSON válida, e nenhuma verificação será feita pelo Python antes do envio à API Rest.</span><span class="sxs-lookup"><span data-stu-id="24115-140">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="24115-141">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="24115-141">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/management)
