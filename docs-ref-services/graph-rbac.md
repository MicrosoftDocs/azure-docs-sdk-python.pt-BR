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
# <a name="azure-active-directory-graph-libraries-for-python"></a><span data-ttu-id="86202-104">Bibliotecas do Graph do Azure Active Directory para Python</span><span class="sxs-lookup"><span data-stu-id="86202-104">Azure Active Directory Graph libraries for Python</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="86202-105">Em fevereiro de 2019, iniciamos o processo de substituição de algumas versões anteriores da API do Graph do Azure Active Directory pela API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="86202-105">As of February 2019, we started the process to deprecate some earlier versions of Azure Active Directory Graph API in favor of the Microsoft Graph API.</span></span> 
>
> <span data-ttu-id="86202-106">Para saber mais detalhes, atualizações e períodos, confira [Microsoft Graph ou Graph do Azure AD](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) no Centro de Desenvolvimento do Office.</span><span class="sxs-lookup"><span data-stu-id="86202-106">For details, updates, and time frames, see [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) in the Office Dev Center.</span></span>
>
> <span data-ttu-id="86202-107">Mais adiante, os aplicativos devem usar a API do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="86202-107">Moving forward, applications should use the Microsoft Graph API.</span></span> 

## <a name="overview"></a><span data-ttu-id="86202-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="86202-108">Overview</span></span> 

<span data-ttu-id="86202-109">Conectar usuários e controlar o acesso a aplicativos e APIs com o [Graph do Active Directory](/azure/active-directory/develop/active-directory-graph-apis).</span><span class="sxs-lookup"><span data-stu-id="86202-109">Sign-on users and control access to applications and APIs with [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-apis).</span></span>   

## <a name="client-library"></a><span data-ttu-id="86202-110">Biblioteca do cliente</span><span class="sxs-lookup"><span data-stu-id="86202-110">Client library</span></span>   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a><span data-ttu-id="86202-111">Exemplo</span><span class="sxs-lookup"><span data-stu-id="86202-111">Example</span></span> 
> [!NOTE]   
> <span data-ttu-id="86202-112">Você precisa alterar o parâmetro do recurso para https://graph.windows.net ao criar a instância de credenciais</span><span class="sxs-lookup"><span data-stu-id="86202-112">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>    
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
<span data-ttu-id="86202-113">O código a seguir cria um usuário, obtenha-o diretamente e pela filtragem da lista e, em seguida, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="86202-113">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>   
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