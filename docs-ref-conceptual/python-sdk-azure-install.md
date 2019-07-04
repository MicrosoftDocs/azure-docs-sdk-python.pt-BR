---
title: Instalação
description: Como instalar o SDK de Python do Azure
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 478118642122d7c0c80b1ddf37b13f71d8ca3adc
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534453"
---
# <a name="installation"></a><span data-ttu-id="1598d-104">Instalação</span><span class="sxs-lookup"><span data-stu-id="1598d-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="1598d-105">Qual Python e qual versão usar</span><span class="sxs-lookup"><span data-stu-id="1598d-105">Which Python and which version to use</span></span>

<span data-ttu-id="1598d-106">Existem vários interpretadores do Python disponíveis, entre eles:</span><span class="sxs-lookup"><span data-stu-id="1598d-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="1598d-107">CPython - o interpretador do Python padrão e mais geralmente usado</span><span class="sxs-lookup"><span data-stu-id="1598d-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="1598d-108">PyPy – implementação alternativa rápida e compatível para CPython</span><span class="sxs-lookup"><span data-stu-id="1598d-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="1598d-109">IronPython -interpretador do Python que é executado no .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="1598d-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="1598d-110">Jython – interpretador do Python que é executado na Máquina Virtual Java</span><span class="sxs-lookup"><span data-stu-id="1598d-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="1598d-111">O **CPython** v2.7 ou v3.4+ e o PyPy 5.4.0 são testados e têm suporte do SDK do Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="1598d-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="1598d-112">Onde obter o Python?</span><span class="sxs-lookup"><span data-stu-id="1598d-112">Where to get Python?</span></span>

<span data-ttu-id="1598d-113">Existem várias maneiras de obter o CPython:</span><span class="sxs-lookup"><span data-stu-id="1598d-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="1598d-114">Diretamente no [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="1598d-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="1598d-115">Em uma distribuição confiável, como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="1598d-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="1598d-116">Criá-lo a partir do código-fonte!</span><span class="sxs-lookup"><span data-stu-id="1598d-116">Build from source!</span></span>

<span data-ttu-id="1598d-117">A menos que você tenha uma necessidade específica, recomendamos as duas primeiras opções.</span><span class="sxs-lookup"><span data-stu-id="1598d-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="1598d-118">Instalação com PIP</span><span class="sxs-lookup"><span data-stu-id="1598d-118">Installation with pip</span></span>

<span data-ttu-id="1598d-119">Você pode instalar cada biblioteca de serviço do Azure individualmente:</span><span class="sxs-lookup"><span data-stu-id="1598d-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="1598d-120">Pacotes de preview podem ser instalados usando o sinalizador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="1598d-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="1598d-121">Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando o pacote meta `azure` .</span><span class="sxs-lookup"><span data-stu-id="1598d-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="1598d-122">Publicamos uma versão de visualização desse pacote, que pode ser acessada usando o sinalizador – pre:</span><span class="sxs-lookup"><span data-stu-id="1598d-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="1598d-123">Instalar a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="1598d-123">Install from GitHub</span></span>

<span data-ttu-id="1598d-124">Se você deseja instalar `azure` a partir da fonte:</span><span class="sxs-lookup"><span data-stu-id="1598d-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="1598d-125">Instalar uma versão mais antiga com o PIP</span><span class="sxs-lookup"><span data-stu-id="1598d-125">Install an older version with pip</span></span>
<span data-ttu-id="1598d-126">Você pode instalar uma versão mais antiga do `azure` especificando os detalhes de versão 'azure==3.0.0'.</span><span class="sxs-lookup"><span data-stu-id="1598d-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="1598d-127">Verifique os detalhes de instalação do SDK com o PIP</span><span class="sxs-lookup"><span data-stu-id="1598d-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="1598d-128">Você pode verificar o local de instalação, os detalhes de versão etc. do SDK do `azure`.</span><span class="sxs-lookup"><span data-stu-id="1598d-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="1598d-129">Para desinstalar com o PIP</span><span class="sxs-lookup"><span data-stu-id="1598d-129">To uninstall with pip</span></span>
<span data-ttu-id="1598d-130">Você pode desinstalar todas as bibliotecas do Azure em uma única linha usando o pacote meta `azure`.</span><span class="sxs-lookup"><span data-stu-id="1598d-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="1598d-131">O `pip uninstall azure` remove o pacote meta do `azure`, mas deixa os pacotes individuais do `azure-*` para trás (e outros, como o `adal` e o `msrest`).</span><span class="sxs-lookup"><span data-stu-id="1598d-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="1598d-132">Um aspecto do Python e do PIP é que para todos os pacotes que têm dependências, a desinstalação do pacote inicial não desinstala as dependências.</span><span class="sxs-lookup"><span data-stu-id="1598d-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="1598d-133">Para remover o `azure-` e seus pacotes de suporte, execute o comando `pip freeze | grep 'azure-' | xargs pip uninstall -y` (e, em seguida, realize desinstalações individuais para o adal, o msrest e o msrestazure).</span><span class="sxs-lookup"><span data-stu-id="1598d-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

