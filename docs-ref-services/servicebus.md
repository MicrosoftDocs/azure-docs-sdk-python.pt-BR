---
title: "Bibliotecas de Barramento de Serviço para Python"
description: "Documentação de referência para as bibliotecas de gerenciamento e de cliente de Python para Barramento de Serviço"
keywords: Azure, Python, SDK, API, sistema de mensagens, pubsub, pub-sub, agente de mensagens
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: bf7be945f2c7a3daea93ff4e5b770459c00632c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Barramento de Serviço para Python

## <a name="overview"></a>Visão geral

O Barramento de Serviço do Microsoft Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável. 

## <a name="install-the-libraries"></a>Instalar as bibliotecas
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a>Exemplo
Enviar mensagens a uma fila.

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/servicebus/managementlibrary)

