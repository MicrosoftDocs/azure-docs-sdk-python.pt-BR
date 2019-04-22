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
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Autenticar com as Bibliotecas de Gerenciamento do Azure para Python

Várias opções estão disponíveis para autenticar seu aplicativo com o Azure ao usar as bibliotecas de gerenciamento de Python para criar e gerenciar recursos.

## <a name="mgmt-auth-token"></a>Autenticar com credenciais do token

Armazene as credenciais com segurança em um arquivo de configuração, no registro ou no Azure Key Vault.

O exemplo a seguir usa uma [entidade de serviço](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) para autenticação.

> [!NOTE]
> Para criar uma entidade de serviço com a CLI do Azure, use o seguinte comando:
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> Para saber mais sobre como configurar as entidades de serviço com a CLI, confira [Criar uma entidade de serviço do Azure com a CLI do Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

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

> [OBSERVAÇÃO!] Para conectar uma das nuvens soberanas do Azure, use o parâmetro `cloud_environment`.
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

Se você precisar de mais controle, é recomendável usar [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) e o wrapper ADAL do SDK. Consulte o site ADAL para ver todos os exemplos e lista de cenários disponíveis. Para autenticação de entidade de serviço, por exemplo:

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

Todas as chamadas válidas ADAL podem ser usadas com a classe `AdalAuthentication`.

Em seguida, crie um objeto de cliente para começar a trabalhar com a API:

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> [OBSERVAÇÃO!] Ao usar uma nuvem soberana do Azure, você também deve especificar a URL base apropriada (por meio de constantes em `msrestazure.azure_cloud`) ao criar o cliente de gerenciamento. Por exemplo, para a nuvem do Azure na China:
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a>Autenticação baseada em arquivos

A maneira mais simples de autenticar é criar um arquivo JSON que contém as credenciais para uma entidade de serviço do Azure. Você pode usar o seguinte comando da CLI para criar uma nova entidade de serviço e esse arquivo ao mesmo tempo:

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

Salve esse arquivo em um local seguro no sistema onde o seu código possa lê-lo. Defina uma variável de ambiente com o caminho completo para o arquivo no shell:

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

Se você deseja criar o arquivo por conta própria, siga este formato:

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

Você pode então criar qualquer cliente usando a fábrica do cliente:

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a>Autenticar com as Identidades Gerenciadas do Azure
A Identidade Gerenciada do Azure é uma maneira simples de um recurso no Azure usar o SDK/CLI sem precisar criar credenciais específicas.

> [!IMPORTANT]
>
> Para usar as identidades gerenciadas, você deve se conectar ao Azure a partir de um recurso dele, como uma Função do Azure ou uma VM em execução no Azure. Para saber como configurar uma identidade gerenciada para um recurso, confira [Configurar identidades gerenciadas para recursos do Azure](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) e [Como usar identidades gerenciadas para os recursos do Azure](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).

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

## <a name="mgmt-auth-cli"></a>Autenticação com base em CLI

O SDK é capaz de criar um cliente usando uma assinatura ativa da CLI do Azure.

> [!IMPORTANT]
> Isso deve ser usado como a experiência de início rápido do desenvolvedor. Para fins de produção, use [ADAL](#mgmt-auth-legacy) ou o seu próprio sistema de credenciais.
> Qualquer alteração em sua configuração de CLI terá impacto sobre a execução do SDK.

Para definir as credenciais ativas, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).
A ID de assinatura padrão é a única que você tem, ou você pode defini-la usando [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a>Autenticar com credenciais do token (herdadas)

Na versão anterior do SDK, ADAL ainda não estava disponível e fornecíamos uma classe `UserPassCredentials`. Ela é considerada obsoleta e não deve ser mais usada.

Este exemplo mostra um cenário de usuário/senha. Ele não oferece suporte a 2FA.

```python
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
    'user@domain.com',
    'my_smart_password'
)
```
