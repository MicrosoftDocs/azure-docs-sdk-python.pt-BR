---
title: Bibliotecas do Azure Key Vault para Python
description: Documentação de referência para as bibliotecas de cliente de Python para o Azure Key Vault
author: lisawong19
keywords: Azure, Python, SDK, API, Chaves, Key Vault, Autenticação, Segredo, chave, segurança
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3e7d9970f5799708c6822493106aec5466de52d9
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35719637"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="4b014-104">Bibliotecas do Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="4b014-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="4b014-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4b014-105">Overview</span></span>

<span data-ttu-id="4b014-106">Criar, atualizar e excluir chaves e segredos no Azure Key Vault com as bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="4b014-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="4b014-107">Use as bibliotecas de gerenciamento do Azure Key Vault para criar cofres de chaves, autorizar aplicativos e gerenciar permissões.</span><span class="sxs-lookup"><span data-stu-id="4b014-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="4b014-108">Saiba mais sobre o [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="4b014-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="4b014-109">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="4b014-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="4b014-110">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="4b014-110">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="4b014-111">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4b014-111">Examples</span></span>

<span data-ttu-id="4b014-112">Recuperar uma [chave da Web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) de um Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="4b014-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```

<span data-ttu-id="4b014-113">De modo semelhante, você pode usar o trecho a seguir para recuperar um segredo do cofre:</span><span class="sxs-lookup"><span data-stu-id="4b014-113">Similarly, you can use the following snippet to retrieve a secret from the vault:</span></span>

```
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret("https://VAULT_ID.vault.azure.net/", "SECRET_ID", "SECRET_VERSION")

print(secret_bundle.value)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b014-114">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="4b014-114">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a><span data-ttu-id="4b014-115">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4b014-115">Management API</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="4b014-116">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4b014-116">Example</span></span>
<span data-ttu-id="4b014-117">O exemplo a seguir mostra como criar um Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4b014-117">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'

kv_client = KeyVaultManagementClient(credentials, subscription_id)

vault = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': os.environ['AZURE_TENANT_ID'],
            'access_policies': [{
                'tenant_id': os.environ['AZURE_TENANT_ID'],
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="4b014-118">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4b014-118">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b014-119">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4b014-119">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="4b014-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="4b014-120">Samples</span></span>
* <span data-ttu-id="4b014-121">[Gerenciar Cofres de Chaves][1]</span><span class="sxs-lookup"><span data-stu-id="4b014-121">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="4b014-122">[Recuperação do Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="4b014-122">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="4b014-123">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de exemplos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4b014-123">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
