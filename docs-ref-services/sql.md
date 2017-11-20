---
title: Bibliotecas de Banco de Dados SQL do Azure para Python
description: 
keywords: Azure, Python, SDK, API, SQL, banco de dados, pyodbc
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: b580c5011412bc77fd8fd55b709a305be07e2316
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-sql-database-libraries-for-python"></a><span data-ttu-id="3a46e-103">Bibliotecas de Banco de Dados SQL do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="3a46e-103">Azure SQL Database libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="3a46e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3a46e-104">Overview</span></span>

<span data-ttu-id="3a46e-105">Trabalhar com dados armazenados no [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview) a partir de Python com o driver ODBC e pyodbc.</span><span class="sxs-lookup"><span data-stu-id="3a46e-105">Work with data stored in [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) from Python with the Microsoft ODBC driver and pyodbc.</span></span> 

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="3a46e-106">Pyodbc e driver ODBC de cliente</span><span class="sxs-lookup"><span data-stu-id="3a46e-106">Client ODBC driver and pyodbc</span></span>

```bash
pip install pyodbc
```
<span data-ttu-id="3a46e-107">Mais detalhes sobre como instalar as bibliotecas de comunicação de banco de dados e Python podem ser encontrados [aqui](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="3a46e-107">More details about installing the python and database communication libraries can be found [here](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span>

### <a name="example"></a><span data-ttu-id="3a46e-108">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3a46e-108">Example</span></span>

<span data-ttu-id="3a46e-109">Conectar-se a um banco de dados SQL e selecionar todos os registros em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="3a46e-109">Connect to a SQL database and select all records in a table.</span></span>

```python
import pyodbc 

SERVER = 'YOUR_SERVER_NAME.database.windows.net'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_DB_USERNAME'
PASSWORD = 'YOUR_DB_PASSWORD'

DRIVER= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER=' + DRIVER + ';PORT=1433;SERVER=' + SERVER +
    ';PORT=1443;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a><span data-ttu-id="3a46e-110">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="3a46e-110">Management API</span></span>

<span data-ttu-id="3a46e-111">Criar e gerenciar recursos do Banco de Dados SQL do Azure em sua assinatura com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="3a46e-111">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span> 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a><span data-ttu-id="3a46e-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3a46e-112">Example</span></span>

<span data-ttu-id="3a46e-113">Criar um recurso de Banco de Dados SQL e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="3a46e-113">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="3a46e-114">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="3a46e-114">Explore the Management APIs</span></span>](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a><span data-ttu-id="3a46e-115">Exemplos</span><span class="sxs-lookup"><span data-stu-id="3a46e-115">Samples</span></span>

* <span data-ttu-id="3a46e-116">[Criar e gerenciar bancos de dados SQL][1]</span><span class="sxs-lookup"><span data-stu-id="3a46e-116">[Create and manage SQL databases][1]</span></span>    
* <span data-ttu-id="3a46e-117">[Usar o Python para se conectar e consultar dados][2]</span><span class="sxs-lookup"><span data-stu-id="3a46e-117">[Use Python to connect and query data][2]</span></span>   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

<span data-ttu-id="3a46e-118">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) de exemplos do banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a46e-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) of Azure SQL database samples.</span></span> 