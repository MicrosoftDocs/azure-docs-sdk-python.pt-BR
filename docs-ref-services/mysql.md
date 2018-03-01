---
title: Bibliotecas do MySQL do Azure para Python
description: 
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
---
# <a name="azure-mysql-libraries-for-python"></a><span data-ttu-id="c750f-103">Bibliotecas do MySQL do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="c750f-103">Azure MySQL libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="c750f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c750f-104">Overview</span></span>

<span data-ttu-id="c750f-105">Trabalhar com recursos e dados armazenados no [Banco de Dados MySQL do Azure](/azure/mysql/overview) a partir do Python com o gerenciador do MySQL e pyodbc.</span><span class="sxs-lookup"><span data-stu-id="c750f-105">Work with resources and data stored in [Azure MySQL Database](/azure/mysql/overview) from python with the MySQL manager and pyodbc.</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="c750f-106">Pyodbc e driver ODBC de cliente</span><span class="sxs-lookup"><span data-stu-id="c750f-106">Client ODBC driver and pyodbc</span></span>

<span data-ttu-id="c750f-107">A biblioteca de cliente recomendada para acessar o Banco de Dados do Azure para MySQL é o [driver ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c750f-107">The recommended client library for accessing Azure Database for MySQL is the Microsoft [ODBC driver](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span> <span data-ttu-id="c750f-108">Use o driver ODBC para se conectar ao banco de dados e executar instruções SQL diretamente.</span><span class="sxs-lookup"><span data-stu-id="c750f-108">Use the ODBC driver to connect to the database and execute SQL statements directly.</span></span>

### <a name="example"></a><span data-ttu-id="c750f-109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c750f-109">Example</span></span>

<span data-ttu-id="c750f-110">Conectar-se ao Banco de Dados do Azure para MySQL e selecionar todos os registros na tabela de vendas.</span><span class="sxs-lookup"><span data-stu-id="c750f-110">Connect to a Azure Database for MySQL and select all records in the sales table.</span></span> <span data-ttu-id="c750f-111">Você pode obter a cadeia de conexão de ODBC para o seu banco de dados a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c750f-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="c750f-112">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c750f-112">Management API</span></span>

<span data-ttu-id="c750f-113">Criar e gerenciar recursos do MySQL na sua assinatura com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c750f-113">Create and manage MySQL resources in your subscription with the management API.</span></span>

### <a name="requirements"></a><span data-ttu-id="c750f-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="c750f-114">Requirements</span></span>
<span data-ttu-id="c750f-115">Você deve instalar as bibliotecas de gerenciamento do MySQL para Python.</span><span class="sxs-lookup"><span data-stu-id="c750f-115">You must install the MySQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="c750f-116">Consulte a página de [autenticação do SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) para obter detalhes sobre como obter credenciais para autenticar com o cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c750f-116">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="c750f-117">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c750f-117">Example</span></span>

<span data-ttu-id="c750f-118">Criar um recurso de Banco de Dados MySQL 5.7 e restringir o acesso a um intervalo de endereços IP usando uma regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="c750f-118">Create a MySQL 5.7 Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="c750f-119">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c750f-119">Explore the Management APIs</span></span>](/python/api/overview/azure/mysql/management)