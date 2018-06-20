---
title: Bibliotecas do Azure para Python
description: Visão geral das bibliotecas de serviço e gerenciamento do Azure para Python
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: ''
ms.openlocfilehash: 2b3e6d31edd7b946664853b3478e22205ab8c92e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478799"
---
# <a name="azure-libraries-for-python"></a>Bibliotecas do Azure para Python

As bibliotecas do Azure para Python permitem que você use serviços do Azure e gerencie recursos do Azure no código do seu aplicativo. 

## <a name="manage-azure-resources"></a>Gerenciar recursos do Azure

Criar e gerenciar recursos do Azure a partir de aplicativos Python usando as bibliotecas do Azure para Python.

Por exemplo, para criar uma instância do SQL Server, você pode usar o código a seguir:

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

Analise as [instruções de instalação](python-sdk-azure-install.md) para obter uma lista completa das bibliotecas e como importá-las para seus projetos e, em seguida, leia o [artigo de introdução](python-sdk-azure-get-started.yml) para configurar a autenticação e executar o código de exemplo em relação a sua assinatura do Azure.

## <a name="connect-to-azure-services"></a>Conectar-se aos serviços do Azure

Além de usar bibliotecas de Python para criar e gerenciar recursos no Azure, você também pode usar bibliotecas de Python para se conectar e usar esses recursos em seus aplicativos. Por exemplo, você pode atualizar um Banco de Dados SQL de tabela ou armazenar arquivos no Armazenamento do Azure. Selecione a biblioteca necessária para um serviço específico a partir da lista completa das bibliotecas e visite a central de desenvolvedores de Python para ver os tutoriais e exemplos de código e obter ajuda para usá-las em seus aplicativos.

Por exemplo, para carregar uma página HTML simples em um blob e obter a URL:

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

## <a name="sample-code-and-reference"></a>Referência e código de exemplo
Os exemplos a seguir abordam tarefas comuns de automação com as bibliotecas de gerenciamento do Azure para Python e possuem códigos prontos para uso em seus próprios aplicativos:
- [Máquinas virtuais](python-sdk-azure-virtual-machine-samples.md)
- [Aplicativos Web](python-sdk-azure-web-apps-samples.md)
- [Banco de Dados SQL](python-sdk-azure-sql-database-samples.md)

Uma [referência](/python/api/overview/azure) está disponível para todos os pacotes nas bibliotecas de serviço e de gerenciamento. Novos recursos, alterações significativas, e instruções de migração de versões anteriores estão disponíveis nas [notas de versão](python-sdk-azure-release-notes.md). 

## <a name="get-help-and-give-feedback"></a>Obter ajuda e fazer comentários

Poste perguntas para a comunidade no [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) e divulgue problemas com o SDK no [GitHub do projeto](https://github.com/Azure/azure-sdk-for-python).
