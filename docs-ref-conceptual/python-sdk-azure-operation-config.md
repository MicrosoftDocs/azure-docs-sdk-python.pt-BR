---
title: SDK do Azure para configuração de operações do Python
description: C gerado pelo SDK do Azure para Python
keywords: Azure, Python, SDK, API, exceções
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 03/07/2018
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: adeb6aa8a2c363c3119e97503df9536fb0633b4c
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376871"
---
# <a name="operation-config"></a>Configuração de operação 

Os métodos em operações têm parâmetros adicionais que podem ser fornecidos no `kwargs`. Isso é chamado de operation_config.

As opções de configuração da operação são:

|Nome do parâmetro|Type|Função|
|----------------------|------|---------------|
| verificar |`bool`|Se deseja verificar o certificado SSL. Padrão: True.|
|  cert |`str`| Caminho até o certificado local para verificação do lado do cliente.|
|  Tempo limite |`int`| Tempo limite para estabelecer uma conexão de servidor em segundos.|
|  allow_redirects |`bool` | Se deseja permitir redirecionamentos.|
|  max_redirects  |`int`| O número máximo de redirecionamentos permitidos.|
|  proxies  |`dict` |Configurações do servidor de proxy.|
|  use_env_proxies |`bool` |Se deseja ler as configurações de proxy de variáveis de ambiente local.|
|  retries  |`int` | O número total de novas tentativas.|
|  enable_http_logger | `bool`| Habilite logs de HTTP no modo de depuração (False por padrão).|
