---
title: SDK do Azure HDInsight para Python
description: Referência do SDK do Azure HDInsight para Python. O SDK do HDInsight para Python oferece classes e métodos que permitem gerenciar os clusters do HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 04/10/2019
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: f16e5da474e1c506c800b860b451754a6bdc75bc
ms.sourcegitcommit: 3c6087cbc1fee5a2c88c40fe96d351375c6c6377
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59504543"
---
# <a name="hdinsight-sdk-for-python"></a>SDK do HDInsight para Python

## <a name="overview"></a>Visão geral

O SDK do HDInsight para Python oferece classes e métodos que permitem gerenciar os clusters do HDInsight. Inclui operações para criar, excluir, atualizar, listar, redimensionar, executar ações de script, monitorar, obter propriedades dos clusters HDInsight e muito mais.

## <a name="prerequisites"></a>Pré-requisitos

* Uma conta do Azure. Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/).
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>Instalação do SDK

O SDK do HDInsight para Python pode ser encontrado no [Índice do Pacote do Python](https://pypi.org/project/azure-mgmt-hdinsight/) e instalado executando: 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>Authentication

O SDK precisa primeiro ser autenticado com a assinatura do Azure.  Siga o exemplo abaixo para criar uma entidade de serviço e use-a para a autenticação. Após isso ser feito, você terá uma instância de um `HDInsightManagementClient`, que contém muitos métodos (destacados nas seções abaixo) que podem ser usados para realizar operações de gerenciamento.

> [!NOTE]
> Existem outras formas de autenticar além do exemplo abaixo que talvez sejam mais adequadas às suas necessidades. Todos os métodos são descritos aqui: [Autenticar com as Bibliotecas de Gerenciamento do Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>Exemplo de autenticação usando uma entidade de serviço

Primeiro, faça logon no [Azure Cloud Shell](https://shell.azure.com/bash). Verifique se você está usando atualmente a assinatura na qual deseja a entidade de serviço criada. 

```azurecli-interactive
az account show
```

As informações da assinatura são exibidas como JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Se você não estiver conectado à assinatura correta, selecione a correta executando: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Se você já não tiver registrado o Provedor de Recursos do HDInsight através de outro método (tais como criar um cluster do HDInsight através do portal do Azure), você precisa fazer isso uma vez antes de poder autenticar. Isso também pode ser feito no [Azure Cloud Shell](https://shell.azure.com/bash) executando o seguinte comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Em seguida, escolha um nome para a sua entidade de serviço e crie-a com o seguinte comando:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

As informações da entidade de serviço são exibidas como JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Copie o trecho do Python abaixo e preencha `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` com as cadeias de caracteres do JSON retornadas após a execução do comando para criar a entidade de serviço.

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a>Gerenciamento de clusters

> [!NOTE]
> Essa seção pressupõe que você já autenticou e criou uma `HDInsightManagementClient` instância e a armazenou em uma variável chamada `client`. As instruções para autenticar e obter um `HDInsightManagementClient` podem ser encontradas na seção Autenticação acima.

### <a name="create-a-cluster"></a>Criar um cluster

Um novo cluster pode ser criado chamando `client.clusters.create()`. 

#### <a name="example"></a>Exemplo

Este exemplo demonstra como criar um cluster Spark com 2 nós principais e 1 nó de trabalho.

> [!NOTE]
> Primeiro você precisa criar um grupo de recursos e uma conta de armazenamento, conforme explicado abaixo. Se você já os tiver criado, ignore as próximas etapas.

##### <a name="creating-a-resource-group"></a>Criar um grupo de recursos

É possível criar um grupo de recursos usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Criar uma conta de armazenamento

É possível criar uma conta de armazenamento usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Agora execute o comando a seguir para obter a chave para a sua conta de armazenamento (você precisará dela para criar um cluster):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
O trecho do Python abaixo cria um cluster Spark com dois nós principais e um nó de trabalho. Preencha as variáveis em branco conforme explicado nos comentários e fique à vontade para alterar outros parâmetros conforme as suas necessidades.

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

#### <a name="samples"></a>Exemplos

Os exemplos de código para criar vários tipos comuns de clusters HDInsight também estão disponíveis: [Exemplos de HDInsight para Python](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).

### <a name="get-cluster-details"></a>Obter detalhes do cluster

Para obter propriedades para um determinado cluster:

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemplo

Você pode usar `get` para confirmar que criou com êxito o seu cluster.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

A saída deve ser assim:

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>Listar clusters

#### <a name="list-clusters-under-the-subscription"></a>Listar os clusters em uma assinatura

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>Listar os clusters por grupo de recursos

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> Tanto `list()` quanto `list_by_resource_group()` retornam um objeto `ClusterPaged`. Chamar `advance_page()` retorna uma lista de clusters nessa página e avança o objeto `ClusterPaged` para a página seguinte. Isso pode ser repetido até uma exceção `StopIteration` ser gerada, indicando que não existem mais páginas.

#### <a name="example"></a>Exemplo

O exemplo a seguir imprime as propriedades de todos os clusters da assinatura atual:

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>Excluir um cluster

Para excluir um cluster:

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>Atualizar marcas de cluster

É possível atualizar as marcas de um determinado cluster da seguinte forma:

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>Exemplo

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a>Redimensionar Cluster

É possível redimensionar o número de nós de trabalho de determinado cluster especificando um novo tamanho, assim:

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>Monitoramento do cluster

O SDK de gerenciamento do HDInsight também pode ser usado para gerenciar o monitoramento dos seus clusters através do Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Habilitar Monitoramento de OMS

> [!NOTE]
> Para habilitar o Monitoramento de OMS, você deve ter um espaço de trabalho do Log Analytics existente. Se você ainda não criou, aprenda como fazer isso aqui: [Criar um espaço de trabalho do Log Analytics no Portal do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Para habilitar o Monitoramento de OMS no seu cluster:

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>Exibir o status do Monitoramento de OMS

Para obter o status do OMS no seu cluster:

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>Desabilitar Monitoramento de OMS

Para desabilitar o OMS no seu cluster:

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>Ações de script

O HDInsight fornece um método de configuração chamado ações de script que chama os scripts personalizados para personalizar o cluster.
> [!NOTE]
> Mais informações sobre como usar as ações de script podem ser encontradas aqui: [Customizar clusters HDInsight baseados em Linux usando as ações de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Executar ações de script
Para executar as ações de script em um determinado cluster:

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Excluir ação de script

Para excluir uma ação de script persistente específica em um determinado cluster:

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>Listar ações de script persistentes

> [!NOTE]
> `list()` e `list_persisted_scripts()` retornam um objeto `RuntimeScriptActionDetailPaged`. Chamar `advance_page()` retorna uma lista de `RuntimeScriptActionDetail` nessa página e avança o objeto `RuntimeScriptActionDetailPaged` para a página seguinte. Isso pode ser repetido até uma exceção `StopIteration` ser gerada, indicando que não existem mais páginas. Veja o exemplo abaixo.

Para listar todas as ações de script persistentes para o cluster especificado:
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemplo

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>Listar o histórico de execução de todos os scripts

Para listar o histórico de execução de todos os scripts para o cluster especificado:

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemplo

Este exemplo imprime todos os detalhes para todas as execuções de script anteriores.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
