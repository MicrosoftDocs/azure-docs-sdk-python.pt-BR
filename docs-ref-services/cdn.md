---
title: Bibliotecas da CDN do Azure para Python
description: Referência para bibliotecas da CDN do Azure para Python
keywords: Azure, Python, SDK, API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 2dd7703e94a814d85716a7b96994666e32f95565
ms.sourcegitcommit: 3db75daa592da90ea9aa8fd17fb99627a30eb4fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66179875"
---
# <a name="azure-cdn-libraries-for-python"></a>Bibliotecas da CDN do Azure para Python

## <a name="overview"></a>Visão geral

A [Rede de Distribuição de Conteúdo do Azure (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) permite que você forneça caches de conteúdo da Web para garantir uma disponibilidade de alta largura de banda em todo o mundo.

Para começar a usar a CDN do Azure, consulte [Introdução à CDN do Azure](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).

## <a name="management-apis"></a>APIs de gerenciamento

Criar, consultar e gerenciar as CDNs do Azure com a API de gerenciamento.

Instalar o pacote de gerenciamento com PIP.

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a>Exemplo

Criar um perfil de CDN com um único ponto de extremidade definido:

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = cdn_client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/cdn/management)
