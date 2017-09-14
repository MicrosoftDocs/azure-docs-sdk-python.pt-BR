---
title: Bibliotecas de Aplicativos Web do Azure para Python
description: 
keywords: "Azure, Python, SDK, API, aplicativos Web, Serviço de Aplicativo"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 05f6ad173f4ec051654b5eb2a986b2c2a93cc33a
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-web-apps-libraries-for-python"></a><span data-ttu-id="60389-103">Bibliotecas de Aplicativos Web do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="60389-103">Azure Web Apps libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="60389-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="60389-104">Overview</span></span>

<span data-ttu-id="60389-105">Implantar e dimensionar sites, aplicativos Web, serviços e APIs REST com o [Serviço de Aplicativo do Azure](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="60389-105">Deploy and scale websites, web applications, services, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="60389-106">Para começar a usar o Serviço de Aplicativo do Azure, consulte [Criar um aplicativo Web Python no Azure](/azure/app-service-web/app-service-web-get-started-python).</span><span class="sxs-lookup"><span data-stu-id="60389-106">To get started with Azure App Service, see [Create a Python web app in Azure](/azure/app-service-web/app-service-web-get-started-python).</span></span>

## <a name="management-api"></a><span data-ttu-id="60389-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="60389-107">Management API</span></span>

<span data-ttu-id="60389-108">Implantar, gerenciar e dimensionar elementos hospedados no Serviço de Aplicativo do Azure com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="60389-108">Deploy, manage, and scale elements hosted in the Azure App Service with the management API.</span></span>

<span data-ttu-id="60389-109">Instalar a biblioteca por meio de PIP.</span><span class="sxs-lookup"><span data-stu-id="60389-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-web
```

### <a name="example"></a><span data-ttu-id="60389-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="60389-110">Example</span></span>

<span data-ttu-id="60389-111">Implantar um aplicativo Web de um repositório GitHub no Aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="60389-111">Deploy a webapp from a GitHub repository into Azure Web App.</span></span>

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
> [<span data-ttu-id="60389-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="60389-112">Explore the Management APIs</span></span>](/python/api/overview/azure/webapps/managementlibrary)

## <a name="samples"></a><span data-ttu-id="60389-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="60389-113">Samples</span></span> 

* <span data-ttu-id="60389-114">[Gerenciar sites do Azure com Python][1]</span><span class="sxs-lookup"><span data-stu-id="60389-114">[Manage Azure websites with python][1]</span></span>
* <span data-ttu-id="60389-115">[Criar um fluxo de trabalho do Aplicativo Lógico][2]</span><span class="sxs-lookup"><span data-stu-id="60389-115">[Create a Logic App workflow][2]</span></span>
 
<span data-ttu-id="60389-116">Veja a [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) de exemplos de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="60389-116">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) of web application samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md