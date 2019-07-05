---
title: Bibliotecas de Instâncias de Contêiner do Azure para Python
description: Referência para bibliotecas de Instâncias de Contêiner do Azure para Python
keywords: Azure, python, SDK, API, ACI, contêiner, instâncias
author: dlepow
manager: jeconnoc
ms.date: 04/15/2019
ms.author: danlep
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 19e0e629253462f77d58740857b853d1c94d53cf
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534328"
---
# <a name="azure-container-instances-libraries-for-python"></a>Bibliotecas de Instâncias de Contêiner do Azure para Python

Use as bibliotecas de Instâncias de Contêiner do Microsoft Azure para Python para criar e gerenciar as instâncias de contêiner do Azure. Saiba mais lendo a [Visão geral das Instâncias de Contêiner do Azure](/azure/container-instances/container-instances-overview).

## <a name="management-apis"></a>APIs de gerenciamento

Use a biblioteca de gerenciamento para criar e gerenciar instâncias de contêiner do Azure no Azure.

Instalar o pacote de gerenciamento com pip:

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>Fonte de exemplo

Se quiser ver os seguintes exemplos de código em contexto, você pode encontrá-los no repositório do GitHub a seguir:

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Authentication

Uma das maneiras mais fáceis para autenticar clientes SDK (como os clientes de Instâncias de Contêiner do Azure e do Gerenciador de Recursos no exemplo a seguir) é com a [autenticação baseada em arquivo](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file). A autenticação baseada em arquivo consulta a variável de ambiente `AZURE_AUTH_LOCATION` para o caminho para um arquivo de credenciais. Para usar a autenticação baseada em arquivo:

1. Criar um arquivo de credenciais com a [CLI do Azure](/cli/azure) ou o [Cloud Shell](https://shell.azure.com/):

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Se você usar o [Cloud Shell](https://shell.azure.com/) para gerar o arquivo de credenciais, copie o conteúdo em um arquivo local onde seu aplicativo Python possa acessar.

2. Defina a variável de ambiente `AZURE_AUTH_LOCATION` para o caminho completo do arquivo de credenciais gerado. Por exemplo, (no Bash):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Depois que você criar o arquivo de credenciais e preencher a variável de ambiente `AZURE_AUTH_LOCATION`, use o método `get_client_from_auth_file` dos objetos [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] e [ContainerInstanceManagementClient][ContainerInstanceManagementClient].

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Para obter mais detalhes sobre os métodos de autenticação disponíveis nas bibliotecas de gerenciamento do Python para Azure, confira [Autenticar com Bibliotecas de Gerenciamento do Azure para Python](/python/azure/python-sdk-azure-authenticate).

## <a name="create-container-group---single-container"></a>Criar grupo de contêineres - contêiner único

Este exemplo cria um grupo de contêineres com um único contêiner

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Criar grupo de contêineres - vários contêineres

Este exemplo cria um grupo de contêineres com dois contêineres: um contêiner do aplicativo e um secundário.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>Criar grupo de contêineres baseado em tarefas

Este exemplo cria um grupo de contêineres com um único contêiner baseado em tarefas. Este exemplo demonstra vários recursos:

* [Substituição de linha de comando](/azure/container-instances/container-instances-start-command) - uma linha de comando personalizada, diferente da que é especificada na linha `CMD` do Dockerfile do contêiner, é especificada. A substituição de linha de comando permite que você especifique uma linha de comando personalizada para executar na inicialização do contêiner, substituindo a linha de comando padrão salva no contêiner. Sobre a execução de vários comandos na inicialização do contêiner, aplica-se o seguinte:

   Se você quiser executar um **único comando** com vários argumentos da linha de comando, por exemplo `echo FOO BAR`, deve fornecê-los como uma lista de cadeia de caracteres para a propriedade `command` do [Contêiner][Container]. Por exemplo:

   `command = ['echo', 'FOO', 'BAR']`

   Se, no entanto, quiser executar **vários comandos** com (potencialmente) vários argumentos, deve executar um shell e passar os comandos em cadeia como um argumento. Por exemplo, isso executa os comandos `echo` e `tail`:

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [Variáveis de ambiente](/azure/container-instances/container-instances-environment-variables) - Duas variáveis de ambiente são especificadas para o contêiner no grupo de contêiner. Use variáveis de ambiente para modificar o comportamento de script ou aplicativo em tempo de execução ou, caso contrário, passar informações dinâmicas para um aplicativo em execução no contêiner.
* [Reiniciar política](/azure/container-instances/container-instances-restart-policy) - O contêiner está configurado com uma política de reinicialização de "Nunca", útil para contêineres baseados em tarefas que são executados como parte de um trabalho em lotes.
* Sondagem da operação com o [AzureOperationPoller][AzureOperationPoller] – Depois que o método de criação é chamado, a operação é sondada para determinar quando será concluída e os logs do grupo de contêineres poderão ser obtidos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a>Listar grupos de contêineres

Este exemplo lista os grupos de contêineres em um grupo de recursos e, em seguida, imprime algumas de suas propriedades.

Ao listar grupos de contêineres, o [instance_view][instance_view] de cada grupo retornado é `None`. Para obter os detalhes dos contêineres dentro de um grupo de contêineres, você deve [obter][containergroupoperations_get] o grupo de contêineres, que retorna o grupo com sua propriedade `instance_view` preenchida. Confira a próxima seção, [Obter um grupo existente do contêiner](#get-an-existing-container-group), para obter um exemplo de iteração em contêineres do grupo de contêineres em seu `instance_view`.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a>Obter um grupo de contêineres existente

Este exemplo obtém um grupo de contêineres específico de um grupo de recursos e, em seguida, imprime algumas de suas propriedades (incluindo os contêineres) e os valores.

A [operação get][containergroupoperations_get] returns a container group with its [instance_view][instance_view] preenchida, que permite iterar com cada contêiner no grupo. Somente a operação `get` preenche a propriedade `instance_vew` do grupo de contêineres – listar os grupos de contêineres em um assinatura ou grupo de recursos não preenche a exibição de instância devido à natureza potencialmente cara da operação (por exemplo, ao listar centenas de grupos de contêineres, cada uma contendo potencialmente vários contêineres). Como mencionado anteriormente na seção [Listar grupos de contêineres](#list-container-groups), após um `list`, você deve subsequentemente `get` um grupo de contêineres específico para obter detalhes da instância de seu contêiner.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a>Excluir um grupo de contêineres

Este exemplo exclui vários grupos de contêineres de um grupo de recursos, além do grupo de recursos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>Próximas etapas

* O código-fonte para os exemplos anteriores pode ser encontrado no GitHub:

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* Mais exemplos de código das Instâncias de Contêiner do Azure:

  [Exemplos de código do Azure][samples-aci]

* Explore mais [exemplos de código de Python][samples-python] que você pode usar em seus aplicativos.

> [!div class="nextstepaction"]
> [Explorar as APIs de gerenciamento](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get-resource-group-name--container-group-name--custom-headers-none--raw-false----operation-config-
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient