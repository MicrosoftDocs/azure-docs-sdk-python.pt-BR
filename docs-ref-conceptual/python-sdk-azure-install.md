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
ms.openlocfilehash: 6014937fb41d6074e94578ccc47c30eb7b3f63d2
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376874"
---
# <a name="installation"></a>Instalação

## <a name="which-python-and-which-version-to-use"></a>Qual Python e qual versão usar

Existem vários interpretadores do Python disponíveis, entre eles:

* CPython - o interpretador do Python padrão e mais geralmente usado
* PyPy – implementação alternativa rápida e compatível para CPython
* IronPython -interpretador do Python que é executado no .Net/CLR
* Jython – interpretador do Python que é executado na Máquina Virtual Java

O **CPython** v2.7 ou v3.4+ e o PyPy 5.4.0 são testados e têm suporte do SDK do Azure para Python.

## <a name="where-to-get-python"></a>Onde obter o Python?

Existem várias maneiras de obter o CPython:

* Diretamente no [Python](https://www.python.org/)
* Em uma distribuição confiável, como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)
* Criá-lo a partir do código-fonte!

A menos que você tenha uma necessidade específica, recomendamos as duas primeiras opções.

## <a name="installation-with-pip"></a>Instalação com PIP

Você pode instalar cada biblioteca de serviço do Azure individualmente:

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

Pacotes de preview podem ser instalados usando o sinalizador `--pre` :

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando o pacote meta `azure` .

```bash
pip install azure
```

Publicamos uma versão de visualização desse pacote, que pode ser acessada usando o sinalizador – pre:

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Instalar a partir do GitHub

Se você deseja instalar `azure` a partir da fonte:

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```
