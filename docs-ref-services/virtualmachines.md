---
title: Bibliotecas de Máquina Virtual do Azure para Python
description: ''
keywords: Azure, Python, SDK, API, Computação, Máquinas Virtuais
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: adea3dfd1e38fb8c880009d5a02ab2b8be2a67e1
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478819"
---
# <a name="azure-virtual-machine-libraries"></a>Bibliotecas de máquina virtual do Azure

## <a name="overview"></a>Visão geral

Recursos de computação escalonáveis, sob demanda que executam Linux ou Windows.

Para começar a usar Máquinas Virtuais do Azure, consulte [Criar uma máquina virtual Linux com o portal do Azure](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de gerenciamento

Criar, configurar, gerenciar e expandir máquinas virtuais Windows e Linux no Azure a partir do seu código com a API de gerenciamento.

Instalar a biblioteca por meio de PIP.

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a>Exemplo

Crie uma nova máquina virtual Linux em um grupo de recursos do Azure existente com a autenticação MSI (Identidade do Serviço Gerenciada).

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
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a>Exemplos

* [Gerenciar redes virtuais][1]
* [Autenticar com a Identidade do serviço Gerenciada][2]
* [Criar uma máquina virtual com a Extensão de Identidade do Serviço Gerenciado][3]
* [Gerenciar um balanceador de carga][4]
* [Criar e configurar discos gerenciados][5]
* [Listar imagens][6] 
* [Monitorar máquinas virtuais][7]

Veja a [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de exemplos de máquina virtual.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md