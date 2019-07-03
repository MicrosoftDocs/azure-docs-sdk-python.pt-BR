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
ms.openlocfilehash: e9b0aba7998565284ae18e0036da96d033b2b05f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534271"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a><span data-ttu-id="5de38-104">Bibliotecas do Graph do Azure Active Directory para Python</span><span class="sxs-lookup"><span data-stu-id="5de38-104">Azure Active Directory Graph libraries for Python</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="5de38-105">Em fevereiro de 2019, iniciamos o processo de substituição de algumas versões anteriores da API do Graph do Azure Active Directory pela API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="5de38-105">As of February 2019, we started the process to deprecate some earlier versions of Azure Active Directory Graph API in favor of the Microsoft Graph API.</span></span> 
>
> <span data-ttu-id="5de38-106">Para saber mais detalhes, atualizações e períodos, confira [Microsoft Graph ou Graph do Azure AD](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) no Centro de Desenvolvimento do Office.</span><span class="sxs-lookup"><span data-stu-id="5de38-106">For details, updates, and time frames, see [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) in the Office Dev Center.</span></span>
>
> <span data-ttu-id="5de38-107">Mais adiante, os aplicativos devem usar a API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="5de38-107">Moving forward, applications should use the Microsoft Graph API.</span></span> 

## <a name="overview"></a><span data-ttu-id="5de38-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5de38-108">Overview</span></span> 

<span data-ttu-id="5de38-109">Conectar usuários e controlar o acesso a aplicativos e APIs com o [Graph do Active Directory](/azure/active-directory/develop/active-directory-graph-api).</span><span class="sxs-lookup"><span data-stu-id="5de38-109">Sign-on users and control access to applications and APIs with [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).</span></span>    

## <a name="client-library"></a><span data-ttu-id="5de38-110">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="5de38-110">Client library</span></span>   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a><span data-ttu-id="5de38-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5de38-111">Example</span></span> 
> [!NOTE]   
> <span data-ttu-id="5de38-112">Você precisa alterar o parâmetro do recurso para https://graph.windows.net ao criar a instância de credenciais</span><span class="sxs-lookup"><span data-stu-id="5de38-112">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>    
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
<span data-ttu-id="5de38-113">O código a seguir cria um usuário, obtenha-o diretamente e pela filtragem da lista e, em seguida, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="5de38-113">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>   
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