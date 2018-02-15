---
title: "Instalação"
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
ms.openlocfilehash: 5ce4ef27667d45697200eef67be92c62812b3809
ms.sourcegitcommit: 66e112df9be660354e23955b0adf3efd784ba739
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="installation"></a><span data-ttu-id="42d67-104">Instalação</span><span class="sxs-lookup"><span data-stu-id="42d67-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="42d67-105">Instalação com PIP</span><span class="sxs-lookup"><span data-stu-id="42d67-105">Installation with pip</span></span>

<span data-ttu-id="42d67-106">Você pode instalar cada biblioteca de serviço do Azure individualmente:</span><span class="sxs-lookup"><span data-stu-id="42d67-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="42d67-107">Pacotes de preview podem ser instalados usando o sinalizador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="42d67-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="42d67-108">Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando o pacote meta `azure` .</span><span class="sxs-lookup"><span data-stu-id="42d67-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="42d67-109">Publicamos uma versão de visualização desse pacote, que pode ser acessada usando o sinalizador – pre:</span><span class="sxs-lookup"><span data-stu-id="42d67-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="42d67-110">Instalar a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="42d67-110">Install from GitHub</span></span>

<span data-ttu-id="42d67-111">Se você deseja instalar `azure` a partir da fonte:</span><span class="sxs-lookup"><span data-stu-id="42d67-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
