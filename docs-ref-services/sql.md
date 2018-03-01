---
title: Bibliotecas de Banco de Dados SQL do Azure para Python
description: "Conecte-se ao banco de dados SQL do Azure usando pyodbc e o driver ODBC ou gerencie as instâncias do SQL do Azure com a API de gerenciamento."
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 01/09/2018
ms.topic: reference
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: 6c442a7a1e639938c993e8c1e6f74bc5e0a730b7
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-sql-database-libraries-for-python"></a>Bibliotecas de Banco de Dados SQL do Azure para Python

## <a name="overview"></a>Visão geral

Trabalhe com dados armazenados no [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview) a partir de Python com o [driver de banco de dados ODBC](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers). Confira nosso [início rápido](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python). Basta se conectar a um banco de dados SQL do Azure e usar instruções Transact-SQL para consultar dados e [exemplo](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) de introdução com pyodbc.

## <a name="install-odbc-driver-and-pyodbc"></a>Instalar pyodbc e o driver ODBC

```bash
pip install pyodbc
```
Mais [detalhes](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) sobre como instalar as bibliotecas de comunicação de banco de dados e Python.

## <a name="connect-and-execute-a-sql-query"></a>Conectar e executar uma consulta SQL

### <a name="connect-to-a-sql-database"></a>Conectar-se a um Banco de Dados SQL

```python
import pyodbc

server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'

cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
```

### <a name="execute-a-sql-query"></a>Executar uma consulta SQL

```python
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

> [!div class="nextstepaction"]
> [exemplo de pyodbc](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)

## <a name="connecting-to-orms"></a>Conectando ao ORMs

o pyodbc funciona com outros ORMs como [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) e [Django](https://github.com/lionheart/django-pyodbc/). 

## <a name="management-apipythonapioverviewazuresqlmanagement"></a>[API de Gerenciamento](/python/api/overview/azure/sql/management)

Criar e gerenciar recursos do Banco de Dados SQL do Azure em sua assinatura com a API de gerenciamento. 

```bash
pip install azure-common
pip install azure-mgmt-sql
pip install azure-mgmt-resource
```

## <a name="example"></a>Exemplo

Criar um recurso de Banco de Dados SQL e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# create resource client
resource_client = get_client_from_cli_profile(ResourceManagementClient)
# create resource group
resource_client.resource_groups.create_or_update(RESOURCE_GROUP, {'location': LOCATION})

sql_client = get_client_from_cli_profile(SqlManagementClient)

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/sql/management)

