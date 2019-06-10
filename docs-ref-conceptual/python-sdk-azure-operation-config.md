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
# <a name="operation-config"></a><span data-ttu-id="3b0a0-104">Configuração de operação</span><span class="sxs-lookup"><span data-stu-id="3b0a0-104">Operation config</span></span> 

<span data-ttu-id="3b0a0-105">Os métodos em operações têm parâmetros adicionais que podem ser fornecidos no `kwargs`.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-105">Methods on operations have extra parameters which can be provided in the `kwargs`.</span></span> <span data-ttu-id="3b0a0-106">Isso é chamado de operation_config.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-106">This is called operation_config.</span></span>

<span data-ttu-id="3b0a0-107">As opções de configuração da operação são:</span><span class="sxs-lookup"><span data-stu-id="3b0a0-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="3b0a0-108">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="3b0a0-108">Parameter name</span></span>|<span data-ttu-id="3b0a0-109">Type</span><span class="sxs-lookup"><span data-stu-id="3b0a0-109">Type</span></span>|<span data-ttu-id="3b0a0-110">Função</span><span class="sxs-lookup"><span data-stu-id="3b0a0-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="3b0a0-111">verificar</span><span class="sxs-lookup"><span data-stu-id="3b0a0-111">verify</span></span> |`bool`|<span data-ttu-id="3b0a0-112">Se deseja verificar o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="3b0a0-113">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-113">Default is True.</span></span>|
|  <span data-ttu-id="3b0a0-114">cert</span><span class="sxs-lookup"><span data-stu-id="3b0a0-114">cert</span></span> |`str`| <span data-ttu-id="3b0a0-115">Caminho até o certificado local para verificação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="3b0a0-116">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="3b0a0-116">timeout</span></span> |`int`| <span data-ttu-id="3b0a0-117">Tempo limite para estabelecer uma conexão de servidor em segundos.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="3b0a0-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="3b0a0-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="3b0a0-119">Se deseja permitir redirecionamentos.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="3b0a0-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="3b0a0-120">max_redirects</span></span>  |`int`| <span data-ttu-id="3b0a0-121">O número máximo de redirecionamentos permitidos.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="3b0a0-122">proxies</span><span class="sxs-lookup"><span data-stu-id="3b0a0-122">proxies</span></span>  |`dict` |<span data-ttu-id="3b0a0-123">Configurações do servidor de proxy.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="3b0a0-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="3b0a0-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="3b0a0-125">Se deseja ler as configurações de proxy de variáveis de ambiente local.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="3b0a0-126">retries</span><span class="sxs-lookup"><span data-stu-id="3b0a0-126">retries</span></span>  |`int` | <span data-ttu-id="3b0a0-127">O número total de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="3b0a0-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="3b0a0-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="3b0a0-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="3b0a0-129">Habilite logs de HTTP no modo de depuração (False por padrão).</span><span class="sxs-lookup"><span data-stu-id="3b0a0-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
