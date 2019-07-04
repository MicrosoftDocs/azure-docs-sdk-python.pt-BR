---
title: Bibliotecas do Azure Key Vault para Python
description: Documentação de referência para as bibliotecas de cliente de Python para o Azure Key Vault
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149332"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="538d8-103">Bibliotecas do Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="538d8-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="538d8-104">O [Azure Key Vault](/azure/key-vault/) é o sistema de armazenamento e gerenciamento do Azure para gerenciamento de chaves criptográficas, segredos e certificados.</span><span class="sxs-lookup"><span data-stu-id="538d8-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="538d8-105">A API do SDK do Python para o Key Vault é dividida entre as bibliotecas de cliente e as bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="538d8-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="538d8-106">Use a biblioteca de clientes para:</span><span class="sxs-lookup"><span data-stu-id="538d8-106">Use the client library to:</span></span>
- <span data-ttu-id="538d8-107">Acessar, atualizar ou excluir itens armazenados em um Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="538d8-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="538d8-108">Obter metadados para certificados armazenados</span><span class="sxs-lookup"><span data-stu-id="538d8-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="538d8-109">Verificar assinaturas em relação às chaves simétricas no key Vault</span><span class="sxs-lookup"><span data-stu-id="538d8-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="538d8-110">Use a biblioteca de gerenciamento para:</span><span class="sxs-lookup"><span data-stu-id="538d8-110">Use the management library to:</span></span>
- <span data-ttu-id="538d8-111">Criar, atualizar ou excluir novos armazenamentos do Key Vault</span><span class="sxs-lookup"><span data-stu-id="538d8-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="538d8-112">Controlar as políticas de acesso a cofres</span><span class="sxs-lookup"><span data-stu-id="538d8-112">Control vault access policies</span></span>
- <span data-ttu-id="538d8-113">Listar os cofres por assinatura ou grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="538d8-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="538d8-114">Verificar a disponibilidade dos nomes de cofre</span><span class="sxs-lookup"><span data-stu-id="538d8-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="538d8-115">Instalar as bibliotecas</span><span class="sxs-lookup"><span data-stu-id="538d8-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="538d8-116">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="538d8-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="538d8-117">Exemplos</span><span class="sxs-lookup"><span data-stu-id="538d8-117">Examples</span></span>

<span data-ttu-id="538d8-118">Os exemplos a seguir usam a autenticação por entidade de serviço, que é o método de entrada recomendado para aplicativos que se conectam ao Azure.</span><span class="sxs-lookup"><span data-stu-id="538d8-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="538d8-119">Para saber mais sobre a autenticação por entidade de serviço, consulte [Autenticação com o SDK do Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span><span class="sxs-lookup"><span data-stu-id="538d8-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="538d8-120">Recuperar a parte pública de uma chave assimétrica de um cofre:</span><span class="sxs-lookup"><span data-stu-id="538d8-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

<span data-ttu-id="538d8-121">Recuperar um segredo de um cofre:</span><span class="sxs-lookup"><span data-stu-id="538d8-121">Retrieve a secret from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="538d8-122">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="538d8-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="538d8-123">Biblioteca de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="538d8-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="538d8-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="538d8-124">Example</span></span>

<span data-ttu-id="538d8-125">O exemplo a seguir mostra como criar um Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="538d8-125">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="538d8-126">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="538d8-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="538d8-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="538d8-127">Samples</span></span>
* <span data-ttu-id="538d8-128">[Gerenciar Azure Key Vaults][1]</span><span class="sxs-lookup"><span data-stu-id="538d8-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="538d8-129">[Recuperação do Azure Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="538d8-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="538d8-130">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de exemplos do Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="538d8-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
