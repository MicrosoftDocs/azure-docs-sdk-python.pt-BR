---
title: Bibliotecas do Azure CosmosDB para Python
description: "Documentação de referência para as bibliotecas de cliente de Python para Cosmos DB"
keywords: Azure, Python, SDK, API, SQL, banco de dados, PostGres, CosmosDB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/11/2017
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: 5382779d659f7c85e5ecbd304920e00b78a08a49
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmosdb-libraries-for-python"></a><span data-ttu-id="d3d9c-104">Bibliotecas do Azure CosmosDB para Python</span><span class="sxs-lookup"><span data-stu-id="d3d9c-104">Azure CosmosDB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="d3d9c-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d3d9c-105">Overview</span></span>

<span data-ttu-id="d3d9c-106">Use CosmosDB nos seus aplicativos do Python para armazenar e consultar documentos JSON em um repositório de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="d3d9c-106">Use CosmosDB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="d3d9c-107">Saiba mais sobre o [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="d3d9c-107">Learn more about [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="d3d9c-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="d3d9c-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="d3d9c-109">Biblioteca de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="d3d9c-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="d3d9c-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d3d9c-110">Example</span></span>

<span data-ttu-id="d3d9c-111">Localizar documentos correspondentes no CosmosDB usando uma interface de consulta do tipo SQL:</span><span class="sxs-lookup"><span data-stu-id="d3d9c-111">Find matching documents in CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python DocumentDB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="d3d9c-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="d3d9c-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/managementlibrary)

## <a name="samples"></a><span data-ttu-id="d3d9c-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d3d9c-113">Samples</span></span>

[<span data-ttu-id="d3d9c-114">Desenvolver um aplicativo Python usando a API do DocumentDB do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d3d9c-114">Develop a Python app using Azure Cosmos DB's DocumentDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


