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
ms.openlocfilehash: 92d6dd6ce55964bc48bb9bc654e8dec25f6b8344
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478879"
---
# <a name="azure-cdn-libraries-for-python"></a><span data-ttu-id="93559-104">Bibliotecas da CDN do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="93559-104">Azure CDN libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="93559-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="93559-105">Overview</span></span>

<span data-ttu-id="93559-106">A [Rede de Distribuição de Conteúdo do Azure (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) permite que você forneça caches de conteúdo da Web para garantir uma disponibilidade de alta largura de banda em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="93559-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) allows you to provide web content caches to ensure high-bandwidth availability across the globe.</span></span>

<span data-ttu-id="93559-107">Para começar a usar a CDN do Azure, consulte [Introdução à CDN do Azure](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="93559-107">To get started with Azure CDN, see [Getting started with Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-apis"></a><span data-ttu-id="93559-108">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="93559-108">Management APIs</span></span>

<span data-ttu-id="93559-109">Criar, consultar e gerenciar as CDNs do Azure com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="93559-109">Create, query, and manage Azure CDNs with the management API.</span></span>

<span data-ttu-id="93559-110">Instalar o pacote de gerenciamento com PIP.</span><span class="sxs-lookup"><span data-stu-id="93559-110">Install the management package via pip.</span></span>

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a><span data-ttu-id="93559-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="93559-111">Example</span></span>

<span data-ttu-id="93559-112">Criar um perfil de CDN com um único ponto de extremidade definido:</span><span class="sxs-lookup"><span data-stu-id="93559-112">Creating a CDN profile with a single defined endpoint:</span></span>

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

endpoint_poller = client.endpoints.create('my-resource-group',
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
> [<span data-ttu-id="93559-113">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="93559-113">Explore the Management APIs</span></span>](/python/api/overview/azure/cdn/management)
