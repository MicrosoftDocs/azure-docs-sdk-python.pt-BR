---
title: Bibliotecas de Recursos do Azure para Python
description: 
keywords: Azure, Python, SDK, API, Recursos
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: 32e13bee27db091f0bca12c7d9ae4fc62165f4c0
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="ffae2-103">Bibliotecas de Recursos do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="ffae2-103">Azure Resources libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="ffae2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ffae2-104">Overview</span></span> 
<span data-ttu-id="ffae2-105">Gerenciar recursos do Azure nos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ffae2-105">Manage Azure resources in resource groups.</span></span>

| <span data-ttu-id="ffae2-106">Pacote</span><span class="sxs-lookup"><span data-stu-id="ffae2-106">Package</span></span>  |  <span data-ttu-id="ffae2-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffae2-107">Description</span></span> |
|---|---|
|<span data-ttu-id="ffae2-108">[azure.mgmt.resource.features][1]</span><span class="sxs-lookup"><span data-stu-id="ffae2-108">[azure.mgmt.resource.features][1]</span></span>|<span data-ttu-id="ffae2-109">O Controle de Exposição de Recurso do Azure (AFEC) fornece um mecanismo para os provedores de recursos controlar a exposição de recurso aos usuários.</span><span class="sxs-lookup"><span data-stu-id="ffae2-109">Azure Feature Exposure Control (AFEC) provides a mechanism for the resource providers to control feature exposure to users.</span></span>|
|<span data-ttu-id="ffae2-110">[azure.mgmt.resource.links][2]</span><span class="sxs-lookup"><span data-stu-id="ffae2-110">[azure.mgmt.resource.links][2]</span></span>|<span data-ttu-id="ffae2-111">Os recursos do Azure podem ser vinculados para formarem a relações lógicas.</span><span class="sxs-lookup"><span data-stu-id="ffae2-111">Azure resources can be linked together to form logical relationships.</span></span> <span data-ttu-id="ffae2-112">Você pode estabelecer links entre recursos que pertencem a grupos de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ffae2-112">You can establish links between resources belonging to different resource groups.</span></span>|
|<span data-ttu-id="ffae2-113">[azure.mgmt.resource.locks][3]</span><span class="sxs-lookup"><span data-stu-id="ffae2-113">[azure.mgmt.resource.locks][3]</span></span>|<span data-ttu-id="ffae2-114">Os recursos do Azure podem ser bloqueados para impedir que outros usuários na sua organização excluam ou modifiquem os recursos.</span><span class="sxs-lookup"><span data-stu-id="ffae2-114">Azure resources can be locked to prevent other users in your organization from deleting or modifying resources.</span></span>|
|<span data-ttu-id="ffae2-115">[azure.mgmt.resource.managedapplications][4]</span><span class="sxs-lookup"><span data-stu-id="ffae2-115">[azure.mgmt.resource.managedapplications][4]</span></span>|<span data-ttu-id="ffae2-116">Aplicativos gerenciados de ARM (dispositivos).</span><span class="sxs-lookup"><span data-stu-id="ffae2-116">ARM managed applications (appliances).</span></span>|
|<span data-ttu-id="ffae2-117">[azure.mgmt.resource.policy][5]</span><span class="sxs-lookup"><span data-stu-id="ffae2-117">[azure.mgmt.resource.policy][5]</span></span>|<span data-ttu-id="ffae2-118">Para gerenciar e controlar o acesso aos recursos, você pode definir políticas personalizadas e atribuí-las a um escopo.</span><span class="sxs-lookup"><span data-stu-id="ffae2-118">To manage and control access to your resources, you can define customized policies and assign them at a scope.</span></span>|
|<span data-ttu-id="ffae2-119">[azure.mgmt.resource.resources][6]</span><span class="sxs-lookup"><span data-stu-id="ffae2-119">[azure.mgmt.resource.resources][6]</span></span>| <span data-ttu-id="ffae2-120">Fornece operações para trabalhar com recursos e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ffae2-120">Provides operations for working with resources and resource groups.</span></span>|
|<span data-ttu-id="ffae2-121">[azure.mgmt.resource.subscriptions][7]</span><span class="sxs-lookup"><span data-stu-id="ffae2-121">[azure.mgmt.resource.subscriptions][7]</span></span>|<span data-ttu-id="ffae2-122">Todos os grupos de recursos e recursos existem em assinaturas.</span><span class="sxs-lookup"><span data-stu-id="ffae2-122">All resource groups and resources exist within subscriptions.</span></span> <span data-ttu-id="ffae2-123">Essa operação permite obter informações sobre suas assinaturas e locatários.</span><span class="sxs-lookup"><span data-stu-id="ffae2-123">These operation enable you get information about your subscriptions and tenants.</span></span>|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a><span data-ttu-id="ffae2-124">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="ffae2-124">Install the libraries</span></span> 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="ffae2-125">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ffae2-125">Example</span></span>
<span data-ttu-id="ffae2-126">Abaixo está um exemplo de como criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ffae2-126">The following is an example of how to create a resource group.</span></span> 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

<span data-ttu-id="ffae2-127">Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ffae2-127">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span> 