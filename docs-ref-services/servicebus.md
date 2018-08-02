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
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Barramento de Serviço para Python

## <a name="overview"></a>Visão geral

O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável. 

## <a name="install-the-libraries"></a>Instalar as bibliotecas
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a>Filas do ServiceBus
As Filas do ServiceBus são uma alternativa às Filas de Armazenamento que possam ser úteis em cenários em que são necessários recursos de mensagens mais avançados (tamanhos maiores de mensagem, classificação das mensagens, leituras destrutivas de única operação, entrega agendada) usando a entrega de estilo push (usando sondagem longa).

O serviço pode usar a autenticação de Assinatura de Acesso Compartilhado ou autenticação de ACS.

Os namespaces de barramento de serviço criados usando o portal do Azure depois de agosto de 2014 não oferecem mais suporte à autenticação de ACS. É possível criar namespaces compatíveis do ACS com o SDK do Azure.

### <a name="shared-access-signature-authentication"></a>Autenticação de Assinatura de Acesso Compartilhado

Para usar a autenticação de Assinatura de Acesso Compartilhado, crie o barramento de serviço com:

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a>Autenticação de ACS

Para usar a autenticação de ACS, crie o serviço do barramento de serviço com:

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a>Como enviar e receber mensagens

O método **create\_queue** pode ser usado para garantir que exista uma fila:

```python
sbs.create_queue('taskqueue')
```
O método **send\_queue\_message** pode, então, ser chamado para inserir a mensagem na fila:

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
O método **send\_queue\_message_batch** pode, então, ser chamado para enviar várias mensagens de uma vez:

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
Assim, é possível chamar o método **receive\_queue\_message** para remover a mensagem da fila.

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a>Tópicos do ServiceBus

Os tópicos do ServiceBus são uma abstração sobre as Filas do ServiceBus, que tornam os cenários de publicação/assinatura fáceis de implementar.

O método **create\_topic** pode ser usado para criar um tópico no servidor:

```python
sbs.create_topic('taskdiscussion')
```
O método **send\_topic\_message** pode ser usado para enviar uma mensagem para um tópico:

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

O método **send\_topic\_message_batch** pode ser usado para enviar várias mensagens de uma vez:

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Leve em consideração que, no Python 3, uma mensagem str será codificada em utf-8 e você deve ter de gerenciar sua codificação por conta própria no Python 2.

Um cliente pode criar uma assinatura e começar a consumir mensagens chamando o método **create\_subscription** seguido do método **receive\_subscription\_message**. Observe que todas as mensagens enviadas antes da assinatura ser criada não serão recebidas.

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a>Hub de evento

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

## <a name="advanced-features"></a>Recursos avançados

### <a name="broker-properties-and-user-properties"></a>Propriedades do agente e propriedades de usuário

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

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/servicebus/management)
