---
title: Bibliotecas do Azure Monitor para Python
description: "Referência para bibliotecas de Monitoramento do Azure para Python"
keywords: Azure, Python, SDK, API, Monitoramento
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51cdf73060caeb74c587d932eb70c3fd3a2d3b71
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="78533-104">Bibliotecas do Azure Monitor para Python</span><span class="sxs-lookup"><span data-stu-id="78533-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="78533-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="78533-105">Overview</span></span> 
<span data-ttu-id="78533-106">O monitoramento fornece dados para garantir que seu aplicativo permaneça ativo e em execução em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="78533-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="78533-107">Ele também ajuda a afastar os problemas potenciais ou solucionar problemas antigos.</span><span class="sxs-lookup"><span data-stu-id="78533-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="78533-108">Além disso, você pode usar os dados de monitoramento para obter mais informações sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="78533-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="78533-109">Esse conhecimento pode ajudá-lo a melhorar o desempenho ou a capacidade de manutenção do aplicativo ou automatizar ações que normalmente exigiriam intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="78533-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="78533-110">Saiba mais sobre o Azure Monitor [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="78533-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="client"></a><span data-ttu-id="78533-111">Cliente</span><span class="sxs-lookup"><span data-stu-id="78533-111">Client</span></span>
```bash
pip install azure-monitor
```

### <a name="example"></a><span data-ttu-id="78533-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="78533-112">Example</span></span>
<span data-ttu-id="78533-113">Este exemplo obtém as métricas de um recurso no Azure (VMs, etc.).</span><span class="sxs-lookup"><span data-stu-id="78533-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> 

<span data-ttu-id="78533-114">Uma lista completa das palavras-chave disponíveis para filtros está disponível [aqui](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span><span class="sxs-lookup"><span data-stu-id="78533-114">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="78533-115">As métricas suportadas por tipo de recurso estão disponívelis [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span><span class="sxs-lookup"><span data-stu-id="78533-115">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.monitor import MonitorClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorClient(
    credentials,
    subscription_id
)

# You can get the available metrics of this specific resource
for metric in client.metric_definitions.list(resource_id):
    # azure.monitor.models.MetricDefinition
    print("{}: id={}, unit={}".format(
        metric.name.localized_value,
        metric.name.value,
        metric.unit
    ))

# Example of result for a VM:
# Percentage CPU: id=Percentage CPU, unit=Unit.percent
# Network In: id=Network In, unit=Unit.bytes
# Network Out: id=Network Out, unit=Unit.bytes
# Disk Read Bytes: id=Disk Read Bytes, unit=Unit.bytes
# Disk Write Bytes: id=Disk Write Bytes, unit=Unit.bytes
# Disk Read Operations/Sec: id=Disk Read Operations/Sec, unit=Unit.count_per_second
# Disk Write Operations/Sec: id=Disk Write Operations/Sec, unit=Unit.count_per_second

# Get CPU total of yesterday for this VM, by hour

today = datetime.datetime.now().date()
yesterday = today - datetime.timedelta(days=1)

filter = " and ".join([
    "name.value eq 'Percentage CPU'",
    "aggregationType eq 'Total'",
    "startTime eq {}".format(yesterday),
    "endTime eq {}".format(today),
    "timeGrain eq duration'PT1H'"
])

metrics_data = client.metrics.list(
    resource_id,
    filter=filter
)

for item in metrics_data:
    # azure.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for data in item.data:
        # azure.monitor.models.MetricData
        print("{}: {}".format(data.time_stamp, data.total))

# Example of result:
# Percentage CPU (percent)
# 2016-11-16 00:00:00+00:00: 72.0
# 2016-11-16 01:00:00+00:00: 90.59
# 2016-11-16 02:00:00+00:00: 60.58
# 2016-11-16 03:00:00+00:00: 65.78
# 2016-11-16 04:00:00+00:00: 43.96
# 2016-11-16 05:00:00+00:00: 43.96
# 2016-11-16 06:00:00+00:00: 114.9
# 2016-11-16 07:00:00+00:00: 45.4
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="78533-116">Explorar as APIs de cliente</span><span class="sxs-lookup"><span data-stu-id="78533-116">Explore the Client APIs</span></span>](/python/api/overview/azure/monitoring/clientlibrary)

## <a name="mangement-api"></a><span data-ttu-id="78533-117">API de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="78533-117">Mangement API</span></span>
```bash
pip install azure-mgmt-monitor
```

### <a name="example"></a><span data-ttu-id="78533-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="78533-118">Example</span></span>
<span data-ttu-id="78533-119">Este exemplo mostra como configurar de modo automático alertas sobre os recursos quando eles são criados para garantir que todos os recursos sejam monitorados corretamente.</span><span class="sxs-lookup"><span data-stu-id="78533-119">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="78533-120">Criar uma fonte de dados em uma VM para alertar sobre o uso da CPU:</span><span class="sxs-lookup"><span data-stu-id="78533-120">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
monitor_mgmt_client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="78533-121">Crie uma condição de limite que dispara quando o uso médio de CPU de uma máquina virtual para os últimos 5 minutos está acima de 90% (usando a fonte de dados anterior):</span><span class="sxs-lookup"><span data-stu-id="78533-121">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
```python
from azure.mgmt.monitor.models import ThresholdRuleCondition

# I need a subclasses of "RuleCondition"
rule_condition = ThresholdRuleCondition(
    data_source = data_source,
    operator = 'GreaterThanOrEqual',
    threshold = 90,
    window_size = 'PT5M',
    time_aggregation = 'Average'
)
```

<span data-ttu-id="78533-122">Criar uma ação de email:</span><span class="sxs-lookup"><span data-stu-id="78533-122">Create an email action:</span></span>
```python
from azure.mgmt.monitor.models import RuleEmailAction

# I need a subclass of "RuleAction"
rule_action = RuleEmailAction(
    send_to_service_owners = True,
    custom_emails = [
        'monitoringemail@microsoft.com'
    ]
)
```

<span data-ttu-id="78533-123">Criar o alerta:</span><span class="sxs-lookup"><span data-stu-id="78533-123">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = monitor_mgmt_client.alert_rules.create_or_update(
    group_name,
    rule_name,
    {
        'location': 'westus',
        'alert_rule_resource_name': rule_name,
        'description': 'Testing Alert rule creation',
        'is_enabled': True,
        'condition': rule_condition,
        'actions': [
            rule_action
        ]
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="78533-124">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="78533-124">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/managementlibrary)