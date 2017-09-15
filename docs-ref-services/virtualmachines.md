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
ms.openlocfilehash: e2f2ad4e42bd847c9286333bacd583c3cd3f1b8c
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="04df4-103">Bibliotecas de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="04df4-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="04df4-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="04df4-104">Overview</span></span>

<span data-ttu-id="04df4-105">Recursos de computação escalonáveis, sob demanda que executam Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="04df4-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="04df4-106">Para começar a usar Máquinas Virtuais do Azure, consulte [Criar uma máquina virtual Linux com o portal do Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="04df4-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="04df4-107">API de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="04df4-107">Management API</span></span>

<span data-ttu-id="04df4-108">Criar, configurar, gerenciar e expandir máquinas virtuais Windows e Linux no Azure a partir do seu código com a API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="04df4-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="04df4-109">Instalar a biblioteca por meio de PIP.</span><span class="sxs-lookup"><span data-stu-id="04df4-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="04df4-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="04df4-110">Example</span></span>

<span data-ttu-id="04df4-111">Crie uma nova máquina virtual Linux em um grupo de recursos do Azure existente com a autenticação MSI (Identidade do Serviço Gerenciada).</span><span class="sxs-lookup"><span data-stu-id="04df4-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

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
> [<span data-ttu-id="04df4-112">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="04df4-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a><span data-ttu-id="04df4-113">Exemplos</span><span class="sxs-lookup"><span data-stu-id="04df4-113">Samples</span></span>

* <span data-ttu-id="04df4-114">[Gerenciar redes virtuais][1]</span><span class="sxs-lookup"><span data-stu-id="04df4-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="04df4-115">[Autenticar com a Identidade do serviço Gerenciada][2]</span><span class="sxs-lookup"><span data-stu-id="04df4-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="04df4-116">[Gerenciar um balanceador de carga][3]</span><span class="sxs-lookup"><span data-stu-id="04df4-116">[Manage a load balancer][3]</span></span>
* <span data-ttu-id="04df4-117">[Criar e configurar discos gerenciados][4]</span><span class="sxs-lookup"><span data-stu-id="04df4-117">[Create and configure managed disks][4]</span></span>
* <span data-ttu-id="04df4-118">[Listar imagens][5]</span><span class="sxs-lookup"><span data-stu-id="04df4-118">[List images][5]</span></span> 
* <span data-ttu-id="04df4-119">[Monitorar máquinas virtuais][6]</span><span class="sxs-lookup"><span data-stu-id="04df4-119">[Monitor virtual machines][6]</span></span>

<span data-ttu-id="04df4-120">Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de exemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04df4-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md