---
title: Bibliotecas de PostgreSQL do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, SQL, banco de dados, PostGres, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: postgresql
ms.openlocfilehash: cad5995072d5040764986765d9a900f46f5141ec
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478929"
---
#<a name="azure-postgresql-libraries-for-python"></a>Bibliotecas de PostgreSQL do Azure para Python

## <a name="overview"></a>Visão geral
Use o driver ODBC e o pyodbc para se conectar ao banco de dados e executar instruções SQL diretamente.

Saiba mais sobre o [Banco de Dados do Azure para PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

## <a name="client-odbc-driver-and-pyodbc"></a>Pyodbc e driver ODBC de cliente
A biblioteca de cliente recomendada para acessar o Banco de Dados do Azure para PostgreSQL é o Microsoft [ODBC driver e o pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)

### <a name="example"></a>Exemplo 

Conectar-se ao Banco de Dados do Azure para PostgreSQL e selecionar todos os registros na tabela `SALES`. Você pode obter a cadeia de conexão de ODBC para o seu banco de dados a partir do portal do Azure.

```python
import pyodbc

SERVER = 'YOUR_SERVER_NAME.postgres.database.azure.com'
DATABASE = 'YOUR_DB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

DRIVER = '{PostgreSQL ODBC Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=5432;SERVER=' + SERVER +
    ';PORT=5432;DATABASE=' + DATABASE + ';UID=' + USERNAME +
    ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES" # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>API de gerenciamento
### <a name="requirements"></a>Requisitos
Você deve instalar as bibliotecas de gerenciamento do PostGreSQL para Python.
```bash
pip install azure-mgmt-rdbms
```

Consulte a página de [autenticação do SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre como obter credenciais para autenticar com o cliente de gerenciamento.

### <a name="example"></a>Exemplo
Neste exemplo, criaremos um novo banco de dados Postgres em nosso servidor Postgres existente.
```python
from azure.mgtm.rdbms.postgresql import PostgreSQLManagementClient

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE_GROUP_WITH_POSTGRES"
POSTGRES_SERVER = "YOUR_POSTGRES_SERVER_NAME"
DB_NAME = "YOUR_DESIRED_DATABASE_NAME"

client = PostgreSQLManagementClient(credentials, SUBSCRIPTION_ID)

db_creation_poller = client.databases.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=POSTGRES_SERVER, database_name=DB_NAME)
db = db_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/postgresql/management)

