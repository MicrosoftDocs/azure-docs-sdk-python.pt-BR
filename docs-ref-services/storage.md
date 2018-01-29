---
title: Bibliotecas do Armazenamento do Azure para Python
description: 
keywords: Azure, Python, SDK, API, Armazenamento
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: e00e821ff3e806a994fa8d96aae50c35eeeb8392
ms.sourcegitcommit: 5ab15a7214082d16f339a13e4ae7735b3a57a9aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="azure-storage-libraries-for-python"></a>Bibliotecas do Armazenamento do Azure para Python

## <a name="overview"></a>Visão geral
- Ler e gravar objetos e arquivos do [Armazenamento de Blobs do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)
- Enviar e receber mensagens entre aplicativos conectados à nuvem com o [Armazenamento de Filas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)
- Ler e gravar dados estruturados grandes com [Armazenamento de Tabelas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage) 
- Compartilhar o armazenamento entre aplicativos com [Armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)

Criar, atualizar e gerenciar contas de Armazenamento do Azure e consultar e regenerar chaves de acesso do seu código Python com as bibliotecas de gerenciamento.

## <a name="install-the-libraries"></a>Instalar as bibliotecas

### <a name="client"></a>Cliente

As Bibliotecas de Cliente de Armazenamento do Azure consistem em 4 pacotes: Blobs, Arquivos, Filas e Tabelas. Para instalar o pacote de blobs, exeucte:

```bash
pip install azure-storage-blob
```

### <a name="management"></a>Gerenciamento

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Exemplo
```python
blob_service = BlockBlobService(account_name, account_key)

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="samples"></a>Exemplos

| | |
|--|--|
| [Introdução ao Armazenamento de Blobs do Azure no Python](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | Criar, ler, atualizar, restringir o acesso e excluir arquivos e objetos no Armazenamento do Azure. |
| [Introdução ao Armazenamento de Filas do Azure no Python](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | Inserir, inspecionar, recuperar e excluir mensagens das filas do Armazenamento do Azure. | 
| [Gerenciar contas de Armazenamento do Azure](https://azure.microsoft.com/resources/samples/storage-python-manage) | Criar, atualizar e excluir contas de armazenamento. Recuperar e regenerar chaves de acesso da conta de armazenamento.

Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos.
