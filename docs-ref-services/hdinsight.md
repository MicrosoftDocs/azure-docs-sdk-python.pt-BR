---
title: Versão Prévia do SDK do Python do Azure HDInsight
description: Referência para o SDK do Python do Azure HDInsight. O SDK do Python do HDInsight oferece classes e métodos que permitem gerenciar os clusters do HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 42e1e36b5854fda93188564be3ed3064b9ba4435
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277463"
---
# <a name="hdinsight-python-management-sdk-preview"></a><span data-ttu-id="5a0b9-104">Versão Prévia do SDK de Gerenciamento do Python do HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a0b9-104">HDInsight Python Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="5a0b9-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5a0b9-105">Overview</span></span>

<span data-ttu-id="5a0b9-106">O SDK do Python do HDInsight oferece classes e métodos que permitem gerenciar os clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-106">The HDInsight Python SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="5a0b9-107">Ele inclui operações para criar, excluir, atualizar, listar, dimensionar, executar ações de script, monitorar, obter propriedades de clusters HDInsight e muito mais.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a0b9-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5a0b9-108">Prerequisites</span></span>

* <span data-ttu-id="5a0b9-109">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-109">An Azure account.</span></span> <span data-ttu-id="5a0b9-110">Se você não tiver uma, [obtenha uma avaliação gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5a0b9-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="5a0b9-111">Python</span><span class="sxs-lookup"><span data-stu-id="5a0b9-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="5a0b9-112">pip</span><span class="sxs-lookup"><span data-stu-id="5a0b9-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="5a0b9-113">Instalação do SDK</span><span class="sxs-lookup"><span data-stu-id="5a0b9-113">SDK Installation</span></span>

