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
ms.openlocfilehash: d7be7cd76d019c6741d93c04458376a9352e363b
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="operation-config"></a><span data-ttu-id="29c27-104">Configuração de operação</span><span class="sxs-lookup"><span data-stu-id="29c27-104">Operation config</span></span> 

<span data-ttu-id="29c27-105">Os métodos em operações têm parâmetros adicionais que podem ser fornecidos no kwargs.</span><span class="sxs-lookup"><span data-stu-id="29c27-105">Methods on operations have extra parameters which can be provided in the kwargs.</span></span> <span data-ttu-id="29c27-106">Isso é chamado de operation_config.</span><span class="sxs-lookup"><span data-stu-id="29c27-106">This is called operation_config.</span></span>

<span data-ttu-id="29c27-107">As opções de configuração da operação são:</span><span class="sxs-lookup"><span data-stu-id="29c27-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="29c27-108">Nome do parâmetro</span><span class="sxs-lookup"><span data-stu-id="29c27-108">Parameter name</span></span>|<span data-ttu-id="29c27-109">type</span><span class="sxs-lookup"><span data-stu-id="29c27-109">Type</span></span>|<span data-ttu-id="29c27-110">Função</span><span class="sxs-lookup"><span data-stu-id="29c27-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="29c27-111">verificar</span><span class="sxs-lookup"><span data-stu-id="29c27-111">verify</span></span> |`bool`|<span data-ttu-id="29c27-112">Se deseja verificar o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="29c27-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="29c27-113">Padrão: True.</span><span class="sxs-lookup"><span data-stu-id="29c27-113">Default is True.</span></span>|
|  <span data-ttu-id="29c27-114">cert</span><span class="sxs-lookup"><span data-stu-id="29c27-114">cert</span></span> |`str`| <span data-ttu-id="29c27-115">Caminho até o certificado local para verificação do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="29c27-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="29c27-116">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="29c27-116">timeout</span></span> |`int`| <span data-ttu-id="29c27-117">Tempo limite para estabelecer uma conexão de servidor em segundos.</span><span class="sxs-lookup"><span data-stu-id="29c27-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="29c27-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="29c27-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="29c27-119">Se deseja permitir redirecionamentos.</span><span class="sxs-lookup"><span data-stu-id="29c27-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="29c27-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="29c27-120">max_redirects</span></span>  |`int`| <span data-ttu-id="29c27-121">O número máximo de redirecionamentos permitidos.</span><span class="sxs-lookup"><span data-stu-id="29c27-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="29c27-122">proxies</span><span class="sxs-lookup"><span data-stu-id="29c27-122">proxies</span></span>  |`dict` |<span data-ttu-id="29c27-123">Configurações do servidor de proxy.</span><span class="sxs-lookup"><span data-stu-id="29c27-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="29c27-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="29c27-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="29c27-125">Se deseja ler as configurações de proxy de variáveis de ambiente local.</span><span class="sxs-lookup"><span data-stu-id="29c27-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="29c27-126">retries</span><span class="sxs-lookup"><span data-stu-id="29c27-126">retries</span></span>  |`int` | <span data-ttu-id="29c27-127">O número total de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="29c27-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="29c27-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="29c27-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="29c27-129">Habilite logs de HTTP no modo de depuração (False por padrão).</span><span class="sxs-lookup"><span data-stu-id="29c27-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
