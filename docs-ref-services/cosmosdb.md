---
title: Bibliotecas do Azure Cosmos DB para Python
description: Documentação de referência para as bibliotecas de cliente de Python para o Azure Cosmos DB
keywords: Azure, Python, SDK, API, SQL, banco de dados, PostGres,Cosmos DB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: 391b556ece7d818406fa501763814eb7f0d50d22
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204133"
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="c02e0-104">Bibliotecas do Azure Cosmos DB para Python</span><span class="sxs-lookup"><span data-stu-id="c02e0-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="c02e0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c02e0-105">Overview</span></span>

<span data-ttu-id="c02e0-106">Use o Azure Cosmos DB em seus aplicativos do Python para armazenar e consultar documentos JSON em um repositório de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="c02e0-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="c02e0-107">Saiba mais sobre o [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="c02e0-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="c02e0-108">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="c02e0-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="c02e0-109">Biblioteca de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c02e0-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="c02e0-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c02e0-110">Example</span></span>

<span data-ttu-id="c02e0-111">Localizar documentos correspondentes no Azure Cosmos DB usando uma interface de consulta do tipo SQL:</span><span class="sxs-lookup"><span data-stu-id="c02e0-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
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
> [<span data-ttu-id="c02e0-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c02e0-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="c02e0-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="c02e0-113">Samples</span></span>

[<span data-ttu-id="c02e0-114">Desenvolver um aplicativo Python usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c02e0-114">Develop a Python app using Azure Cosmos DB</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


