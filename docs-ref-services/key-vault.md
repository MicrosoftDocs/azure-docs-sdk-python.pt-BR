---
title: Bibliotecas do Azure Key Vault para Python
description: "Documentação de referência para as bibliotecas de cliente de Python para o Azure Key Vault"
author: lisawong19
keywords: "Azure, Python, SDK, API, Chaves, Key Vault, Autenticação, Segredo, chave, segurança"
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 6f0f1012839dad21fb8140dbbdf0f883d2877317
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="e3423-104">Bibliotecas do Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="e3423-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="e3423-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e3423-105">Overview</span></span>

<span data-ttu-id="e3423-106">Criar, atualizar e excluir chaves e segredos no Azure Key Vault com as bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="e3423-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="e3423-107">Use as bibliotecas de gerenciamento do Azure Key Vault para criar cofres de chaves, autorizar aplicativos e gerenciar permissões.</span><span class="sxs-lookup"><span data-stu-id="e3423-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="e3423-108">Saiba mais sobre o [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="e3423-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="e3423-109">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="e3423-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="e3423-110">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="e3423-110">Client library</span></span>
```bash
pip install azure-keyvault
```

## <a name="example"></a><span data-ttu-id="e3423-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e3423-111">Example</span></span>
<span data-ttu-id="e3423-112">Recuperar uma [chave da Web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) de um Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="e3423-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callack(server, resource, scope):
    credentials = credentials or ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = resource
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callack))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```
[!div class="nextstepaction"]
[<span data-ttu-id="e3423-113">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="e3423-113">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a><span data-ttu-id="e3423-114">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e3423-114">Management API</span></span>
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="e3423-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e3423-115">Example</span></span>
<span data-ttu-id="e3423-116">O exemplo a seguir mostra como criar um Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e3423-116">The following example shows how to create an Azure Key Vault.</span></span> 

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
> [<span data-ttu-id="e3423-117">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e3423-117">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3423-118">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e3423-118">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="e3423-119">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e3423-119">Samples</span></span>
* <span data-ttu-id="e3423-120">[Gerenciar Cofres de Chaves][1]</span><span class="sxs-lookup"><span data-stu-id="e3423-120">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="e3423-121">[Recuperação do Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="e3423-121">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="e3423-122">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de exemplos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e3423-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 