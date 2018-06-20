---
title: Bibliotecas do MySQL do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, SQL, banco de dados, MySQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: mysql
ms.openlocfilehash: f03134bfddfabc426cbcaf4d98ef86d14038861f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479179"
---
# <a name="azure-mysql-libraries-for-python"></a>Bibliotecas do MySQL do Azure para Python 

## <a name="overview"></a>Visão geral

Trabalhar com recursos e dados armazenados no [Banco de Dados MySQL do Azure](/azure/mysql/overview) a partir do Python com o gerenciador do MySQL e pyodbc.

## <a name="client-odbc-driver-and-pyodbc"></a>Pyodbc e driver ODBC de cliente

A biblioteca de cliente recomendada para acessar o Banco de Dados do Azure para MySQL é o [driver ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) da Microsoft. Use o driver ODBC para se conectar ao banco de dados e executar instruções SQL diretamente.

### <a name="example"></a>Exemplo

Conectar-se ao Banco de Dados do Azure para MySQL e selecionar todos os registros na tabela de vendas. Você pode obter a cadeia de conexão de ODBC para o seu banco de dados a partir do portal do Azure.

```python
SERVER = 'YOUR_SEVER_NAME' + '.mysql.database.azure.com'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_MYSQL_USERNAME'
PASSWORD = 'YOUR_MYSQL_PASSWORD'

DRIVER = '{MySQL ODBC 5.3 UNICODE Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=3306;SERVER=' + SERVER + ';PORT=3306;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>API de gerenciamento

Criar e gerenciar recursos do MySQL na sua assinatura com a API de gerenciamento.

### <a name="requirements"></a>Requisitos
Você deve instalar as bibliotecas de gerenciamento do MySQL para Python.
```bash
pip install azure-mgmt-rdbms
```

Consulte a página de [autenticação do SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre como obter credenciais para autenticar com o cliente de gerenciamento.

### <a name="example"></a>Exemplo

Criar um recurso de Banco de Dados MySQL 5.7 e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.

```python

from azure.mgmt.rdbms.mysql import MySQLManagementClient
from azure.mgmt.rdbms.mysql.models import ServerForCreate, ServerPropertiesForDefaultCreate, ServerVersion

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE-GROUP_WITH_POSTGRES"
MYSQL_SERVER = "YOUR_DESIRED_MYSQL_SERVER_NAME"
MYSQL_ADMIN_USER = "YOUR_MYSQL_ADMIN_USERNAME"
MYSQL_ADMIN_PASSWORD = "YOUR_MYSQL_ADMIN_PASSOWRD"
LOCATION = "westus"  # example Azure availability zone, should match resource group


client = MySQLManagementClient(credentials=creds,
    subscription_id=SUBSCRIPTION_ID)

server_creation_poller = client.servers.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=MYSQL_SERVER,
    ServerForCreate(
        ServerPropertiesForDefaultCreate(
            administrator_login=MYSQL_ADMIN_USER,
            administrator_login_password=MYSQL_ADMIN_PASSWORD,
            version=ServerVersion.five_full_stop_seven
        ),
        location=LOCATION
    )
)

server = server_creation_poller.result()

# Open access to this server for IPs
rule_creation_poller = client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    MYSQL_SERVER,
    "some_custom_ip_range_whitelist_rule_name",  # Custom firewall rule name
    "123.123.123.123",  # Start ip range
    "167.220.0.235"  # End ip range
)

firewall_rule = rule_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/mysql/management)