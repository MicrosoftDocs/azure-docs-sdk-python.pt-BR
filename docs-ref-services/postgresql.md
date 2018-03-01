---
title: Bibliotecas de PostgreSQL do Azure para Python
description: 
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
---
#<a name="azure-postgresql-libraries-for-python"></a><span data-ttu-id="2b6fa-103">Bibliotecas de PostgreSQL do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="2b6fa-103">Azure PostgreSQL libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="2b6fa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2b6fa-104">Overview</span></span>
<span data-ttu-id="2b6fa-105">Use o driver ODBC e o pyodbc para se conectar ao banco de dados e executar instruções SQL diretamente.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-105">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="2b6fa-106">Saiba mais sobre o [Banco de Dados do Azure para PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="2b6fa-106">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="2b6fa-107">Pyodbc e driver ODBC de cliente</span><span class="sxs-lookup"><span data-stu-id="2b6fa-107">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="2b6fa-108">A biblioteca de cliente recomendada para acessar o Banco de Dados do Azure para PostgreSQL é o Microsoft [ODBC driver e o pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span><span class="sxs-lookup"><span data-stu-id="2b6fa-108">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

### <a name="example"></a><span data-ttu-id="2b6fa-109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2b6fa-109">Example</span></span> 

<span data-ttu-id="2b6fa-110">Conectar-se ao Banco de Dados do Azure para PostgreSQL e selecionar todos os registros na tabela `SALES`.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-110">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="2b6fa-111">Você pode obter a cadeia de conexão de ODBC para o seu banco de dados a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="2b6fa-112">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="2b6fa-112">Management API</span></span>
### <a name="requirements"></a><span data-ttu-id="2b6fa-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="2b6fa-113">Requirements</span></span>
<span data-ttu-id="2b6fa-114">Você deve instalar as bibliotecas de gerenciamento do PostGreSQL para Python.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-114">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="2b6fa-115">Consulte a página de [autenticação do SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre como obter credenciais para autenticar com o cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-115">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="2b6fa-116">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2b6fa-116">Example</span></span>
<span data-ttu-id="2b6fa-117">Neste exemplo, criaremos um novo banco de dados Postgres em nosso servidor Postgres existente.</span><span class="sxs-lookup"><span data-stu-id="2b6fa-117">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
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
> [<span data-ttu-id="2b6fa-118">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="2b6fa-118">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/management)

