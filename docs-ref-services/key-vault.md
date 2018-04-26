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
ms.openlocfilehash: 1ac9cc92a4c830a8c156117d3e0d188b8032f29a
ms.sourcegitcommit: 42d868d89eb28a6fdceffccfa03e3209a755b812
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/20/2018
---
# <a name="azure-key-vault-libraries-for-python"></a>Bibliotecas do Azure Key Vault para Python

## <a name="overview"></a>Visão geral

Criar, atualizar e excluir chaves e segredos no Azure Key Vault com as bibliotecas de cliente.

Use as bibliotecas de gerenciamento do Azure Key Vault para criar cofres de chaves, autorizar aplicativos e gerenciar permissões. 

Saiba mais sobre o [Azure Key Vault](/azure/key-vault/key-vault-whatis).

## <a name="install-the-libraries"></a>Instalar as bibliotecas

### <a name="client-library"></a>Biblioteca do cliente

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Exemplos

Recuperar uma [chave da Web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) de um Cofre de Chaves.

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

De modo semelhante, você pode usar o trecho a seguir para recuperar um segredo do cofre:

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

[!div class="nextstepaction"]
[Explorar as APIs de cliente](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a>API de gerenciamento

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Exemplo
O exemplo a seguir mostra como criar um Azure Key Vault. 

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
> [Explorar as APIs de gerenciamento](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Exemplos
* [Gerenciar Cofres de Chaves][1] 
* [Recuperação do Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de exemplos do Azure Key Vault. 
