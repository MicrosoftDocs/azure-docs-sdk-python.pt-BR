---
title: Bibliotecas RBAC do Graph para Python
description: Referência para bibliotecas RBAC do Graph para Python
keywords: Azure, Python, SDK, API, RBAC do Graph
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 27238e00463ae30ec0e47e8c18497ffb9edac62c
ms.sourcegitcommit: 253c8d4b3dbc2bb76d1a273a757ab96ba37617a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65731532"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a>Bibliotecas do Graph do Azure Active Directory para Python

> [!IMPORTANT]
>
> Em fevereiro de 2019, iniciamos o processo de substituição de algumas versões anteriores da API do Graph do Azure Active Directory pela API do Microsoft Graph. 
>
> Para saber mais detalhes, atualizações e períodos, confira [Microsoft Graph ou Graph do Azure AD](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) no Centro de Desenvolvimento do Office.
>
> Mais adiante, os aplicativos devem usar a API do Microsoft Graph. 

## <a name="overview"></a>Visão geral 

Conectar usuários e controlar o acesso a aplicativos e APIs com o [Graph do Active Directory](/azure/active-directory/develop/active-directory-graph-apis).   

## <a name="client-library"></a>Biblioteca do cliente   

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