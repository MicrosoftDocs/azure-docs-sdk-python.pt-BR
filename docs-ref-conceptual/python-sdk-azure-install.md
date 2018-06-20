---
title: Instalação
description: Como instalar o SDK de Python do Azure
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 792feac12f8328e2467017530065350e347c59b7
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
ms.locfileid: "29565815"
---
# <a name="installation"></a><span data-ttu-id="97713-104">Instalação</span><span class="sxs-lookup"><span data-stu-id="97713-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="97713-105">Qual Python e qual versão usar</span><span class="sxs-lookup"><span data-stu-id="97713-105">Which Python and which version to use</span></span>
<span data-ttu-id="97713-106">Existem vários interpretadores do Python disponíveis, entre eles:</span><span class="sxs-lookup"><span data-stu-id="97713-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="97713-107">CPython - o interpretador do Python padrão e mais geralmente usado</span><span class="sxs-lookup"><span data-stu-id="97713-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="97713-108">PyPy – implementação alternativa rápida e compatível para CPython</span><span class="sxs-lookup"><span data-stu-id="97713-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="97713-109">IronPython -interpretador do Python que é executado no .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="97713-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="97713-110">Jython – interpretador do Python que é executado na Máquina Virtual Java</span><span class="sxs-lookup"><span data-stu-id="97713-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="97713-111">O **CPython** v2.7 ou v3.4+ e o PyPy 5.4.0 são testados e têm suporte do SDK do Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="97713-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="97713-112">Onde obter o Python?</span><span class="sxs-lookup"><span data-stu-id="97713-112">Where to get Python?</span></span>
<span data-ttu-id="97713-113">Existem várias maneiras de obter o CPython:</span><span class="sxs-lookup"><span data-stu-id="97713-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="97713-114">Diretamente no [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="97713-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="97713-115">Em uma distribuição confiável, como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="97713-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="97713-116">Criá-lo a partir do código-fonte!</span><span class="sxs-lookup"><span data-stu-id="97713-116">Build from source!</span></span>

<span data-ttu-id="97713-117">A menos que você tenha uma necessidade específica, recomendamos as duas primeiras opções.</span><span class="sxs-lookup"><span data-stu-id="97713-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="97713-118">Instalação com PIP</span><span class="sxs-lookup"><span data-stu-id="97713-118">Installation with pip</span></span>

<span data-ttu-id="97713-119">Você pode instalar cada biblioteca de serviço do Azure individualmente:</span><span class="sxs-lookup"><span data-stu-id="97713-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="97713-120">Pacotes de preview podem ser instalados usando o sinalizador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="97713-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="97713-121">Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando o pacote meta `azure` .</span><span class="sxs-lookup"><span data-stu-id="97713-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="97713-122">Publicamos uma versão de visualização desse pacote, que pode ser acessada usando o sinalizador – pre:</span><span class="sxs-lookup"><span data-stu-id="97713-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="97713-123">Instalar a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="97713-123">Install from GitHub</span></span>

<span data-ttu-id="97713-124">Se você deseja instalar `azure` a partir da fonte:</span><span class="sxs-lookup"><span data-stu-id="97713-124">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install