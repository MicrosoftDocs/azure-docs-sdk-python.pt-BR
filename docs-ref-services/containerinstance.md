---
title: Bibliotecas de Instâncias de Contêiner do Azure para Python
description: Referência para bibliotecas de Instâncias de Contêiner do Azure para Python
keywords: Azure, python, SDK, API, ACI, contêiner, instâncias
author: mmacy
manager: jeconnoc
ms.date: 06/04/2018
ms.author: marsma
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 09f39375e0e92b6d09a965c3972d772a1437d0d4
ms.sourcegitcommit: 8c70bfd95309c3a77a4c0f73373c1785d59cdd10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34761317"
---
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="e6a5e-104">Bibliotecas de Instâncias de Contêiner do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="e6a5e-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="e6a5e-105">Use as bibliotecas de Instâncias de Contêiner do Microsoft Azure para Python para criar e gerenciar as instâncias de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="e6a5e-106">Saiba mais lendo a [Visão geral das Instâncias de Contêiner do Azure](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="e6a5e-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="e6a5e-107">APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e6a5e-107">Management APIs</span></span>

<span data-ttu-id="e6a5e-108">Use a biblioteca de gerenciamento para criar e gerenciar instâncias de contêiner do Azure no Azure.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="e6a5e-109">Instalar o pacote de gerenciamento com pip:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="e6a5e-110">Fonte de exemplo</span><span class="sxs-lookup"><span data-stu-id="e6a5e-110">Example source</span></span>

<span data-ttu-id="e6a5e-111">Se quiser ver os seguintes exemplos de código em contexto, você pode encontrá-los no repositório do GitHub a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="e6a5e-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="e6a5e-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="e6a5e-113">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e6a5e-113">Authentication</span></span>

