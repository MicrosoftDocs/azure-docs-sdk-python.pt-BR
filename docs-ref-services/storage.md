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
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="0e085-103">Bibliotecas do Armazenamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="0e085-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="0e085-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0e085-104">Overview</span></span>
- <span data-ttu-id="0e085-105">Ler e gravar objetos e arquivos do [Armazenamento de Blobs do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span><span class="sxs-lookup"><span data-stu-id="0e085-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="0e085-106">Enviar e receber mensagens entre aplicativos conectados à nuvem com [Armazenamento de Filas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span><span class="sxs-lookup"><span data-stu-id="0e085-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="0e085-107">Ler e gravar dados estruturados grandes com [Armazenamento de Tabelas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span><span class="sxs-lookup"><span data-stu-id="0e085-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="0e085-108">Compartilhar o armazenamento entre aplicativos com [Armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span><span class="sxs-lookup"><span data-stu-id="0e085-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="0e085-109">Criar, atualizar e gerenciar contas de Armazenamento do Azure e consultar e regenerar chaves de acesso do seu código Python com as bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0e085-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="0e085-110">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="0e085-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="0e085-111">Cliente</span><span class="sxs-lookup"><span data-stu-id="0e085-111">Client</span></span>

```bash
pip install azure-storage
```

### <a name="management"></a><span data-ttu-id="0e085-112">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0e085-112">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="0e085-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0e085-113">Example</span></span>
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

## <a name="samples"></a><span data-ttu-id="0e085-114">Exemplos</span><span class="sxs-lookup"><span data-stu-id="0e085-114">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="0e085-115">Introdução ao Armazenamento de Blobs do Azure no Python</span><span class="sxs-lookup"><span data-stu-id="0e085-115">Get started with Azure Blob Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | <span data-ttu-id="0e085-116">Criar, ler, atualizar, restringir o acesso e excluir arquivos e objetos no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e085-116">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="0e085-117">Introdução ao Armazenamento de Filas do Azure no Python</span><span class="sxs-lookup"><span data-stu-id="0e085-117">Get started with Azure Queue Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | <span data-ttu-id="0e085-118">Inserir, inspecionar, recuperar e excluir mensagens das filas do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e085-118">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="0e085-119">Gerenciar contas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0e085-119">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="0e085-120">Criar, atualizar e excluir contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0e085-120">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="0e085-121">Recuperar e regenerar chaves de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0e085-121">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="0e085-122">Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="0e085-122">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>