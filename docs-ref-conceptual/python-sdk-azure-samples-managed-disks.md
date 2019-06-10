---
title: Managed Disks
description: Criar, redimensionar e atualizar um disco gerenciado.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: bee17efdb90d6365acb2adbf9c01d1f7e843da42
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376856"
---
# <a name="managed-disks"></a><span data-ttu-id="e59af-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e59af-103">Managed Disks</span></span>

<span data-ttu-id="e59af-104">O Azure Managed Disks oferece um gerenciamento de discos simplificado, escalabilidade aprimorada, segurança e escala melhores.</span><span class="sxs-lookup"><span data-stu-id="e59af-104">Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="e59af-105">Ele retira a noção de conta de armazenamento para discos, permitindo que os clientes façam o dimensionamento sem se preocupar com as limitações associadas às contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e59af-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="e59af-106">Esta postagem fornece uma breve introdução e referência sobre o consumo do serviço do Python.</span><span class="sxs-lookup"><span data-stu-id="e59af-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>

<span data-ttu-id="e59af-107">Da perspectiva do desenvolvedor, a experiência do Managed Disks experiência na CLI do Azure é única em relação à linguagem quando comparada com a CLI em outras ferramentas de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="e59af-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="e59af-108">Você pode usar o SDK do [Azure Python](https://azure.microsoft.com/develop/python/) e o [pacote do azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) para administrar Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e59af-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="e59af-109">Você pode criar um cliente de computação usando este [tutorial](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="e59af-109">You can create a compute client using this [tutorial](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span></span>

## <a name="standalone-managed-disks"></a><span data-ttu-id="e59af-110">Managed Disks Autônomos</span><span class="sxs-lookup"><span data-stu-id="e59af-110">Standalone Managed Disks</span></span>

<span data-ttu-id="e59af-111">Você pode facilmente criar Managed Disks autônomos de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="e59af-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="e59af-112">Criar um Managed Disk vazio</span><span class="sxs-lookup"><span data-stu-id="e59af-112">Create an empty Managed Disk</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="e59af-113">Criar um Managed Disk com base no armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="e59af-113">Create a Managed Disk from blob storage</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="e59af-114">Criar um Managed Disk com base na sua própria imagem</span><span class="sxs-lookup"><span data-stu-id="e59af-114">Create a Managed Disk from your own image</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="e59af-115">Máquina virtual com Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e59af-115">Virtual machine with Managed Disks</span></span>

<span data-ttu-id="e59af-116">Você pode criar uma Máquina Virtual com um Managed Disk implícito para uma imagem de disco específica.</span><span class="sxs-lookup"><span data-stu-id="e59af-116">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="e59af-117">A criação foi simplificada com a criação implícita de Managed Disks sem especificar todos os detalhes de disco.</span><span class="sxs-lookup"><span data-stu-id="e59af-117">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="e59af-118">Você não precisa se preocupar com a criação e gerenciamento das Contas de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e59af-118">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="e59af-119">Um Managed Disk é criado implicitamente ao criar a VM a partir de uma imagem do sistema operacional no Azure.</span><span class="sxs-lookup"><span data-stu-id="e59af-119">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="e59af-120">No parâmetro ``storage_profile``, ``os_disk`` agora é opcional e você não precisa criar uma conta de armazenamento como uma pré-condição necessária para criar uma Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="e59af-120">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
```

<span data-ttu-id="e59af-121">Esse parâmetro ``storage_profile`` é opcional.</span><span class="sxs-lookup"><span data-stu-id="e59af-121">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="e59af-122">Para obter um exemplo completo sobre como criar uma VM em Python (inclusive rede, etc), verifique o [tutorial de VM no Python](https://github.com/Azure-Samples/virtual-machines-python-manage) completo.</span><span class="sxs-lookup"><span data-stu-id="e59af-122">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="e59af-123">Você pode facilmente anexar um Managed Disk provisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e59af-123">You can easily attach a previously provisioned Managed Disk.</span></span>

```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="e59af-124">Conjuntos de Dimensionamento de Máquinas Virtuais com Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e59af-124">Virtual machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="e59af-125">Antes dos Managed Disks, é necessário criar uma conta de armazenamento manualmente para todas as VMs que você deseja dentro dp seu Conjunto de Dimensionamento e, em seguida, usar o parâmetro de lista ``vhd_containers`` para fornecer todo o nome da conta de armazenamento para o API REST do Conjunto de Dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e59af-125">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="e59af-126">O guia de transição oficial está disponível neste artigo `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span><span class="sxs-lookup"><span data-stu-id="e59af-126">The official transition guide is available in this article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span></span>

<span data-ttu-id="e59af-127">Agora com o Managed Disk, você não precisa gerenciar nenhuma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e59af-127">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="e59af-128">Se você estiver acostumado com o para o SDK de Python VMSS, seu ``storage_profile`` agora pode ser exatamente o mesmo que aquele usado na criação da VM:</span><span class="sxs-lookup"><span data-stu-id="e59af-128">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

<span data-ttu-id="e59af-129">O exemplo completo sendo:</span><span class="sxs-lookup"><span data-stu-id="e59af-129">The full sample being:</span></span>

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
```

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="e59af-130">Outras operações com Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e59af-130">Other operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="e59af-131">Redimensionar um Managed Disk</span><span class="sxs-lookup"><span data-stu-id="e59af-131">Resizing a Managed Disk</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="e59af-132">Atualizar o tipo de conta de armazenamento dos Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e59af-132">Update the storage account type of the Managed Disks</span></span>

```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-nlob-storage"></a><span data-ttu-id="e59af-133">Criar uma imagem usando um armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="e59af-133">Create an image from nlob storage</span></span>

```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="e59af-134">Criar um instantâneo de um Managed Disk que está atualmente anexado a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e59af-134">Create a snapshot of a Managed Disk that is currently attached to a virtual machine</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```