<span data-ttu-id="e6a5e-114">Uma das maneiras mais fáceis para autenticar clientes SDK (como os clientes de Instâncias de Contêiner do Azure e do Gerenciador de Recursos no exemplo a seguir) é com a [autenticação baseada em arquivo](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span><span class="sxs-lookup"><span data-stu-id="e6a5e-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="e6a5e-115">A autenticação baseada em arquivo consulta a variável de ambiente `AZURE_AUTH_LOCATION` para o caminho para um arquivo de credenciais.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="e6a5e-116">Para usar a autenticação baseada em arquivo:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="e6a5e-117">Criar um arquivo de credenciais com a [CLI do Azure](/cli/azure) ou o [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="e6a5e-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="e6a5e-118">Se você usar o [Cloud Shell](https://shell.azure.com/) para gerar o arquivo de credenciais, copie o conteúdo em um arquivo local onde seu aplicativo Python possa acessar.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="e6a5e-119">Defina a variável de ambiente `AZURE_AUTH_LOCATION` para o caminho completo do arquivo de credenciais gerado.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="e6a5e-120">Por exemplo, (no Bash):</span><span class="sxs-lookup"><span data-stu-id="e6a5e-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="e6a5e-121">Depois que você criar o arquivo de credenciais e preencher a variável de ambiente `AZURE_AUTH_LOCATION`, use o método `get_client_from_auth_file` do módulo [client_factory][client_factory] para inicializar os objetos [ResourceManagementClient][ResourceManagementClient] e [ContainerInstanceManagementClient][ContainerInstanceManagementClient].</span><span class="sxs-lookup"><span data-stu-id="e6a5e-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

<span data-ttu-id="e6a5e-122">Para obter mais detalhes sobre os métodos de autenticação disponíveis nas bibliotecas de gerenciamento do Python para Azure, confira [Autenticar com Bibliotecas de Gerenciamento do Azure para Python](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="e6a5e-122">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="e6a5e-123">Criar grupo de contêineres - contêiner único</span><span class="sxs-lookup"><span data-stu-id="e6a5e-123">Create container group - single container</span></span>

<span data-ttu-id="e6a5e-124">Este exemplo cria um grupo de contêineres com um único contêiner</span><span class="sxs-lookup"><span data-stu-id="e6a5e-124">This example creates a container group with a single container</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="e6a5e-125">Criar grupo de contêineres - vários contêineres</span><span class="sxs-lookup"><span data-stu-id="e6a5e-125">Create container group - multiple containers</span></span>

<span data-ttu-id="e6a5e-126">Este exemplo cria um grupo de contêineres com dois contêineres: um contêiner do aplicativo e um secundário.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-126">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="e6a5e-127">Criar grupo de contêineres baseado em tarefas</span><span class="sxs-lookup"><span data-stu-id="e6a5e-127">Create task-based container group</span></span>

<span data-ttu-id="e6a5e-128">Este exemplo cria um grupo de contêineres com um único contêiner baseado em tarefas.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-128">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="e6a5e-129">Este exemplo demonstra vários recursos:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-129">This example demonstrates several features:</span></span>

* <span data-ttu-id="e6a5e-130">[Substituição de linha de comando](/azure/container-instances/container-instances-restart-policy#command-line-override) - uma linha de comando personalizada, diferente da que é especificada na linha `CMD` do Dockerfile do contêiner, é especificada.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-130">[Command line override](/azure/container-instances/container-instances-restart-policy#command-line-override) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="e6a5e-131">A substituição de linha de comando permite que você especifique uma linha de comando personalizada para executar na inicialização do contêiner, substituindo a linha de comando padrão salva no contêiner.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-131">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="e6a5e-132">Sobre a execução de vários comandos na inicialização do contêiner, aplica-se o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-132">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="e6a5e-133">Se você quiser executar um **único comando** com vários argumentos da linha de comando, por exemplo `echo FOO BAR`, deve fornecê-los como uma lista de cadeia de caracteres para a propriedade `command` do [Contêiner][Container].</span><span class="sxs-lookup"><span data-stu-id="e6a5e-133">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="e6a5e-134">Por exemplo: </span><span class="sxs-lookup"><span data-stu-id="e6a5e-134">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="e6a5e-135">Se, no entanto, quiser executar **vários comandos** com (potencialmente) vários argumentos, deve executar um shell e passar os comandos em cadeia como um argumento.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-135">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="e6a5e-136">Por exemplo, isso executa os comandos `echo` e `tail`:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-136">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="e6a5e-137">[Variáveis de ambiente](/azure/container-instances/container-instances-environment-variables) - Duas variáveis de ambiente são especificadas para o contêiner no grupo de contêiner.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-137">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="e6a5e-138">Use variáveis de ambiente para modificar o comportamento de script ou aplicativo em tempo de execução ou, caso contrário, passar informações dinâmicas para um aplicativo em execução no contêiner.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-138">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="e6a5e-139">[Reiniciar política](/azure/container-instances/container-instances-restart-policy) - O contêiner está configurado com uma política de reinicialização de "Nunca", útil para contêineres baseados em tarefas que são executados como parte de um trabalho em lotes.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="e6a5e-140">Operação de pesquisa com [AzureOperationPoller][AzureOperationPoller] - Depois que o método de criação é chamado, a operação é sondada para determinar quando ele for concluído e logs do grupo de contêiner podem ser obtidos.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-140">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="e6a5e-141">Listar grupos de contêineres</span><span class="sxs-lookup"><span data-stu-id="e6a5e-141">List container groups</span></span>

<span data-ttu-id="e6a5e-142">Este exemplo lista os grupos de contêineres em um grupo de recursos e, em seguida, imprime algumas de suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-142">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="e6a5e-143">Ao listar grupos de contêineres, o [instance_view][instance_view] de cada grupo retornado é `None`.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-143">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="e6a5e-144">Para obter os detalhes dos contêineres dentro de um grupo de contêineres, você deve [obter][containergroupoperations_get] o grupo de contêineres, que retorna o grupo com sua propriedade `instance_view` preenchida.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-144">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="e6a5e-145">Confira a próxima seção, [Obter um grupo existente do contêiner](#get-an-existing-container-group), para obter um exemplo de iteração em contêineres do grupo de contêineres em seu `instance_view`.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-145">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="e6a5e-146">Obter um grupo de contêineres existente</span><span class="sxs-lookup"><span data-stu-id="e6a5e-146">Get an existing container group</span></span>

<span data-ttu-id="e6a5e-147">Este exemplo obtém um grupo de contêineres específico de um grupo de recursos e, em seguida, imprime algumas de suas propriedades (incluindo os contêineres) e os valores.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-147">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="e6a5e-148">A [operação get][containergroupoperations_get] retorna um grupo de contêineres com sua [instance_view][instance_view] preenchida, que permite iterar com cada contêiner no grupo.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-148">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="e6a5e-149">Somente a operação `get` preenche a propriedade `instance_vew` do grupo de contêineres – listar os grupos de contêineres em um assinatura ou grupo de recursos não preenche a exibição de instância devido à natureza potencialmente cara da operação (por exemplo, ao listar centenas de grupos de contêineres, cada uma contendo potencialmente vários contêineres).</span><span class="sxs-lookup"><span data-stu-id="e6a5e-149">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="e6a5e-150">Como mencionado anteriormente na seção [Listar grupos de contêineres](#list-container-groups), após um `list`, você deve subsequentemente `get` um grupo de contêineres específico para obter detalhes da instância de seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-150">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="e6a5e-151">Excluir um grupo de contêineres</span><span class="sxs-lookup"><span data-stu-id="e6a5e-151">Delete a container group</span></span>

<span data-ttu-id="e6a5e-152">Este exemplo exclui vários grupos de contêineres de um grupo de recursos, além do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-152">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a><span data-ttu-id="e6a5e-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6a5e-153">Next steps</span></span>

* <span data-ttu-id="e6a5e-154">O código-fonte para os exemplos anteriores pode ser encontrado no GitHub:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-154">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="e6a5e-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="e6a5e-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="e6a5e-156">Mais exemplos de código das Instâncias de Contêiner do Azure:</span><span class="sxs-lookup"><span data-stu-id="e6a5e-156">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="e6a5e-157">[Exemplos de Código do Azure][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="e6a5e-157">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="e6a5e-158">Explore mais [exemplos de código de Python][samples-python] que você pode usar em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e6a5e-158">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e6a5e-159">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="e6a5e-159">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient