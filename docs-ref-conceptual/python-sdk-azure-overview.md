---
title: Bibliotecas do Azure para Python
description: "Visão geral das bibliotecas de serviço e gerenciamento do Azure para Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: e0c7b4acd1aa57d141f4407c0ba483a1529d2b35
ms.sourcegitcommit: 97e5d660eb4a006f969c3010087e1386cc6eb482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2018
---
# <a name="azure-libraries-for-python"></a><span data-ttu-id="bc789-104">Bibliotecas do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="bc789-104">Azure libraries for Python</span></span>

<span data-ttu-id="bc789-105">As bibliotecas do Azure para Python permitem que você use serviços do Azure e gerencie recursos do Azure no código do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bc789-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="bc789-106">Gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="bc789-106">Manage Azure resources</span></span>

<span data-ttu-id="bc789-107">Criar e gerenciar recursos do Azure a partir de aplicativos Python usando as bibliotecas do Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="bc789-107">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="bc789-108">Por exemplo, para criar uma instância do SQL Server, você pode usar o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc789-108">For example, to create a SQL Server instance, you can use the following code:</span></span>

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

<span data-ttu-id="bc789-109">Analise as [instruções de instalação](/azure/python-how-to-install) para obter uma lista completa das bibliotecas e como importá-las para seus projetos e, em seguida, leia o [artigo de introdução](python-sdk-azure-get-started.yml) para configurar a autenticação e executar o código de exemplo em relação a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc789-109">Review the [install instructions](/azure/python-how-to-install) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="bc789-110">Conectar-se aos serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="bc789-110">Connect to Azure services</span></span>

<span data-ttu-id="bc789-111">Além de usar bibliotecas de Python para criar e gerenciar recursos no Azure, você também pode usar bibliotecas de Python para se conectar e usar esses recursos em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bc789-111">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="bc789-112">Por exemplo, você pode atualizar um Banco de Dados SQL de tabela ou armazenar arquivos no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc789-112">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="bc789-113">Selecione a biblioteca necessária para um serviço específico a partir da lista completa das bibliotecas e visite a central de desenvolvedores de Python para ver os tutoriais e exemplos de código e obter ajuda para usá-las em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bc789-113">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="bc789-114">Por exemplo, para carregar uma página HTML simples em um blob e obter a URL:</span><span class="sxs-lookup"><span data-stu-id="bc789-114">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="bc789-115">Referência e código de exemplo</span><span class="sxs-lookup"><span data-stu-id="bc789-115">Sample code and reference</span></span>
<span data-ttu-id="bc789-116">Os exemplos a seguir abordam tarefas comuns de automação com as bibliotecas de gerenciamento do Azure para Python e possuem códigos prontos para uso em seus próprios aplicativos:</span><span class="sxs-lookup"><span data-stu-id="bc789-116">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="bc789-117">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="bc789-117">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="bc789-118">Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="bc789-118">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="bc789-119">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="bc789-119">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="bc789-120">Uma [referência](/python/api/overview/azure) está disponível para todos os pacotes nas bibliotecas de serviço e de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bc789-120">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="bc789-121">Novos recursos, alterações significativas, e instruções de migração de versões anteriores estão disponíveis nas [notas de versão](python-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="bc789-121">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="bc789-122">Obter ajuda e fazer comentários</span><span class="sxs-lookup"><span data-stu-id="bc789-122">Get help and give feedback</span></span>

<span data-ttu-id="bc789-123">Poste perguntas para a comunidade no [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) e divulgue problemas com o SDK no [GitHub do projeto](https://github.com/Azure/azure-sdk-for-python).</span><span class="sxs-lookup"><span data-stu-id="bc789-123">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
