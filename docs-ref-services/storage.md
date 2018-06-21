---
title: Bibliotecas do Armazenamento do Azure para Python
description: ''
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
ms.openlocfilehash: e45b12af9e026e0f6390556813385d86784feaa4
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720057"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="6625e-103">Bibliotecas do Armazenamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="6625e-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="6625e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6625e-104">Overview</span></span>
- <span data-ttu-id="6625e-105">Ler e gravar objetos e arquivos do [Armazenamento de Blobs do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span><span class="sxs-lookup"><span data-stu-id="6625e-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="6625e-106">Enviar e receber mensagens entre aplicativos conectados à nuvem com o [Armazenamento de Filas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span><span class="sxs-lookup"><span data-stu-id="6625e-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="6625e-107">Ler e gravar dados estruturados grandes com [Armazenamento de Tabelas do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span><span class="sxs-lookup"><span data-stu-id="6625e-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="6625e-108">Compartilhar o armazenamento entre aplicativos com [Armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span><span class="sxs-lookup"><span data-stu-id="6625e-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="6625e-109">Criar, atualizar e gerenciar contas de Armazenamento do Azure e consultar e regenerar chaves de acesso do seu código Python com as bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="6625e-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="6625e-110">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="6625e-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="6625e-111">Cliente</span><span class="sxs-lookup"><span data-stu-id="6625e-111">Client</span></span>

<span data-ttu-id="6625e-112">As Bibliotecas de Cliente de Armazenamento do Azure consistem em 4 pacotes: Blobs, Arquivos, Filas e Tabelas.</span><span class="sxs-lookup"><span data-stu-id="6625e-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="6625e-113">Para instalar o pacote de blobs, exeucte:</span><span class="sxs-lookup"><span data-stu-id="6625e-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="6625e-114">Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6625e-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="6625e-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6625e-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

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

## <a name="samples"></a><span data-ttu-id="6625e-116">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6625e-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="6625e-117">Introdução ao Armazenamento de Blobs do Azure no Python</span><span class="sxs-lookup"><span data-stu-id="6625e-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="6625e-118">Criar, ler, atualizar, restringir o acesso e excluir arquivos e objetos no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6625e-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="6625e-119">Introdução ao Armazenamento de Filas do Azure no Python</span><span class="sxs-lookup"><span data-stu-id="6625e-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="6625e-120">Inserir, inspecionar, recuperar e excluir mensagens das filas do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6625e-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="6625e-121">Gerenciar contas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6625e-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="6625e-122">Criar, atualizar e excluir contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6625e-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="6625e-123">Recuperar e regenerar chaves de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6625e-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="6625e-124">Explore mais [exemplos de código de Python](https://azure.microsoft.com/resources/samples/?platform=python) que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6625e-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
