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
ms.openlocfilehash: 64465964d32934a6a45dec44cb92a0a8a84b9c37
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-libraries-for-python"></a>Bibliotecas do Armazenamento do Azure para Python

## <a name="overview"></a>Visão geral
- Ler e gravar objetos e arquivos do [Armazenamento de Blobs do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)
- Enviar e receber mensagens entre aplicativos conectados à nuvem com [Armazenamento de Filas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)
- Ler e gravar dados estruturados grandes com [Armazenamento de Tabelas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage) 
- Compartilhar o armazenamento entre aplicativos com [Armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)

Criar, atualizar e gerenciar contas de Armazenamento do Azure e consultar e regenerar chaves de acesso do seu código Python com as bibliotecas de gerenciamento.

## <a name="install-the-libraries"></a>Instalar as bibliotecas

### <a name="client"></a>Cliente

```bash
pip install azure-storage
```

### <a name="management"></a>Gerenciamento

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Exemplo
```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

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
| [Introdução ao Armazenamento de Blobs do Azure no Python](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | Criar, ler, atualizar, restringir o acesso e excluir arquivos e objetos no Armazenamento do Azure. |
| [Introdução ao Armazenamento de Filas do Azure no Python](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | Inserir, inspecionar, recuperar e excluir mensagens das filas do Armazenamento do Azure. | 
| [Gerenciar contas de Armazenamento do Azure](https://azure.microsoft.com/resources/samples/storage-python-manage) | Criar, atualizar e excluir contas de armazenamento. Recuperar e regenerar chaves de acesso da conta de armazenamento.

Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos.