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
ms.openlocfilehash: 8e8dd78cbc2d5887308361a47a9571ce242aee6e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-web-apps-libraries-for-python"></a>Bibliotecas de Aplicativos Web do Azure para Python

## <a name="overview"></a>Visão geral

Implantar e dimensionar sites, aplicativos Web, serviços e APIs REST com o [Serviço de Aplicativo do Azure](/azure/app-service).

Para começar a usar o Serviço de Aplicativo do Azure, consulte [Criar um aplicativo Web Python no Azure](/azure/app-service-web/app-service-web-get-started-python).

## <a name="management-api"></a>API de gerenciamento

Implantar, gerenciar e dimensionar elementos hospedados no Serviço de Aplicativo do Azure com a API de gerenciamento.

Instalar a biblioteca por meio de PIP.

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>Exemplo

Implantar um aplicativo Web de um repositório GitHub no Aplicativo Web do Azure.

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/webapps/management)

## <a name="samples"></a>Exemplos 

* [Gerenciar sites do Azure com Python][1]
* [Criar um fluxo de trabalho do Aplicativo Lógico][2]
 
Veja a [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) de exemplos de aplicativos Web.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md