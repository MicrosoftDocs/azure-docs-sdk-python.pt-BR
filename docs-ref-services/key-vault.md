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
# <a name="azure-key-vault-libraries-for-python"></a>Bibliotecas do Azure Key Vault para Python

O [Azure Key Vault](/azure/key-vault/) é o sistema de armazenamento e gerenciamento do Azure para gerenciamento de chaves criptográficas, segredos e certificados. A API do SDK do Python para o Key Vault é dividida entre as bibliotecas de cliente e as bibliotecas de gerenciamento.

Use a biblioteca de clientes para:
- Acessar, atualizar ou excluir itens armazenados em um Azure Key Vault
- Obter metadados para certificados armazenados
- Verificar assinaturas em relação às chaves simétricas no key Vault

Use a biblioteca de gerenciamento para:
- Criar, atualizar ou excluir novos armazenamentos do Key Vault
- Controlar as políticas de acesso a cofres
- Listar os cofres por assinatura ou grupo de recursos
- Verificar a disponibilidade dos nomes de cofre

## <a name="install-the-libraries"></a>Instalar as bibliotecas

### <a name="client-library"></a>Biblioteca do cliente

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Exemplos

Os exemplos a seguir usam a autenticação por entidade de serviço, que é o método de entrada recomendado para aplicativos que se conectam ao Azure. Para saber mais sobre a autenticação por entidade de serviço, consulte [Autenticação com o SDK do Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)

Recuperar a parte pública de uma chave assimétrica de um cofre:

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

Recuperar um segredo de um cofre:

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
> [Explorar as APIs de cliente](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>Biblioteca de gerenciamento

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Exemplo

O exemplo a seguir mostra como criar um Azure Key Vault. 

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Exemplos
* [Gerenciar Azure Key Vaults][1] 
* [Recuperação do Azure Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de exemplos do Azure Key Vault. 
