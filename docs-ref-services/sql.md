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
# <a name="azure-sql-database-libraries-for-python"></a>Bibliotecas de Banco de Dados SQL do Azure para Python

## <a name="overview"></a>Visão geral

Trabalhar com dados armazenados no [Banco de Dados SQL do Azure](/azure/sql-database/sql-database-technical-overview) a partir de Python com o driver ODBC e pyodbc. 

## <a name="client-odbc-driver-and-pyodbc"></a>Pyodbc e driver ODBC de cliente

```bash
pip install pyodbc
```
Mais detalhes sobre como instalar as bibliotecas de comunicação de banco de dados e Python podem ser encontrados [aqui](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

### <a name="example"></a>Exemplo

Conectar-se a um banco de dados SQL e selecionar todos os registros em uma tabela.

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

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar recursos do Banco de Dados SQL do Azure em sua assinatura com a API de gerenciamento. 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a>Exemplo

Criar um recurso de Banco de Dados SQL e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a>Exemplos

* [Criar e gerenciar bancos de dados SQL][1]    
* [Usar o Python para se conectar e consultar dados][2]   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) de exemplos do banco de dados SQL do Azure. 