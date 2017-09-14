---
title: Bibliotecas do Azure Active Directory para Python
description: "Documentação de referência para a biblioteca de cliente de Python para o Azure Active Directory"
keywords: "Azure, Python, SDK, API, SQL, autenticação, AAD, Active Directory, Graph, OAuth 2.0"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: active-directory
ms.openlocfilehash: 41234fd44fa98c1ff57287193b0437b7caca46c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-libraries-for-python"></a>Bibliotecas do Azure Active Directory para Python

## <a name="overview"></a>Visão geral

Conectar usuários e controlar o acesso a aplicativos e APIs com o [Azure Active Directory](/azure/active-directory/active-directory-whatis).

## <a name="client-library"></a>Biblioteca do cliente

Configurar a autenticação do OAuth2, OpenID Connect ou Active Directory Graph e conexão de acesso único [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) com a [biblioteca de autenticação do Azure Active Directory (ADAL) para Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).

```bash
pip install azure-graphrbac
```

### <a name="example"></a>Exemplo
> [!NOTE]
> Você precisa alterar o parâmetro do recurso para https://graph.windows.net ao criar a instância de credenciais

```python
from azure.graphrbac import GraphRbacManagementClient
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
            'user@domain.com',      # Your user
            'my_password',          # Your password
            resource="https://graph.windows.net"
    )

tenant_id = "myad.onmicrosoft.com"

graphrbac_client = GraphRbacManagementClient(
    credentials,
    tenant_id
)
```
O código a seguir cria um usuário, obtenha-o diretamente e pela filtragem da lista e, em seguida, exclua-o.
```python
from azure.graphrbac.models import UserCreateParameters, PasswordProfile

user = graphrbac_client.users.create(
    UserCreateParameters(
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),
        account_enabled=False,
        display_name='Test Buddy',
        mail_nickname='testbuddy',
        password_profile=PasswordProfile(
            password='MyStr0ngP4ssword',
            force_change_password_next_login=True
        )
    )
)
# user is a User instance
self.assertEqual(user.display_name, 'Test Buddy')

user = graphrbac_client.users.get(user.object_id)
self.assertEqual(user.display_name, 'Test Buddy')

for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"):
    self.assertEqual(user.display_name, 'Test Buddy')

graphrbac_client.users.delete(user.object_id)
```

> [!div class="nextstepaction"]
> [Explorar as APIs de cliente](/python/api/overview/azure/activedirectory/clientlibrary?)

Explorar mais [exemplos de código Python para o Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) que você pode usar nos seus aplicativos.