<span data-ttu-id="5a0b9-114">O SDK do Python do HDInsight pode ser encontrado no [Índice do Pacote do Python](https://pypi.org/project/azure-mgmt-hdinsight/) e instalado executando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-114">The HDInsight Python SDK can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="5a0b9-115">Autenticação</span><span class="sxs-lookup"><span data-stu-id="5a0b9-115">Authentication</span></span>

<span data-ttu-id="5a0b9-116">O SDK precisa primeiro ser autenticado com a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="5a0b9-117">Siga o exemplo abaixo para criar uma entidade de serviço e use-a para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="5a0b9-118">Após isso ser feito, você terá uma instância de um `HDInsightManagementClient`, que contém muitos métodos (destacados nas seções abaixo) que podem ser usados para realizar operações de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="5a0b9-119">Existem outras formas de autenticar além do exemplo abaixo que talvez sejam mais adequadas às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="5a0b9-120">Todos os métodos são descritos aqui: [Autenticar com as Bibliotecas de Gerenciamento do Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="5a0b9-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="5a0b9-121">Exemplo de autenticação usando uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="5a0b9-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="5a0b9-122">Primeiro, faça logon no [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="5a0b9-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="5a0b9-123">Verifique se você está usando atualmente a assinatura na qual deseja a entidade de serviço criada.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="5a0b9-124">As informações da assinatura são exibidas como JSON.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="5a0b9-125">Se você não estiver conectado à assinatura correta, selecione a correta executando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="5a0b9-126">Se você já não tiver registrado o Provedor de Recursos do HDInsight através de outro método (tais como criar um cluster do HDInsight através do portal do Azure), você precisa fazer isso uma vez antes de poder autenticar.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="5a0b9-127">Isso também pode ser feito no [Azure Cloud Shell](https://shell.azure.com/bash) executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="5a0b9-128">Em seguida, escolha um nome para a sua entidade de serviço e crie-a com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="5a0b9-129">As informações da entidade de serviço são exibidas como JSON.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="5a0b9-130">Copie o trecho do Python abaixo e preencha `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` e `SUBSCRIPTION_ID` com as cadeias de caracteres do JSON retornadas após a execução do comando para criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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


## <a name="cluster-management"></a><span data-ttu-id="5a0b9-131">Gerenciamento de clusters</span><span class="sxs-lookup"><span data-stu-id="5a0b9-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="5a0b9-132">Essa seção pressupõe que você já autenticou e criou uma `HDInsightManagementClient` instância e a armazenou em uma variável chamada `client`.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="5a0b9-133">As instruções para autenticar e obter um `HDInsightManagementClient` podem ser encontradas na seção Autenticação acima.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="5a0b9-134">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-134">Create a Cluster</span></span>

<span data-ttu-id="5a0b9-135">Um novo cluster pode ser criado chamando `client.clusters.create()`.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-135">A new cluster can be created by calling `client.clusters.create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="5a0b9-136">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-136">Example</span></span>

<span data-ttu-id="5a0b9-137">Este exemplo demonstra como criar um cluster Spark com 2 nós principais e 1 nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-137">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="5a0b9-138">Primeiro você precisa criar um grupo de recursos e uma conta de armazenamento, conforme explicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-138">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="5a0b9-139">Se você já os tiver criado, ignore as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-139">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="5a0b9-140">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5a0b9-140">Creating a Resource Group</span></span>

<span data-ttu-id="5a0b9-141">É possível criar um grupo de recursos usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-141">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="5a0b9-142">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5a0b9-142">Creating a Storage Account</span></span>

<span data-ttu-id="5a0b9-143">É possível criar uma conta de armazenamento usando o [Azure Cloud Shell](https://shell.azure.com/bash) executando:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-143">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="5a0b9-144">Agora execute o comando a seguir para obter a chave para a sua conta de armazenamento (você precisará dela para criar um cluster):</span><span class="sxs-lookup"><span data-stu-id="5a0b9-144">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="5a0b9-145">O trecho do Python abaixo cria um cluster Spark com dois nós principais e um nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-145">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="5a0b9-146">Preencha as variáveis em branco conforme explicado nos comentários e fique à vontade para alterar outros parâmetros conforme as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-146">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="5a0b9-147">Obter detalhes do cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-147">Get Cluster Details</span></span>

<span data-ttu-id="5a0b9-148">Para obter propriedades para um determinado cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-148">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5a0b9-149">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-149">Example</span></span>

<span data-ttu-id="5a0b9-150">Você pode usar `get` para confirmar que criou com êxito o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-150">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="5a0b9-151">A saída deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-151">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="5a0b9-152">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="5a0b9-152">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="5a0b9-153">Listar os clusters em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="5a0b9-153">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="5a0b9-154">Listar os clusters por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5a0b9-154">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="5a0b9-155">Ambos `list()` e `list_by_resource_group()` retornam um objeto `ClusterPaged`.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-155">Both `list()` and `list_by_resource_group()` return an `ClusterPaged` object.</span></span> <span data-ttu-id="5a0b9-156">Chamar `advance_page()` retorna uma lista de clusters nessa página e avança o objeto `ClusterPaged` para a página seguinte.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-156">Calling `advance_page()` returns the a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="5a0b9-157">Isso pode ser repetido até uma exceção `StopIteration` ser gerada, indicando que não existem mais páginas.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-157">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="5a0b9-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-158">Example</span></span>

<span data-ttu-id="5a0b9-159">O exemplo a seguir imprime as propriedades de todos os clusters da assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-159">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="5a0b9-160">Excluir um cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-160">Delete a Cluster</span></span>

<span data-ttu-id="5a0b9-161">Para excluir um cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-161">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="5a0b9-162">Atualizar marcas de cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-162">Update Cluster Tags</span></span>

<span data-ttu-id="5a0b9-163">É possível atualizar as marcas de um determinado cluster da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-163">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="5a0b9-164">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-164">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="scale-cluster"></a><span data-ttu-id="5a0b9-165">Dimensionar cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-165">Scale Cluster</span></span>

<span data-ttu-id="5a0b9-166">É possível dimensionar um determinado número de nós de trabalho do cluster especificando um novo tamanho da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-166">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="5a0b9-167">Monitoramento do cluster</span><span class="sxs-lookup"><span data-stu-id="5a0b9-167">Cluster Monitoring</span></span>

<span data-ttu-id="5a0b9-168">O SDK de gerenciamento do HDInsight também pode ser usado para gerenciar o monitoramento dos seus clusters através do Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="5a0b9-168">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="5a0b9-169">Habilitar Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="5a0b9-169">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="5a0b9-170">Para habilitar o Monitoramento de OMS, você deve ter um workspace existente do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-170">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="5a0b9-171">Se você já não tiver criado um, você pode aprender como fazer isso aqui: [Criar um workspace do Log Analytics no portal do Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="5a0b9-171">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="5a0b9-172">Para habilitar o Monitoramento de OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-172">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="5a0b9-173">Exibir o status do Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="5a0b9-173">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="5a0b9-174">Para obter o status do OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-174">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="5a0b9-175">Desabilitar Monitoramento de OMS</span><span class="sxs-lookup"><span data-stu-id="5a0b9-175">Disable OMS Monitoring</span></span>

<span data-ttu-id="5a0b9-176">Para desabilitar o OMS no seu cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-176">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="5a0b9-177">Ações de script</span><span class="sxs-lookup"><span data-stu-id="5a0b9-177">Script Actions</span></span>

<span data-ttu-id="5a0b9-178">O HDInsight fornece um método de configuração chamado ações de script que chama os scripts personalizados para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-178">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="5a0b9-179">Mais informações sobre como usar as ações de script podem ser encontradas aqui: [Personalizar clusters HDInsight com base em Linux usando ações de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="5a0b9-179">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="5a0b9-180">Executar ações de script</span><span class="sxs-lookup"><span data-stu-id="5a0b9-180">Execute Script Actions</span></span>
<span data-ttu-id="5a0b9-181">Para executar as ações de script em um determinado cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-181">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="5a0b9-182">Excluir ação de script</span><span class="sxs-lookup"><span data-stu-id="5a0b9-182">Delete Script Action</span></span>

<span data-ttu-id="5a0b9-183">Para excluir uma ação de script persistente específica em um determinado cluster:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-183">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="5a0b9-184">Listar ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="5a0b9-184">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="5a0b9-185">`list()` e `list_persisted_scripts()` retornam um objeto `RuntimeScriptActionDetailPaged`.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-185">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="5a0b9-186">Chamar `advance_page()` retorna uma lista de `RuntimeScriptActionDetail` nessa página e avança o objeto `RuntimeScriptActionDetailPaged` para a página seguinte.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-186">Calling `advance_page()` returns the a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="5a0b9-187">Isso pode ser repetido até uma exceção `StopIteration` ser gerada, indicando que não existem mais páginas.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-187">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="5a0b9-188">Veja o exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-188">See the example below.</span></span>

<span data-ttu-id="5a0b9-189">Para listar todas as ações de script persistentes para o cluster especificado:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-189">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5a0b9-190">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-190">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="5a0b9-191">Listar o histórico de execução de todos os scripts</span><span class="sxs-lookup"><span data-stu-id="5a0b9-191">List All Scripts' Execution History</span></span>

<span data-ttu-id="5a0b9-192">Para listar o histórico de execução de todos os scripts para o cluster especificado:</span><span class="sxs-lookup"><span data-stu-id="5a0b9-192">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5a0b9-193">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0b9-193">Example</span></span>

<span data-ttu-id="5a0b9-194">Este exemplo imprime todos os detalhes para todas as execuções de script anteriores.</span><span class="sxs-lookup"><span data-stu-id="5a0b9-194">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
