---
title: Módulos de Serviços Cognitivos do Azure para Python
description: Referência dos módulos de Serviços Cognitivos do Azure para Python
keywords: Azure, Python, SDK, API, Serviços Cognitivos
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 1f1dbaa77ee02a1da9386642e001f0a1a63a6599
ms.sourcegitcommit: 61cc12fd4bb1a3ad5f9b79d1c616f005bc21c5d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30849767"
---
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="ee587-104">Módulos de Serviços Cognitivos do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="ee587-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="ee587-105">Adicione imagem e reconhecimento de face, análise de idioma e pesquisa aos seus aplicativos Python, sites e ferramentas usando os módulos de Serviços Cognitivos do Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="ee587-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="ee587-106">Módulos de visão</span><span class="sxs-lookup"><span data-stu-id="ee587-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="ee587-107">Visual Computacional</span><span class="sxs-lookup"><span data-stu-id="ee587-107">Computer Vision</span></span> 

<span data-ttu-id="ee587-108">Retorna informações sobre o conteúdo visual encontrado em uma imagem:</span><span class="sxs-lookup"><span data-stu-id="ee587-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="ee587-109">Use marcação, descrições e modelos específicos do domínio para identificar o conteúdo e rotulá-lo com segurança.</span><span class="sxs-lookup"><span data-stu-id="ee587-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="ee587-110">Aplique configurações de adulto/conteúdo sexual para habilitar restrições automáticas de conteúdo para adultos.</span><span class="sxs-lookup"><span data-stu-id="ee587-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="ee587-111">Identifique os tipos de imagem e esquemas de cores em fotos.</span><span class="sxs-lookup"><span data-stu-id="ee587-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="ee587-112">[Experimente o Visual Computacional](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) gratuitamente em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="ee587-113">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="ee587-114">[Saiba mais](/azure/cognitive-services/computer-vision/home) sobre a API da Pesquisa Visual Computacional e comece a usar o [Início rápido do Python para API da Pesquisa Visual Computacional](/azure/cognitive-services/computer-vision/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="ee587-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="ee587-115">Content Moderator</span></span>

<span data-ttu-id="ee587-116">Moderação de texto, vídeo e imagens assistida por computador, aumentada com ferramentas de análise humana.</span><span class="sxs-lookup"><span data-stu-id="ee587-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="ee587-117">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="ee587-118">[Saiba mais](/azure/cognitive-services/content-moderator/overview) sobre o serviço Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="ee587-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="ee587-119">Serviço de Visão Personalizada</span><span class="sxs-lookup"><span data-stu-id="ee587-119">Custom Vision Service</span></span>

<span data-ttu-id="ee587-120">Carregue imagens para treinar e personalizar um modelo de visão do computador para seu caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="ee587-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="ee587-121">Depois do modelo ser treinado, você pode usar a API para imagens marcadas usando o modelo e avaliar os resultados para melhorar sua classificação.</span><span class="sxs-lookup"><span data-stu-id="ee587-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="ee587-122">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="ee587-123">[Saiba mais](/azure/cognitive-services/Custom-Vision-Service/home) sobre o serviço de Visão Personalizada e comece a usar o [tutorial do Python para Visão Personalizada](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span><span class="sxs-lookup"><span data-stu-id="ee587-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="ee587-124">API de Detecção Facial</span><span class="sxs-lookup"><span data-stu-id="ee587-124">Face API</span></span>

<span data-ttu-id="ee587-125">Detecte, identifique, analise, organize e marque rostos em fotos.</span><span class="sxs-lookup"><span data-stu-id="ee587-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="ee587-126">[Experimente a API de Detecção Facial](https://azure.microsoft.com/en-us/services/cognitive-services/face/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="ee587-127">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install cognitive-face
```

<span data-ttu-id="ee587-128">[Saiba mais](/azure/cognitive-services/face/overview) sobre a API de Detecção Facial e comece a usar o [Início rápido do Python para API de Detecção Facial](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span><span class="sxs-lookup"><span data-stu-id="ee587-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="ee587-129">Módulos de pesquisa</span><span class="sxs-lookup"><span data-stu-id="ee587-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="ee587-130">Pesquisa na Web</span><span class="sxs-lookup"><span data-stu-id="ee587-130">Web search</span></span>

<span data-ttu-id="ee587-131">Recupere documentos da Web indexados pela API de Pesquisa na Web do Bing e restrinja os resultados por tipo de resultado, atualização e muito mais.</span><span class="sxs-lookup"><span data-stu-id="ee587-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="ee587-132">[Experimente a API de Pesquisa na Web](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="ee587-133">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="ee587-134">[Saiba mais](/azure/cognitive-services/bing-web-search/overview) sobre a API de Pesquisa na Web do Bing e comece a usar o [Início rápido do Python para API de Pesquisa na Web](/azure/cognitive-services/bing-web-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="ee587-135">Pesquisa de imagem</span><span class="sxs-lookup"><span data-stu-id="ee587-135">Image search</span></span>

<span data-ttu-id="ee587-136">Pesquise imagens e obtenha miniaturas, URLs de imagem completa, metadados de imagem e muito mais em seus resultados.</span><span class="sxs-lookup"><span data-stu-id="ee587-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="ee587-137">[Experimente a API de Pesquisa de Imagem](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="ee587-138">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="ee587-139">[Saiba mais](/azure/cognitive-services/bing-image-search/overview) sobre a API de Pesquisa de Imagem do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Imagem](/azure/cognitive-services/bing-image-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="ee587-140">Pesquisa de entidade</span><span class="sxs-lookup"><span data-stu-id="ee587-140">Entity search</span></span>

<span data-ttu-id="ee587-141">Pesquise a entidade mais relevante (local, pessoa ou coisa) para determinado termo de pesquisa ou local.</span><span class="sxs-lookup"><span data-stu-id="ee587-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="ee587-142">[Experimente a API de Pesquisa de Entidade](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="ee587-143">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="ee587-144">[Saiba mais](/azure/cognitive-services/bing-entities-search/search-the-web) sobre a API de Pesquisa de Entidade do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Entidade](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="ee587-145">Pesquisa personalizada</span><span class="sxs-lookup"><span data-stu-id="ee587-145">Custom search</span></span>

<span data-ttu-id="ee587-146">Compile e personalize uma pesquisa na Web que atenda a seu domínio de pesquisa específico.</span><span class="sxs-lookup"><span data-stu-id="ee587-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="ee587-147">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="ee587-148">[Saiba mais](/azure/cognitive-services/bing-custom-search/) sobre o serviço de Pesquisa Personalizada do Bing e comece a trabalhar com a consulta de sua pesquisa personalizada no Python com o [Início rápido do Python para API de Pesquisa Personalizada](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span><span class="sxs-lookup"><span data-stu-id="ee587-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="ee587-149">Pesquisa de vídeo</span><span class="sxs-lookup"><span data-stu-id="ee587-149">Video search</span></span>

<span data-ttu-id="ee587-150">Encontre vídeos na Web, obtenha resultados com o criador, codificação, duração, e exiba os metadados de contagem.</span><span class="sxs-lookup"><span data-stu-id="ee587-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="ee587-151">[Experimente a API de Pesquisa de Vídeo](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="ee587-152">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="ee587-153">[Saiba mais](/azure/cognitive-services/bing-video-search/search-the-web) sobre o serviço de Pesquisa de Vídeo do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Vídeo](/azure/cognitive-services/bing-video-search/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="ee587-154">Pesquisa de notícias</span><span class="sxs-lookup"><span data-stu-id="ee587-154">News search</span></span>

<span data-ttu-id="ee587-155">Pesquise na Web artigos de notícias e trabalhe com o artigo, notícias relacionadas, imagens e metadados de informações do provedor.</span><span class="sxs-lookup"><span data-stu-id="ee587-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="ee587-156">[Experimente a API de Pesquisa de Notícias](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="ee587-157">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="ee587-158">[Saiba mais](/azure/cognitive-services/bing-news-search/search-the-web) sobre o serviço de Pesquisa de Notícias do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Notícias](//azure/cognitive-services/bing-news-search/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](//azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="ee587-159">Módulos de linguagem</span><span class="sxs-lookup"><span data-stu-id="ee587-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="ee587-160">Análise de texto</span><span class="sxs-lookup"><span data-stu-id="ee587-160">Text Analytics</span></span> 

<span data-ttu-id="ee587-161">A API de Análise de Texto é um serviço baseado em nuvem que fornece processamento de texto natural em torno de texto bruto.</span><span class="sxs-lookup"><span data-stu-id="ee587-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="ee587-162">A API inclui três funções principais:</span><span class="sxs-lookup"><span data-stu-id="ee587-162">The API includes three main functions:</span></span>

- <span data-ttu-id="ee587-163">Análise de sentimento</span><span class="sxs-lookup"><span data-stu-id="ee587-163">Sentiment analysis</span></span>
- <span data-ttu-id="ee587-164">Extração de frases-chave</span><span class="sxs-lookup"><span data-stu-id="ee587-164">Key phrase extraction</span></span>
- <span data-ttu-id="ee587-165">Detecção de idioma</span><span class="sxs-lookup"><span data-stu-id="ee587-165">Language detection</span></span>

<span data-ttu-id="ee587-166">[Experimente a API de Análise de Texto](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="ee587-167">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="ee587-168">[Saiba mais](/azure/cognitive-services/text-analytics/overview) sobre a API de Análise de Texto e comece a usar o [Início rápido do Python para API de Análise de Texto](/azure/cognitive-services/text-analytics/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="ee587-169">Verificação ortográfica</span><span class="sxs-lookup"><span data-stu-id="ee587-169">Spell Check</span></span>

<span data-ttu-id="ee587-170">Faça verificações da gramática contextual e ortográfica com a API de Verificação Ortográfica do Bing.</span><span class="sxs-lookup"><span data-stu-id="ee587-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="ee587-171">[Experimente a API de Verificação Ortográfica](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="ee587-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="ee587-172">Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="ee587-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="ee587-173">[Saiba mais](/azure/cognitive-services/bing-spell-check/proof-text) sobre a API de Verificação Ortográfica e comece a usar o [Início rápido do Python para API de Verificação Ortográfica](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="ee587-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>