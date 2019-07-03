---
title: Criar um fluxo de trabalho do Aplicativo Lógico
description: Criar um fluxo de trabalho do Aplicativo Lógico
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: routlaw
ms.openlocfilehash: 31cf9755abe24cb1ef5c1c1c5aec8301abde2220
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534424"
---
# <a name="create-a-logic-app-workflow"></a><span data-ttu-id="aa160-103">Criar um fluxo de trabalho do Aplicativo Lógico</span><span class="sxs-lookup"><span data-stu-id="aa160-103">Create a Logic App Workflow</span></span>

<span data-ttu-id="aa160-104">O código a seguir cria um fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="aa160-104">The following code creates a logic app workflow.</span></span>

```python
from azure.mgmt.logic.models import Workflow

group_name = 'myresourcegroup'
workflow_name = '12HourHeartBeat'
logic_client.workflows.create_or_update(
    group_name,
    workflow_name,
    Workflow(
        location = 'East US',
        definition={
            "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {},
            "triggers": {},
            "actions": {},
            "outputs": {}
        }
    )
)
```

