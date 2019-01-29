---
title: Bibliotecas de Barramento de Serviço para Python
description: Documentação de referência para as bibliotecas de gerenciamento e de cliente de Python para Barramento de Serviço
keywords: Azure, Python, SDK, API, sistema de mensagens, pubsub, pub-sub, agente de mensagens
author: annatisch
ms.author: antisch
manager: mayurid
ms.date: 01/15/2019
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 540a2a248f7a2abcc83517bc4a4ef96ef03e8a9f
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747736"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="e594a-104">Bibliotecas de Barramento de Serviço para Python</span><span class="sxs-lookup"><span data-stu-id="e594a-104">Service Bus libraries for Python</span></span>

<span data-ttu-id="e594a-105">O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável.</span><span class="sxs-lookup"><span data-stu-id="e594a-105">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span>

* [<span data-ttu-id="e594a-106">Código-fonte do SDK</span><span class="sxs-lookup"><span data-stu-id="e594a-106">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="e594a-107">Documentação de referência do SDK</span><span class="sxs-lookup"><span data-stu-id="e594a-107">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a><span data-ttu-id="e594a-108">Quais as novidades na v0.50.0?</span><span class="sxs-lookup"><span data-stu-id="e594a-108">What's new in v0.50.0?</span></span>
<span data-ttu-id="e594a-109">A partir da versão 0.50.0, uma nova API baseada em AMQP está disponível para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="e594a-109">As of version 0.50.0 a new AMQP-based API is available for sending and receiving messages.</span></span> <span data-ttu-id="e594a-110">Essa atualização envolve **alterações de falhas**.</span><span class="sxs-lookup"><span data-stu-id="e594a-110">This update involves **breaking changes**.</span></span>
<span data-ttu-id="e594a-111">Leia a [Migração da v0.21.1 para v0.50.0](#migration-from-v0211-to-v0500) para determinar se a atualização é ideal para você no momento.</span><span class="sxs-lookup"><span data-stu-id="e594a-111">Please read [Migration from v0.21.1 to v0.50.0](#migration-from-v0211-to-v0500) to determine if upgrading is right for you at this time.</span></span>

<span data-ttu-id="e594a-112">A nova API baseada em AMQP oferece desempenho e confiabilidade de transmissão de mensagens e suporte expandido a recursos daqui em diante.</span><span class="sxs-lookup"><span data-stu-id="e594a-112">The new AMQP-based API offers improved message passing reliability, performance and expanded feature support going forward.</span></span>
<span data-ttu-id="e594a-113">A nova API também oferece suporte para operações assíncronas (com base em asyncio) para enviar, receber e manusear com mensagens.</span><span class="sxs-lookup"><span data-stu-id="e594a-113">The new API also offers support for asynchronous operations (based on asyncio) for sending, receiving and handling messages.</span></span>

<span data-ttu-id="e594a-114">Para obter a documentação sobre as operações baseadas em HTTP herdadas, consulte [Usar operações baseadas em HTTP da API herdada](#using-http-based-operations-of-the-legacy-api).</span><span class="sxs-lookup"><span data-stu-id="e594a-114">For documentation on the legacy HTTP-based operations please see [Using HTTP-based operations of the legacy API](#using-http-based-operations-of-the-legacy-api).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e594a-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e594a-115">Prerequisites</span></span>

* <span data-ttu-id="e594a-116">Assinatura do Azure – [Criar uma conta gratuita](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="e594a-116">Azure subscription - [Create a free account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="e594a-117">[Credenciais de gerenciamento e namespace do Barramento de Serviço do Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span><span class="sxs-lookup"><span data-stu-id="e594a-117">Azure [Service Bus namespace and management credentials](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span></span>
* [<span data-ttu-id="e594a-118">Python 2.7-3.7</span><span class="sxs-lookup"><span data-stu-id="e594a-118">Python 2.7-3.7</span></span>](https://www.python.org/downloads/)


## <a name="installation"></a><span data-ttu-id="e594a-119">Instalação</span><span class="sxs-lookup"><span data-stu-id="e594a-119">Installation</span></span>
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a><span data-ttu-id="e594a-120">Conectar-se ao Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="e594a-120">Connect to Azure Service Bus</span></span>

### <a name="get-credentials"></a><span data-ttu-id="e594a-121">Obter credenciais</span><span class="sxs-lookup"><span data-stu-id="e594a-121">Get credentials</span></span>
<span data-ttu-id="e594a-122">Use o trecho da CLI do Azure a seguir para preencher uma variável de ambiente com a cadeia de conexão do Barramento de Serviço (você também encontra esse valor no portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="e594a-122">Use the Azure CLI snippet below to populate an environment variable with the Service Bus connection string (you can also find this value in the Azure portal).</span></span> <span data-ttu-id="e594a-123">O trecho é formatado para o shell do Bash.</span><span class="sxs-lookup"><span data-stu-id="e594a-123">The snippet is formatted for the Bash shell.</span></span>

```Bash
RES_GROUP=<resource-group-name>
NAMESPACE=<servicebus-namespace>

export SB_CONN_STR=$(az servicebus namespace authorization-rule keys list \
 --resource-group $RES_GROUP \
 --namespace-name $NAMESPACE \
 --name RootManageSharedAccessKey \
 --query primaryConnectionString \
 --output tsv)
```

### <a name="create-client"></a><span data-ttu-id="e594a-124">Criar cliente</span><span class="sxs-lookup"><span data-stu-id="e594a-124">Create client</span></span>
<span data-ttu-id="e594a-125">Depois de ter preenchido a variável de ambiente `SB_CONN_STR`, você pode criar o ServiceBusClient.</span><span class="sxs-lookup"><span data-stu-id="e594a-125">Once you've populated the `SB_CONN_STR` environment variable, you can create the ServiceBusClient.</span></span>
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
<span data-ttu-id="e594a-126">Caso queira usar as operações assíncronas, use o namespace `azure.servicebus.aio`.</span><span class="sxs-lookup"><span data-stu-id="e594a-126">If you wish to use asynchronous operations, please use the `azure.servicebus.aio` namespace.</span></span>
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a><span data-ttu-id="e594a-127">Filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e594a-127">Service Bus queues</span></span>
<span data-ttu-id="e594a-128">As Filas do Barramento de Serviço são uma alternativa às Filas de armazenamento que podem ser úteis em cenários em que são necessários recursos de mensagens mais avançados (tamanhos maiores de mensagem, classificação das mensagens, leituras destrutivas de única operação, entrega agendada) usando a entrega de estilo push (usando sondagem longa).</span><span class="sxs-lookup"><span data-stu-id="e594a-128">Service Bus queues are an alternative to Storage queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

### <a name="create-queue"></a><span data-ttu-id="e594a-129">Criar fila</span><span class="sxs-lookup"><span data-stu-id="e594a-129">Create queue</span></span>
<span data-ttu-id="e594a-130">Isso cria uma nova fila no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="e594a-130">This creates a new queue within the Service Bus namespace.</span></span> <span data-ttu-id="e594a-131">Se uma fila com o mesmo nome já existir dentro do namespace, um erro será gerado.</span><span class="sxs-lookup"><span data-stu-id="e594a-131">If a queue of the same name already exists within the namespace an error will be raised.</span></span> 
```python
sb_client.create_queue("MyQueue")
```
<span data-ttu-id="e594a-132">Também podem ser especificados parâmetros opcionais para configurar o comportamento de fila.</span><span class="sxs-lookup"><span data-stu-id="e594a-132">Optional parameters to configure the queue behaviour can also be specified.</span></span>
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a><span data-ttu-id="e594a-133">Obter um cliente de fila</span><span class="sxs-lookup"><span data-stu-id="e594a-133">Get a queue client</span></span>
<span data-ttu-id="e594a-134">Um QueueClient pode ser usado para enviar e receber mensagens da fila, juntamente com outras operações.</span><span class="sxs-lookup"><span data-stu-id="e594a-134">A QueueClient can be used to send and receive messages from the queue, along with other operations.</span></span>
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a><span data-ttu-id="e594a-135">Enviar mensagens</span><span class="sxs-lookup"><span data-stu-id="e594a-135">Sending messages</span></span>
<span data-ttu-id="e594a-136">O cliente de fila pode enviar uma ou mais mensagens por vez:</span><span class="sxs-lookup"><span data-stu-id="e594a-136">The queue client can send one or more messages at a time:</span></span>
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
<span data-ttu-id="e594a-137">Cada chamada para QueueClient.send criará uma nova conexão de serviço.</span><span class="sxs-lookup"><span data-stu-id="e594a-137">Each call to QueueClient.send will create a new service connection.</span></span> <span data-ttu-id="e594a-138">Para reutilizar a mesma conexão para várias chamadas de envio, você pode abrir um remetente:</span><span class="sxs-lookup"><span data-stu-id="e594a-138">To reuse the same connection for multiple send calls, you can open a sender:</span></span>
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
<span data-ttu-id="e594a-139">Se você estiver usando um cliente assíncrono, as operações acima usarão a sintaxe assíncrona:</span><span class="sxs-lookup"><span data-stu-id="e594a-139">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
from azure.servicebus.aio import Message

message = Message("Hello World")
await queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
async with queue_client.get_sender() as sender:
    await sender.send(message_one)
    await sender.send(message_two)
```


### <a name="receiving-messages"></a><span data-ttu-id="e594a-140">Recebendo mensagens</span><span class="sxs-lookup"><span data-stu-id="e594a-140">Receiving messages</span></span>
<span data-ttu-id="e594a-141">As mensagens podem ser recebidas de uma fila como um iterador contínuo.</span><span class="sxs-lookup"><span data-stu-id="e594a-141">Messages can be received from a queue as a continuous iterator.</span></span> <span data-ttu-id="e594a-142">O modo padrão para o recebimento de mensagem é [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), que requer que cada mensagem seja explicitamente concluída para que ela seja removida da fila.</span><span class="sxs-lookup"><span data-stu-id="e594a-142">The default mode for message receiving is [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), which requires each message to be explicitly completed in order that it be removed from the queue.</span></span>
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
<span data-ttu-id="e594a-143">A conexão de serviço permanecerá aberta para a totalidade do iterador.</span><span class="sxs-lookup"><span data-stu-id="e594a-143">The service connection will remain open for the entirety of the iterator.</span></span>
<span data-ttu-id="e594a-144">Caso você veja que está iterando o fluxo de mensagens apenas parcialmente, o receptor deve ser executado em uma instrução `with` para garantir que a conexão esteja fechada:</span><span class="sxs-lookup"><span data-stu-id="e594a-144">If you find yourself only partially iterating the message stream, you should run the receiver in a `with` statement to ensure the connection is closed:</span></span>
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
<span data-ttu-id="e594a-145">Se você estiver usando um cliente assíncrono, as operações acima usarão a sintaxe assíncrona:</span><span class="sxs-lookup"><span data-stu-id="e594a-145">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a><span data-ttu-id="e594a-146">Tópicos e assinaturas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e594a-146">Service Bus topics and subscriptions</span></span>

<span data-ttu-id="e594a-147">Os tópicos e as assinaturas do Barramento de Serviço são uma abstração sobre suas filas e fornecem uma forma de comunicação de um para muitos, em um padrão de publicação/assinatura.</span><span class="sxs-lookup"><span data-stu-id="e594a-147">Service Bus topics and subscriptions are an abstraction on top of Service Bus queues that provide a one-to-many form of communication, in a publish/subscribe pattern.</span></span> <span data-ttu-id="e594a-148">As mensagens são enviadas a um tópico e entregues a uma ou mais assinaturas associadas, o que é útil para o dimensionamento de uma grande quantidade de destinatários.</span><span class="sxs-lookup"><span data-stu-id="e594a-148">Messages are sent to a topic and delivered to one or more associated subscriptions, which is useful for scaling to large numbers of recipients.</span></span>

### <a name="create-topic"></a><span data-ttu-id="e594a-149">Criar tópico</span><span class="sxs-lookup"><span data-stu-id="e594a-149">Create topic</span></span>
<span data-ttu-id="e594a-150">Isso cria um novo tópico no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="e594a-150">This creates a new topic within the Service Bus namespace.</span></span> <span data-ttu-id="e594a-151">Se já houver um tópico de mesmo nome, um erro será gerado.</span><span class="sxs-lookup"><span data-stu-id="e594a-151">If a topic of the same name already exists an error will be raised.</span></span> 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a><span data-ttu-id="e594a-152">Obter um cliente de tópico</span><span class="sxs-lookup"><span data-stu-id="e594a-152">Get a topic client</span></span>
<span data-ttu-id="e594a-153">Um TopicClient pode ser usado para enviar mensagens ao tópico, juntamente com outras operações.</span><span class="sxs-lookup"><span data-stu-id="e594a-153">A TopicClient can be used to send messages to the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a><span data-ttu-id="e594a-154">Criar assinatura</span><span class="sxs-lookup"><span data-stu-id="e594a-154">Create subscription</span></span>
<span data-ttu-id="e594a-155">Isso cria uma nova assinatura para o tópico especificado dentro do namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="e594a-155">This creates a new subscription for the specified topic within the Service Bus namespace.</span></span>
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a><span data-ttu-id="e594a-156">Obter um cliente de assinatura</span><span class="sxs-lookup"><span data-stu-id="e594a-156">Get a subscription client</span></span>
<span data-ttu-id="e594a-157">Um SubscriptionClient pode ser usado para receber mensagens do tópico, juntamente com outras operações.</span><span class="sxs-lookup"><span data-stu-id="e594a-157">A SubscriptionClient can be used to receive messages from the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a><span data-ttu-id="e594a-158">Migração da v0.21.1 para v0.50.0</span><span class="sxs-lookup"><span data-stu-id="e594a-158">Migration from v0.21.1 to v0.50.0</span></span>
<span data-ttu-id="e594a-159">As principais alterações de falhas foram introduzidas na versão 0.50.0.</span><span class="sxs-lookup"><span data-stu-id="e594a-159">Major breaking changes were introduced in version 0.50.0.</span></span>
<span data-ttu-id="e594a-160">A API baseada em HTTP original ainda está disponível na v0.50.0, porém, agora ela existe em um novo namespace: `azure.servicebus.control_client`.</span><span class="sxs-lookup"><span data-stu-id="e594a-160">The original HTTP-based API is still available in v0.50.0 - however it now exists under a new namesapce: `azure.servicebus.control_client`.</span></span>

### <a name="should-i-upgrade"></a><span data-ttu-id="e594a-161">Devo atualizar?</span><span class="sxs-lookup"><span data-stu-id="e594a-161">Should I upgrade?</span></span>
<span data-ttu-id="e594a-162">O novo pacote (v0.50.0) não oferece nenhuma melhoria em operações baseadas em HTTP em relação à v0.21.1.</span><span class="sxs-lookup"><span data-stu-id="e594a-162">The new package (v0.50.0) offers no improvements in HTTP-based operations over v0.21.1.</span></span> <span data-ttu-id="e594a-163">A API baseada em HTTP é idêntica, com a diferença de que agora ela existe sob um novo namespace.</span><span class="sxs-lookup"><span data-stu-id="e594a-163">The HTTP-based API is identical except that it now exists under a new namespace.</span></span> <span data-ttu-id="e594a-164">Por esse motivo, se você quiser usar apenas operações baseadas em HTTP (`create_queue`, `delete_queue`, etc.), não há nenhum benefício adicional na atualização nesse momento.</span><span class="sxs-lookup"><span data-stu-id="e594a-164">For this reason if you only wish to use HTTP-based operations (`create_queue`, `delete_queue` etc) - there will be no additional benefit in upgrading at this time.</span></span>


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a><span data-ttu-id="e594a-165">Como fazer para migrar meu código para a nova versão?</span><span class="sxs-lookup"><span data-stu-id="e594a-165">How do I migrate my code to the new version?</span></span>
<span data-ttu-id="e594a-166">O código escrito com base na v0.21.0 pode ser portado para a versão 0.50.0 simplesmente alterando o namespace de importação:</span><span class="sxs-lookup"><span data-stu-id="e594a-166">Code written against v0.21.0 can be ported to version 0.50.0 by simply changing the import namespace:</span></span>

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a><span data-ttu-id="e594a-167">Usando operações baseadas em HTTP da API herdada</span><span class="sxs-lookup"><span data-stu-id="e594a-167">Using HTTP-based operations of the legacy API</span></span>
<span data-ttu-id="e594a-168">A documentação a seguir descreve a API herdada e deve ser usada por aqueles que quiserem transferir o código existente para a v0.50.0 sem fazer nenhuma alteração adicional.</span><span class="sxs-lookup"><span data-stu-id="e594a-168">The following documentation describes the legacy API and should be used for those wishing to port existing code to v0.50.0 without making any additional changes.</span></span> <span data-ttu-id="e594a-169">Essa referência também pode ser usada como uma orientação por aqueles que usam a v0.21.1.</span><span class="sxs-lookup"><span data-stu-id="e594a-169">This reference can also be used as guidance by those using v0.21.1.</span></span>
<span data-ttu-id="e594a-170">Para aqueles escrevendo um novo código, é recomendável usar a nova API descrita acima.</span><span class="sxs-lookup"><span data-stu-id="e594a-170">For those writing new code, we recommend using the new API described above.</span></span>

### <a name="service-bus-queues"></a><span data-ttu-id="e594a-171">Filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e594a-171">Service Bus queues</span></span>

#### <a name="shared-access-signature-sas-authentication"></a><span data-ttu-id="e594a-172">Autenticação da SAS (Assinatura de Acesso Compartilhado)</span><span class="sxs-lookup"><span data-stu-id="e594a-172">Shared Access Signature (SAS) authentication</span></span>

<span data-ttu-id="e594a-173">Para usar a autenticação de Assinatura de Acesso Compartilhado, crie o barramento de serviço com:</span><span class="sxs-lookup"><span data-stu-id="e594a-173">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a><span data-ttu-id="e594a-174">Autenticação do ACS (Serviço de Controle de Acesso)</span><span class="sxs-lookup"><span data-stu-id="e594a-174">Access Control Service (ACS) authentication</span></span>
<span data-ttu-id="e594a-175">Os novos namespaces do Barramento de Serviço não oferecem mais suporte ao ACS.</span><span class="sxs-lookup"><span data-stu-id="e594a-175">ACS is no longer supported on new Service Bus namespaces.</span></span> <span data-ttu-id="e594a-176">É recomendável [migrar aplicativos para a autenticação SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span><span class="sxs-lookup"><span data-stu-id="e594a-176">We recommend [migrating applications to SAS authentication](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span></span>
<span data-ttu-id="e594a-177">Para usar a autenticação ACS dentro de um namespace do Barramento de Serviço mais antigo, crie o ServiceBusService com:</span><span class="sxs-lookup"><span data-stu-id="e594a-177">To use ACS authentication within an older Service Bus namesapce, create the ServiceBusService with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a><span data-ttu-id="e594a-178">Enviar e receber mensagens</span><span class="sxs-lookup"><span data-stu-id="e594a-178">Sending and receiving messages</span></span>

<span data-ttu-id="e594a-179">O método **create\_queue** pode ser usado para garantir que exista uma fila:</span><span class="sxs-lookup"><span data-stu-id="e594a-179">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="e594a-180">O método **send\_queue\_message** pode, então, ser chamado para inserir a mensagem na fila:</span><span class="sxs-lookup"><span data-stu-id="e594a-180">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="e594a-181">O método **send\_queue\_message_batch** pode, então, ser chamado para enviar várias mensagens de uma vez:</span><span class="sxs-lookup"><span data-stu-id="e594a-181">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="e594a-182">Assim, é possível chamar o método **receive\_queue\_message** para remover a mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="e594a-182">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a><span data-ttu-id="e594a-183">Tópicos do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e594a-183">Service Bus topics</span></span>

<span data-ttu-id="e594a-184">O método **create\_topic** pode ser usado para criar um tópico no servidor:</span><span class="sxs-lookup"><span data-stu-id="e594a-184">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="e594a-185">O método **send\_topic\_message** pode ser usado para enviar uma mensagem para um tópico:</span><span class="sxs-lookup"><span data-stu-id="e594a-185">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="e594a-186">O método **send\_topic\_message_batch** pode ser usado para enviar várias mensagens de uma vez:</span><span class="sxs-lookup"><span data-stu-id="e594a-186">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="e594a-187">Leve em consideração que, no Python 3, uma mensagem str será codificada em utf-8 e você deve ter de gerenciar sua codificação por conta própria no Python 2.</span><span class="sxs-lookup"><span data-stu-id="e594a-187">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="e594a-188">Um cliente pode criar uma assinatura e começar a consumir mensagens chamando o método **create\_subscription** seguido do método **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="e594a-188">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="e594a-189">Observe que todas as mensagens enviadas antes da assinatura ser criada não serão recebidas.</span><span class="sxs-lookup"><span data-stu-id="e594a-189">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a><span data-ttu-id="e594a-190">Hub de evento</span><span class="sxs-lookup"><span data-stu-id="e594a-190">Event Hub</span></span>

<span data-ttu-id="e594a-191">Os Hubs de Eventos habilitam a coleção de fluxos de eventos com alta taxa de transferência em um conjunto diversificado de dispositivos e serviços.</span><span class="sxs-lookup"><span data-stu-id="e594a-191">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="e594a-192">O método **create\_event\_hub** pode ser usado para criar um hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="e594a-192">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="e594a-193">Para enviar um evento:</span><span class="sxs-lookup"><span data-stu-id="e594a-193">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="e594a-194">O conteúdo do evento é a mensagem de evento ou uma cadeia de caracteres codificada em JSON que contém várias mensagens.</span><span class="sxs-lookup"><span data-stu-id="e594a-194">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

### <a name="advanced-features"></a><span data-ttu-id="e594a-195">Recursos avançados</span><span class="sxs-lookup"><span data-stu-id="e594a-195">Advanced features</span></span>

#### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="e594a-196">Propriedades de agente e propriedades de usuário</span><span class="sxs-lookup"><span data-stu-id="e594a-196">Broker properties and user properties</span></span>

<span data-ttu-id="e594a-197">Esta seção descreve como usar as propriedades do Agente e do Usuário definidas [aqui](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="e594a-197">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
<span data-ttu-id="e594a-198">É possível usar datetime, int, float ou booleano</span><span class="sxs-lookup"><span data-stu-id="e594a-198">You can use datetime, int, float or boolean</span></span>

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
<span data-ttu-id="e594a-199">Por questões de compatibilidade com a versão antiga dessa biblioteca, `broker_properties` também pode ser definido como uma cadeia de caracteres JSON.</span><span class="sxs-lookup"><span data-stu-id="e594a-199">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="e594a-200">Se essa for a situação, você é o responsável por gravar uma cadeia de caracteres JSON válida, e nenhuma verificação será feita pelo Python antes do envio à API Rest.</span><span class="sxs-lookup"><span data-stu-id="e594a-200">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a><span data-ttu-id="e594a-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e594a-201">Next Steps</span></span>
* [<span data-ttu-id="e594a-202">documentação do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e594a-202">Service Bus documentation</span></span>](https://docs.microsoft.com/azure/service-bus-messaging)
* [<span data-ttu-id="e594a-203">Código-fonte do SDK</span><span class="sxs-lookup"><span data-stu-id="e594a-203">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="e594a-204">Documentação de referência do SDK</span><span class="sxs-lookup"><span data-stu-id="e594a-204">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [<span data-ttu-id="e594a-205">Amostras adicionais</span><span class="sxs-lookup"><span data-stu-id="e594a-205">Additional samples</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
