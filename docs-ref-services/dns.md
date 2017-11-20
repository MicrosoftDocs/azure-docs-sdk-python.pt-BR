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
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="d3886-104">Bibliotecas de DNS do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="d3886-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="d3886-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d3886-105">Overview</span></span>

<span data-ttu-id="d3886-106">O [DNS do Azure](/azure/dns/dns-overview) é um serviço de hospedagem para domínios DNS que fornece resolução de DNS usando a infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d3886-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="d3886-107">Para começar a usar o DNS do Azure, consulte [Introdução ao DNS do Azure usando o portal do Azure](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="d3886-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="d3886-108">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="d3886-108">Management APIs</span></span>

<span data-ttu-id="d3886-109">Criar e gerenciar zonas DNS e registros com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="d3886-109">Create and manage DNS zones and records with the management API.</span></span>

<span data-ttu-id="d3886-110">Instalar o pacote de gerenciamento com PIP.</span><span class="sxs-lookup"><span data-stu-id="d3886-110">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a><span data-ttu-id="d3886-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d3886-111">Example</span></span>

<span data-ttu-id="d3886-112">Criar uma nova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="d3886-112">Create a new DNS zone.</span></span>

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
> [<span data-ttu-id="d3886-113">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="d3886-113">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/managementlibrary)
