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
ms.openlocfilehash: d56dd69f4fc4513034046f9f721608ad94ff5cfe
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-cosmosdb-libraries-for-python"></a>Bibliotecas do Azure CosmosDB para Python

## <a name="overview"></a>Visão geral

Use CosmosDB nos seus aplicativos do Python para armazenar e consultar documentos JSON em um repositório de dados NoSQL.

Saiba mais sobre o [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Biblioteca do cliente
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Biblioteca de gerenciamento
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Exemplo

Localizar documentos correspondentes no CosmosDB usando uma interface de consulta do tipo SQL:

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Exemplos

[Desenvolver um aplicativo Python usando a API do DocumentDB do Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


