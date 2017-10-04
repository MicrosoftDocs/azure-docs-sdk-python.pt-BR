---
title: Managed Disks
description: Criar, redimensionar e atualizar um disco gerenciado.
author: lisawong19
manager: douge
ms.assetid: 
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: ca1af18ae37549238ffaafbd2d5f8223974e0d11
ms.sourcegitcommit: 12ea38af93cc4f1ba6aac333035829a69f6aed0c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2017
---
# <a name="managed-disks"></a>Managed Disks

O Managed Disks do Azure e 1000 VMs em um Conjunto de Dimensionamento agora estão [geralmente disponíveis](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). O Managed Disks do Azure fornece um Gerenciamento de disco simplificado, melhor Escalabilidade, maior Segurança e Escala. Ele retira a noção de conta de armazenamento para discos, permitindo que os clientes façam o dimensionamento sem se preocupar com as limitações associadas às contas de armazenamento. Esta postagem fornece uma breve introdução e referência sobre o consumo do serviço do Python.



Da perspectiva do desenvolvedor, a experiência do Managed Disks experiência na CLI do Azure é única em relação à linguagem quando comparada com a CLI em outras ferramentas de plataforma cruzada. Você pode usar o SDK do [Azure Python](https://azure.microsoft.com/develop/python/) e o [pacote do azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) para administrar Managed Disks. Você pode criar um cliente de computação usando este [tutorial](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html).


## <a name="standalone-managed-disks"></a>Managed Disks Autônomos

Você pode facilmente criar Managed Disks autônomos de várias maneiras.

### <a name="create-an-empty-managed-disk"></a>Criar um Managed Disk vazio.
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

### <a name="create-a-managed-disk-from-blob-storage"></a>Criar um Managed Disk a partir do Armazenamento de Blobs.
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

### <a name="create-a-managed-disk-from-your-own-image"></a>Criar um Managed Disk a partir da sua própria Imagem
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

## <a name="virtual-machine-with-managed-disks"></a>Máquina Virtual com Managed Disks

Você pode criar uma Máquina Virtual com um Managed Disk implícito para uma imagem de disco específica. A criação foi simplificada com a criação implícita de Managed Disks sem especificar todos os detalhes de disco. Você não precisa se preocupar com a criação e gerenciamento das Contas de Armazenamento.

Um Managed Disk é criado implicitamente ao criar a VM a partir de uma imagem do sistema operacional no Azure. No parâmetro ``storage_profile``, ``os_disk`` agora é opcional e você não precisa criar uma conta de armazenamento como uma pré-condição necessária para criar uma Máquina Virtual.

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
Esse parâmetro ``storage_profile`` é opcional. Para obter um exemplo completo sobre como criar uma VM em Python (inclusive rede, etc), verifique o [tutorial de VM no Python](https://github.com/Azure-Samples/virtual-machines-python-manage) completo.

Você pode facilmente anexar um Managed Disk provisionado anteriormente.
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

## <a name="virtual-machine-scale-sets-with-managed-disks"></a>Conjuntos de Dimensionamento de Máquina Virtual com Managed Disks

Antes dos Managed Disks, é necessário criar uma conta de armazenamento manualmente para todas as VMs que você deseja dentro dp seu Conjunto de Dimensionamento e, em seguida, usar o parâmetro de lista ``vhd_containers`` para fornecer todo o nome da conta de armazenamento para o API REST do Conjunto de Dimensionamento. O guia de transição oficial está disponível neste artigo `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`__.

Agora com o Managed Disk, você não precisa gerenciar nenhuma conta de armazenamento. Se você estiver acostumado com o para o SDK de Python VMSS, seu ``storage_profile`` agora pode ser exatamente o mesmo que aquele usado na criação da VM:

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

O exemplo completo sendo:

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

## <a name="other-operations-with-managed-disks"></a>Outras Operações com Managed Disks

### <a name="resizing-a-managed-disk"></a>Redimensionar um Managed Disk.

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

### <a name="update-the-storage-account-type-of-the-managed-disks"></a>Atualizar o tipo de Conta de Armazenamento dos Managed Disks.
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

### <a name="create-an-image-from-blob-storage"></a>Criar uma imagem usando um Armazenamento de Blobs.
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

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a>Criar um instantâneo de um Managed Disk que está atualmente conectado a uma Máquina Virtual.
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
