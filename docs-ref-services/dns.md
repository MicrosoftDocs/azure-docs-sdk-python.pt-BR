---
title: Bibliotecas de DNS do Azure para Python
description: "Referência para bibliotecas de DNS do Azure para Python"
keywords: Azure, Python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a>Bibliotecas de DNS do Azure para Python

## <a name="overview"></a>Visão geral

O [DNS do Azure](/azure/dns/dns-overview) é um serviço de hospedagem para domínios DNS que fornece resolução de DNS usando a infraestrutura do Azure.

Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando o portal do Azure](/azure/dns/dns-getstarted-portal).

## <a name="management-apis"></a>APIs de gerenciamento

Criar e gerenciar zonas DNS e registros com a API de gerenciamento.

Instalar o pacote de gerenciamento com PIP.

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a>Exemplo

Criar uma nova zona DNS.

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/dns/managementlibrary)
