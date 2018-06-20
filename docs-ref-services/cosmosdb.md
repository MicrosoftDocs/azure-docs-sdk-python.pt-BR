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
# <a name="azure-cosmos-db-libraries-for-python"></a>Bibliotecas do Azure Cosmos DB para Python

## <a name="overview"></a>Visão geral

Use o Azure Cosmos DB em seus aplicativos do Python para armazenar e consultar documentos JSON em um repositório de dados NoSQL.

Saiba mais sobre o [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Biblioteca do cliente
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Biblioteca de gerenciamento
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Exemplo

Localizar documentos correspondentes no Azure Cosmos DB usando uma interface de consulta do tipo SQL:

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Exemplos

[Desenvolver um aplicativo Python usando o Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


