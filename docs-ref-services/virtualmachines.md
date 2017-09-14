---
title: "Bibliotecas de Máquina Virtual do Azure para Python"
description: 
keywords: "Azure, Python, SDK, API, Computação, Máquinas Virtuais"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: c25665e19adb44c7112bf1533097ce1e6c739cb8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="bdf5b-103">Bibliotecas de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="bdf5b-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="bdf5b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bdf5b-104">Overview</span></span>

<span data-ttu-id="bdf5b-105">Recursos de computação escalonáveis, sob demanda que executam Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="bdf5b-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="bdf5b-106">Para começar a usar Máquinas Virtuais do Azure, consulte [Criar uma máquina virtual Linux com o portal do Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="bdf5b-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="bdf5b-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="bdf5b-107">Management API</span></span>

<span data-ttu-id="bdf5b-108">Criar, configurar, gerenciar e expandir máquinas virtuais Windows e Linux no Azure a partir do seu código com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bdf5b-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="bdf5b-109">Instalar a biblioteca por meio de PIP.</span><span class="sxs-lookup"><span data-stu-id="bdf5b-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="bdf5b-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bdf5b-110">Example</span></span>

<span data-ttu-id="bdf5b-111">Criar uma nova máquina virtual Linux em um grupo de recursos do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="bdf5b-111">Create a new Linux virtual machine in an existing Azure resource group.</span></span>

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bdf5b-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="bdf5b-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a><span data-ttu-id="bdf5b-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bdf5b-113">Samples</span></span>

* <span data-ttu-id="bdf5b-114">[Gerenciar redes virtuais][1]</span><span class="sxs-lookup"><span data-stu-id="bdf5b-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="bdf5b-115">[Gerenciar um balanceador de carga][2]</span><span class="sxs-lookup"><span data-stu-id="bdf5b-115">[Manage a load balancer][2]</span></span>
* <span data-ttu-id="bdf5b-116">[Criar e configurar discos gerenciados][3]</span><span class="sxs-lookup"><span data-stu-id="bdf5b-116">[Create and configure managed disks][3]</span></span>
* <span data-ttu-id="bdf5b-117">[Listar imagens][4]</span><span class="sxs-lookup"><span data-stu-id="bdf5b-117">[List images][4]</span></span> 
* <span data-ttu-id="bdf5b-118">[Monitorar máquinas virtuais][5]</span><span class="sxs-lookup"><span data-stu-id="bdf5b-118">[Monitor virtual machines][5]</span></span>

<span data-ttu-id="bdf5b-119">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de exemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bdf5b-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[3]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md