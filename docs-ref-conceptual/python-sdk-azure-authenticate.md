---
title: Autenticar com as bibliotecas de gerenciamento do Azure para Python
description: Autenticar com uma entidade de serviço nas bibliotecas de gerenciamento do Azure para Python
keywords: Azure, Python, SDK, API, autenticação, active directory, entidade de serviço
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/11/2019
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51f26b120cefffd2d7f4af9c2b6b2cb532bc6006
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586804"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="4f6ce-104">Autenticar com as Bibliotecas de Gerenciamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="4f6ce-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="4f6ce-105">Várias opções estão disponíveis para autenticar seu aplicativo com o Azure ao usar as bibliotecas de gerenciamento de Python para criar e gerenciar recursos.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="4f6ce-106">Autenticar com credenciais do token</span><span class="sxs-lookup"><span data-stu-id="4f6ce-106">Authenticate with token credentials</span></span>

<span data-ttu-id="4f6ce-107">Armazene as credenciais com segurança em um arquivo de configuração, no registro ou no Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="4f6ce-108">O exemplo a seguir usa uma [entidade de serviço](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6ce-109">Para criar uma entidade de serviço com a CLI do Azure, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-109">To create a service principal with the Azure CLI, use the following command:</span></span>
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> <span data-ttu-id="4f6ce-110">Para saber mais sobre como configurar as entidades de serviço com a CLI, confira [Criar uma entidade de serviço do Azure com a CLI do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="4f6ce-110">To learn more about setting up service princpals with the CLI, see [Create an Azure service principal with Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials

# Tenant ID for your Azure subscription
TENANT_ID = '<Your tenant ID>'

# Your service principal App ID
CLIENT = '<Your service principal ID>'

# Your service principal password
KEY = '<Your service principal password>'

credentials = ServicePrincipalCredentials(
    client_id = CLIENT,
    secret = KEY,
    tenant = TENANT_ID
)
```

> <span data-ttu-id="4f6ce-111">[OBSERVAÇÃO!] Para conectar uma das nuvens soberanas do Azure, use o parâmetro `cloud_environment`.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-111">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>
>
> ```python
> from azure.common.credentials import ServicePrincipalCredentials
> from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
> 
> # Tenant ID for your Azure Subscription
> TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
> 
> # Your Service Principal App ID
> CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'
> 
> # Your Service Principal Password
> KEY = 'password'
> 
> credentials = ServicePrincipalCredentials(
>     client_id = CLIENT,
>     secret = KEY,
>     tenant = TENANT_ID,
>     cloud_environment = AZURE_CHINA_CLOUD
> )
> ```

<span data-ttu-id="4f6ce-112">Se você precisar de mais controle, é recomendável usar [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) e o wrapper ADAL do SDK.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-112">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="4f6ce-113">Consulte o site ADAL para ver todos os exemplos e lista de cenários disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-113">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="4f6ce-114">Para autenticação de entidade de serviço, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-114">For instance for service principal authentication:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD

# Tenant ID for your Azure Subscription
TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

# Your Service Principal App ID
CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

# Your Service Principal Password
KEY = 'password'

LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    RESOURCE,
    CLIENT,
    KEY
)
```

<span data-ttu-id="4f6ce-115">Todas as chamadas válidas ADAL podem ser usadas com a classe `AdalAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-115">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="4f6ce-116">Em seguida, crie um objeto de cliente para começar a trabalhar com a API:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-116">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="4f6ce-117">[OBSERVAÇÃO!] Ao usar uma nuvem soberana do Azure, você também deve especificar a URL base apropriada (por meio de constantes em `msrestazure.azure_cloud`) ao criar o cliente de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-117">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="4f6ce-118">Por exemplo, para a nuvem do Azure na China:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-118">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="4f6ce-119">Autenticação baseada em arquivos</span><span class="sxs-lookup"><span data-stu-id="4f6ce-119">File based authentication</span></span>

<span data-ttu-id="4f6ce-120">A maneira mais simples de autenticar é criar um arquivo JSON que contém as credenciais para uma entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-120">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="4f6ce-121">Você pode usar o seguinte comando da CLI para criar uma nova entidade de serviço e esse arquivo ao mesmo tempo:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-121">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="4f6ce-122">Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-122">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="4f6ce-123">Defina uma variável de ambiente com o caminho completo para o arquivo no shell:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-123">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="4f6ce-124">Se você deseja criar o arquivo por conta própria, siga este formato:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-124">If you want to create the file yourself, please follow this format:</span></span>

```json
{
    "clientId": "<Service principal ID>",
    "clientSecret": "<Service principal secret/password>",
    "subscriptionId": "<Subscription associated with the service principal>",
    "tenantId": "<The service principal's tenant>",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="4f6ce-125">Você pode então criar qualquer cliente usando a fábrica do cliente:</span><span class="sxs-lookup"><span data-stu-id="4f6ce-125">You can then create any client using the client factory:</span></span>

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="4f6ce-126">Autenticar com as Identidades Gerenciadas do Azure</span><span class="sxs-lookup"><span data-stu-id="4f6ce-126">Authenticate with Azure Managed Identities</span></span>
<span data-ttu-id="4f6ce-127">A Identidade Gerenciada do Azure é uma maneira simples de um recurso no Azure usar o SDK/CLI sem precisar criar credenciais específicas.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-127">Azure Managed Identity is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="4f6ce-128">Para usar as identidades gerenciadas, você deve se conectar ao Azure a partir de um recurso dele, como uma Função do Azure ou uma VM em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-128">To use managed identities, you must be connecting to Azure from an Azure resource, such as an Azure Function or a VM running in Azure.</span></span> <span data-ttu-id="4f6ce-129">Para saber como configurar uma identidade gerenciada para um recurso, confira [Configurar identidades gerenciadas para recursos do Azure](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) e [Como usar identidades gerenciadas para os recursos do Azure](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span><span class="sxs-lookup"><span data-stu-id="4f6ce-129">To learn how to configure a managed identity for a resource, see [Configure managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) and [How to use managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span></span>

```python
from msrestazure.azure_active_directory import MSIAuthentication
from azure.mgmt.resource import ResourceManagementClient, SubscriptionClient

# Create MSI Authentication
credentials = MSIAuthentication()


# Create a Subscription Client
subscription_client = SubscriptionClient(credentials)
subscription = next(subscription_client.subscriptions.list())
subscription_id = subscription.subscription_id

# Create a Resource Management client
resource_client = ResourceManagementClient(credentials, subscription_id)


# List resource groups as an example. The only limit is what role and policy are assigned to this MSI token.
for resource_group in resource_client.resource_groups.list():
    print(resource_group.name)
```

## <a name="mgmt-auth-cli"></a><span data-ttu-id="4f6ce-130">Autenticação com base em CLI</span><span class="sxs-lookup"><span data-stu-id="4f6ce-130">CLI-based authentication</span></span>

<span data-ttu-id="4f6ce-131">O SDK é capaz de criar um cliente usando uma assinatura ativa da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-131">The SDK is able to create a client using the Azure CLI's active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f6ce-132">Isso deve ser usado como a experiência de início rápido do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-132">This should be used as quick start developer experience.</span></span> <span data-ttu-id="4f6ce-133">Para fins de produção, use [ADAL](#mgmt-auth-legacy) ou o seu próprio sistema de credenciais.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-133">For production purposes, use [ADAL](#mgmt-auth-legacy) or your own credentials system.</span></span>
> <span data-ttu-id="4f6ce-134">Qualquer alteração em sua configuração de CLI terá impacto sobre a execução do SDK.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-134">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="4f6ce-135">Para definir as credenciais ativas, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4f6ce-135">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="4f6ce-136">A ID de assinatura padrão é a única que você tem, ou você pode defini-la usando [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="4f6ce-136">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="4f6ce-137">Autenticar com credenciais do token (herdadas)</span><span class="sxs-lookup"><span data-stu-id="4f6ce-137">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="4f6ce-138">Na versão anterior do SDK, ADAL ainda não estava disponível e fornecíamos uma classe `UserPassCredentials`.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-138">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="4f6ce-139">Ela é considerada obsoleta e não deve ser mais usada.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-139">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="4f6ce-140">Este exemplo mostra um cenário de usuário/senha.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-140">This sample shows user/password scenario.</span></span> <span data-ttu-id="4f6ce-141">Ele não oferece suporte a 2FA.</span><span class="sxs-lookup"><span data-stu-id="4f6ce-141">This does not support 2FA.</span></span>

```python
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
    'user@domain.com',
    'my_smart_password'
)
```
