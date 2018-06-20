---
title: Bibliotecas de Aplicativos Web do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, aplicativos Web, Serviço de Aplicativo
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 8e8dd78cbc2d5887308361a47a9571ce242aee6e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479219"
---
# <a name="azure-web-apps-libraries-for-python"></a><span data-ttu-id="eb4c8-103">Bibliotecas de Aplicativos Web do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="eb4c8-103">Azure Web Apps libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="eb4c8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="eb4c8-104">Overview</span></span>

<span data-ttu-id="eb4c8-105">Implantar e dimensionar sites, aplicativos Web, serviços e APIs REST com o [Serviço de Aplicativo do Azure](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="eb4c8-105">Deploy and scale websites, web applications, services, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="eb4c8-106">Para começar a usar o Serviço de Aplicativo do Azure, consulte [Criar um aplicativo Web Python no Azure](/azure/app-service-web/app-service-web-get-started-python).</span><span class="sxs-lookup"><span data-stu-id="eb4c8-106">To get started with Azure App Service, see [Create a Python web app in Azure](/azure/app-service-web/app-service-web-get-started-python).</span></span>

## <a name="management-api"></a><span data-ttu-id="eb4c8-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="eb4c8-107">Management API</span></span>

<span data-ttu-id="eb4c8-108">Implantar, gerenciar e dimensionar elementos hospedados no Serviço de Aplicativo do Azure com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="eb4c8-108">Deploy, manage, and scale elements hosted in the Azure App Service with the management API.</span></span>

<span data-ttu-id="eb4c8-109">Instalar a biblioteca por meio de PIP.</span><span class="sxs-lookup"><span data-stu-id="eb4c8-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-web
```

### <a name="example"></a><span data-ttu-id="eb4c8-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="eb4c8-110">Example</span></span>

<span data-ttu-id="eb4c8-111">Implantar um aplicativo Web de um repositório GitHub no Aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb4c8-111">Deploy a webapp from a GitHub repository into Azure Web App.</span></span>

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="eb4c8-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="eb4c8-112">Explore the Management APIs</span></span>](/python/api/overview/azure/webapps/management)

## <a name="samples"></a><span data-ttu-id="eb4c8-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="eb4c8-113">Samples</span></span> 

* <span data-ttu-id="eb4c8-114">[Gerenciar sites do Azure com Python][1]</span><span class="sxs-lookup"><span data-stu-id="eb4c8-114">[Manage Azure websites with python][1]</span></span>
* <span data-ttu-id="eb4c8-115">[Criar um fluxo de trabalho do Aplicativo Lógico][2]</span><span class="sxs-lookup"><span data-stu-id="eb4c8-115">[Create a Logic App workflow][2]</span></span>
 
<span data-ttu-id="eb4c8-116">Veja a [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) de exemplos de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="eb4c8-116">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) of web application samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md