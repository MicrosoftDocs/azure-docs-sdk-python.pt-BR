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
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Barramento de Serviço para Python

O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável.

* [Código-fonte do SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Documentação de referência do SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a>Quais as novidades na v0.50.0?
A partir da versão 0.50.0, uma nova API baseada em AMQP está disponível para enviar e receber mensagens. Essa atualização envolve **alterações de falhas**.
Leia a [Migração da v0.21.1 para v0.50.0](#migration-from-v0211-to-v0500) para determinar se a atualização é ideal para você no momento.

A nova API baseada em AMQP oferece desempenho e confiabilidade de transmissão de mensagens e suporte expandido a recursos daqui em diante.
A nova API também oferece suporte para operações assíncronas (com base em asyncio) para enviar, receber e manusear com mensagens.

Para obter a documentação sobre as operações baseadas em HTTP herdadas, consulte [Usar operações baseadas em HTTP da API herdada](#using-http-based-operations-of-the-legacy-api).


## <a name="prerequisites"></a>Pré-requisitos

* Assinatura do Azure – [Criar uma conta gratuita](https://azure.microsoft.com/free/)
* [Credenciais de gerenciamento e namespace do Barramento de Serviço do Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)
* [Python 2.7-3.7](https://www.python.org/downloads/)


## <a name="installation"></a>Instalação
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a>Conectar-se ao Barramento de Serviço do Azure

### <a name="get-credentials"></a>Obter credenciais
Use o trecho da CLI do Azure a seguir para preencher uma variável de ambiente com a cadeia de conexão do Barramento de Serviço (você também encontra esse valor no portal do Azure). O trecho é formatado para o shell do Bash.

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

### <a name="create-client"></a>Criar cliente
Depois de ter preenchido a variável de ambiente `SB_CONN_STR`, você pode criar o ServiceBusClient.
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
Caso queira usar as operações assíncronas, use o namespace `azure.servicebus.aio`.
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a>Filas do Barramento de Serviço
As Filas do Barramento de Serviço são uma alternativa às Filas de armazenamento que podem ser úteis em cenários em que são necessários recursos de mensagens mais avançados (tamanhos maiores de mensagem, classificação das mensagens, leituras destrutivas de única operação, entrega agendada) usando a entrega de estilo push (usando sondagem longa).

### <a name="create-queue"></a>Criar fila
Isso cria uma nova fila no namespace do Barramento de Serviço. Se uma fila com o mesmo nome já existir dentro do namespace, um erro será gerado. 
```python
sb_client.create_queue("MyQueue")
```
Também podem ser especificados parâmetros opcionais para configurar o comportamento de fila.
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a>Obter um cliente de fila
Um QueueClient pode ser usado para enviar e receber mensagens da fila, juntamente com outras operações.
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a>Enviar mensagens
O cliente de fila pode enviar uma ou mais mensagens por vez:
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
Cada chamada para QueueClient.send criará uma nova conexão de serviço. Para reutilizar a mesma conexão para várias chamadas de envio, você pode abrir um remetente:
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
Se você estiver usando um cliente assíncrono, as operações acima usarão a sintaxe assíncrona:
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


### <a name="receiving-messages"></a>Recebendo mensagens
As mensagens podem ser recebidas de uma fila como um iterador contínuo. O modo padrão para o recebimento de mensagem é [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), que requer que cada mensagem seja explicitamente concluída para que ela seja removida da fila.
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
A conexão de serviço permanecerá aberta para a totalidade do iterador.
Caso você veja que está iterando o fluxo de mensagens apenas parcialmente, o receptor deve ser executado em uma instrução `with` para garantir que a conexão esteja fechada:
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
Se você estiver usando um cliente assíncrono, as operações acima usarão a sintaxe assíncrona:
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a>Tópicos e assinaturas do Barramento de Serviço

Os tópicos e as assinaturas do Barramento de Serviço são uma abstração sobre suas filas e fornecem uma forma de comunicação de um para muitos, em um padrão de publicação/assinatura. As mensagens são enviadas a um tópico e entregues a uma ou mais assinaturas associadas, o que é útil para o dimensionamento de uma grande quantidade de destinatários.

### <a name="create-topic"></a>Criar tópico
Isso cria um novo tópico no namespace do Barramento de Serviço. Se já houver um tópico de mesmo nome, um erro será gerado. 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a>Obter um cliente de tópico
Um TopicClient pode ser usado para enviar mensagens ao tópico, juntamente com outras operações.
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a>Criar assinatura
Isso cria uma nova assinatura para o tópico especificado dentro do namespace do Barramento de Serviço.
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a>Obter um cliente de assinatura
Um SubscriptionClient pode ser usado para receber mensagens do tópico, juntamente com outras operações.
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a>Migração da v0.21.1 para v0.50.0
As principais alterações de falhas foram introduzidas na versão 0.50.0.
A API baseada em HTTP original ainda está disponível na v0.50.0, porém, agora ela existe em um novo namespace: `azure.servicebus.control_client`.

### <a name="should-i-upgrade"></a>Devo atualizar?
O novo pacote (v0.50.0) não oferece nenhuma melhoria em operações baseadas em HTTP em relação à v0.21.1. A API baseada em HTTP é idêntica, com a diferença de que agora ela existe sob um novo namespace. Por esse motivo, se você quiser usar apenas operações baseadas em HTTP (`create_queue`, `delete_queue`, etc.), não há nenhum benefício adicional na atualização nesse momento.


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a>Como fazer para migrar meu código para a nova versão?
O código escrito com base na v0.21.0 pode ser portado para a versão 0.50.0 simplesmente alterando o namespace de importação:

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a>Usando operações baseadas em HTTP da API herdada
A documentação a seguir descreve a API herdada e deve ser usada por aqueles que quiserem transferir o código existente para a v0.50.0 sem fazer nenhuma alteração adicional. Essa referência também pode ser usada como uma orientação por aqueles que usam a v0.21.1.
Para aqueles escrevendo um novo código, é recomendável usar a nova API descrita acima.

### <a name="service-bus-queues"></a>Filas do Barramento de Serviço

#### <a name="shared-access-signature-sas-authentication"></a>Autenticação da SAS (Assinatura de Acesso Compartilhado)

Para usar a autenticação de Assinatura de Acesso Compartilhado, crie o barramento de serviço com:

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a>Autenticação do ACS (Serviço de Controle de Acesso)
Os novos namespaces do Barramento de Serviço não oferecem mais suporte ao ACS. É recomendável [migrar aplicativos para a autenticação SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).
Para usar a autenticação ACS dentro de um namespace do Barramento de Serviço mais antigo, crie o ServiceBusService com:

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a>Enviar e receber mensagens

O método **create\_queue** pode ser usado para garantir que exista uma fila:

```python
sbs.create_queue('taskqueue')
```
O método **send\_queue\_message** pode, então, ser chamado para inserir a mensagem na fila:

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
O método **send\_queue\_message_batch** pode, então, ser chamado para enviar várias mensagens de uma vez:

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
Assim, é possível chamar o método **receive\_queue\_message** para remover a mensagem da fila.

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a>Tópicos do Barramento de Serviço

O método **create\_topic** pode ser usado para criar um tópico no servidor:

```python
sbs.create_topic('taskdiscussion')
```
O método **send\_topic\_message** pode ser usado para enviar uma mensagem para um tópico:

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

O método **send\_topic\_message_batch** pode ser usado para enviar várias mensagens de uma vez:

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Leve em consideração que, no Python 3, uma mensagem str será codificada em utf-8 e você deve ter de gerenciar sua codificação por conta própria no Python 2.

Um cliente pode criar uma assinatura e começar a consumir mensagens chamando o método **create\_subscription** seguido do método **receive\_subscription\_message**. Observe que todas as mensagens enviadas antes da assinatura ser criada não serão recebidas.

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a>Hub de evento

Os Hubs de Eventos habilitam a coleção de fluxos de eventos com alta taxa de transferência em um conjunto diversificado de dispositivos e serviços.

O método **create\_event\_hub** pode ser usado para criar um hub de eventos:

```python
sbs.create_event_hub('myhub')
```
Para enviar um evento:

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
O conteúdo do evento é a mensagem de evento ou uma cadeia de caracteres codificada em JSON que contém várias mensagens.

### <a name="advanced-features"></a>Recursos avançados

#### <a name="broker-properties-and-user-properties"></a>Propriedades de agente e propriedades de usuário

Esta seção descreve como usar as propriedades do Agente e do Usuário definidas [aqui](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
É possível usar datetime, int, float ou booleano

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
Por questões de compatibilidade com a versão antiga dessa biblioteca, `broker_properties` também pode ser definido como uma cadeia de caracteres JSON.
Se essa for a situação, você é o responsável por gravar uma cadeia de caracteres JSON válida, e nenhuma verificação será feita pelo Python antes do envio à API Rest.

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a>Próximas etapas
* [documentação do Barramento de Serviço](https://docs.microsoft.com/azure/service-bus-messaging)
* [Código-fonte do SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Documentação de referência do SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [Amostras adicionais](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
