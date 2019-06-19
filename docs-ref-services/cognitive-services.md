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
ms.openlocfilehash: 5890c2091f8456dd9b8bcb68f8a34eed3cae6e04
ms.sourcegitcommit: d7ad0e8b4ba4add5e6f63e6b9eac54ecccdc7090
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148167"
---
# <a name="azure-cognitive-services-modules-for-python"></a>Módulos de Serviços Cognitivos do Azure para Python

Adicione imagem e reconhecimento de face, análise de idioma e pesquisa aos seus aplicativos Python, sites e ferramentas usando os módulos de Serviços Cognitivos do Azure para Python.

## <a name="vision-modules"></a>Módulos de visão

### <a name="computer-vision"></a>Visual Computacional 

Retorna informações sobre o conteúdo visual encontrado em uma imagem:

- Use marcação, descrições e modelos específicos do domínio para identificar o conteúdo e rotulá-lo com segurança.
- Aplique configurações de adulto/conteúdo sexual para habilitar restrições automáticas de conteúdo para adultos.
- Identifique os tipos de imagem e esquemas de cores em fotos.

[Experimente o Visual Computacional](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) gratuitamente em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-computervision
```

[Saiba mais](/azure/cognitive-services/computer-vision/home) sobre a API da Pesquisa Visual Computacional e comece a usar o [Início rápido do Python para API da Pesquisa Visual Computacional](/azure/cognitive-services/computer-vision/quickstarts/python).

### <a name="content-moderator"></a>Content Moderator

Moderação de texto, vídeo e imagens assistida por computador, aumentada com ferramentas de análise humana.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-contentmoderator
```

[Saiba mais](/azure/cognitive-services/content-moderator/overview) sobre o serviço Content Moderator.

### <a name="custom-vision-service"></a>Serviço de Visão Personalizada

Carregue imagens para treinar e personalizar um modelo de visão do computador para seu caso de uso específico. Depois do modelo ser treinado, você pode usar a API para imagens marcadas usando o modelo e avaliar os resultados para melhorar sua classificação.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-customvision
```

[Saiba mais](/azure/cognitive-services/Custom-Vision-Service/home) sobre o serviço de Visão Personalizada e comece a usar o [tutorial do Python para Visão Personalizada](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)

### <a name="face-api"></a>API de Detecção Facial

Detecte, identifique, analise, organize e marque rostos em fotos. 

[Experimente a API de Detecção Facial](https://azure.microsoft.com/en-us/services/cognitive-services/face/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install cognitive-face
```

[Saiba mais](/azure/cognitive-services/face/overview) sobre a API de Detecção Facial e comece a usar o [Início rápido do Python para API de Detecção Facial](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).

## <a name="search-modules"></a>Módulos de pesquisa

### <a name="web-search"></a>Pesquisa na Web

Recupere documentos da Web indexados pela API de Pesquisa na Web do Bing e restrinja os resultados por tipo de resultado, atualização e muito mais. 

[Experimente a API de Pesquisa na Web](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-websearch
```

[Saiba mais](/azure/cognitive-services/bing-web-search/overview) sobre a API de Pesquisa na Web do Bing e comece a usar o [Início rápido do Python para API de Pesquisa na Web](/azure/cognitive-services/bing-web-search/quickstarts/python).

### <a name="image-search"></a>Pesquisa de imagem

Pesquise imagens e obtenha miniaturas, URLs de imagem completa, metadados de imagem e muito mais em seus resultados.

[Experimente a API de Pesquisa de Imagem](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-imagesearch
```

[Saiba mais](/azure/cognitive-services/bing-image-search/overview) sobre a API de Pesquisa de Imagem do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Imagem](/azure/cognitive-services/bing-image-search/quickstarts/python).


### <a name="entity-search"></a>Pesquisa de entidade

Pesquise a entidade mais relevante (local, pessoa ou coisa) para determinado termo de pesquisa ou local.

[Experimente a API de Pesquisa de Entidade](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-entitysearch
```

[Saiba mais](/azure/cognitive-services/bing-entities-search/search-the-web) sobre a API de Pesquisa de Entidade do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Entidade](/azure/cognitive-services/bing-entities-search/quickstarts/python).

### <a name="custom-search"></a>Pesquisa personalizada

Compile e personalize uma pesquisa na Web que atenda a seu domínio de pesquisa específico.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-customsearch
```

[Saiba mais](/azure/cognitive-services/bing-custom-search/) sobre o serviço de Pesquisa Personalizada do Bing e comece a trabalhar com a consulta de sua pesquisa personalizada no Python com o [Início rápido do Python para API de Pesquisa Personalizada](/azure/cognitive-services/bing-custom-search/call-endpoint-python).

### <a name="video-search"></a>Pesquisa de vídeo

Encontre vídeos na Web, obtenha resultados com o criador, codificação, duração, e exiba os metadados de contagem.

[Experimente a API de Pesquisa de Vídeo](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-videosearch
```

[Saiba mais](/azure/cognitive-services/bing-video-search/search-the-web) sobre o serviço de Pesquisa de Vídeo do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Vídeo](/azure/cognitive-services/bing-video-search/python).


### <a name="news-search"></a>Pesquisa de notícias

Pesquise na Web artigos de notícias e trabalhe com o artigo, notícias relacionadas, imagens e metadados de informações do provedor.

[Experimente a API de Pesquisa de Notícias](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-newssearch
```

[Saiba mais](/azure/cognitive-services/bing-news-search/search-the-web) sobre o serviço de Pesquisa de Notícias do Bing e comece a usar o [Início rápido do Python para API de Pesquisa de Notícias](//azure/cognitive-services/bing-news-search/python).


## <a name="language-modules"></a>Módulos de linguagem

### <a name="text-analytics"></a>Análise de texto 

A API de Análise de Texto é um serviço baseado em nuvem que fornece processamento de texto natural em torno de texto bruto. A API inclui três funções principais:

- Análise de sentimento
- Extração de frases-chave
- Detecção de idioma

[Experimente a API de Análise de Texto](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-textanalytics
```

[Saiba mais](/azure/cognitive-services/text-analytics/overview) sobre a API de Análise de Texto e comece a usar o [Início rápido do Python para API de Análise de Texto](/azure/cognitive-services/text-analytics/quickstarts/python).


### <a name="spell-check"></a>Verificação ortográfica

Faça verificações da gramática contextual e ortográfica com a API de Verificação Ortográfica do Bing.

[Experimente a API de Verificação Ortográfica](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) em seu navegador.

Obtenha o módulo Python com [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-spellcheck
```

[Saiba mais](/azure/cognitive-services/bing-spell-check/proof-text) sobre a API de Verificação Ortográfica e comece a usar o [Início rápido do Python para API de Verificação Ortográfica](/azure/cognitive-services/bing-spell-check/quickstarts/python).
