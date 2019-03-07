---
title: Bibliotecas do Azure Monitor para Python
description: Referência para bibliotecas de Monitoramento do Azure para Python
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
ms.openlocfilehash: 36746da246db2467b336a2eb14bfe2f6300b6ea4
ms.sourcegitcommit: 993aacad1d19d87533023f154c015d840723d716
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57528054"
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="bd37e-104">Bibliotecas do Azure Monitor para Python</span><span class="sxs-lookup"><span data-stu-id="bd37e-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="bd37e-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bd37e-105">Overview</span></span> 
<span data-ttu-id="bd37e-106">O monitoramento fornece dados para garantir que seu aplicativo permaneça ativo e em execução em um estado íntegro.</span><span class="sxs-lookup"><span data-stu-id="bd37e-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="bd37e-107">Ele também ajuda a afastar os problemas potenciais ou solucionar problemas antigos.</span><span class="sxs-lookup"><span data-stu-id="bd37e-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="bd37e-108">Além disso, você pode usar os dados de monitoramento para obter mais informações sobre seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd37e-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="bd37e-109">Esse conhecimento pode ajudá-lo a melhorar o desempenho ou a capacidade de manutenção do aplicativo ou automatizar ações que normalmente exigiriam intervenção manual.</span><span class="sxs-lookup"><span data-stu-id="bd37e-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="bd37e-110">Saiba mais sobre o Azure Monitor [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="bd37e-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="installation"></a><span data-ttu-id="bd37e-111">Instalação</span><span class="sxs-lookup"><span data-stu-id="bd37e-111">Installation</span></span>
```bash
pip install azure-mgmt-monitor
```

## <a name="example---metrics"></a><span data-ttu-id="bd37e-112">Exemplo - Métricas</span><span class="sxs-lookup"><span data-stu-id="bd37e-112">Example - Metrics</span></span>
<span data-ttu-id="bd37e-113">Este exemplo obtém as métricas de um recurso no Azure (VMs, etc.).</span><span class="sxs-lookup"><span data-stu-id="bd37e-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> <span data-ttu-id="bd37e-114">Este exemplo requer pelo menos a versão 0.4.0 do pacote do Python.</span><span class="sxs-lookup"><span data-stu-id="bd37e-114">This sample requires version 0.4.0 of the Python package at least.</span></span>

<span data-ttu-id="bd37e-115">Uma lista completa das palavras-chave disponíveis para filtros está disponível [aqui](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd37e-115">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="bd37e-116">As métricas suportadas por tipo de recurso estão disponívelis [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span><span class="sxs-lookup"><span data-stu-id="bd37e-116">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.mgmt.monitor import MonitorManagementClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorManagementClient(
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

metrics_data = client.metrics.list(
    resource_id,
    timespan="{}/{}".format(yesterday, today),
    interval='PT1H',
    metricnames='Percentage CPU',
    aggregation='Total'
)

for item in metrics_data.value:
    # azure.mgmt.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for timeserie in item.timeseries:
        for data in timeserie.data:
            # azure.mgmt.monitor.models.MetricData
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

## <a name="example---alerts"></a><span data-ttu-id="bd37e-117">Exemplo - Alertas</span><span class="sxs-lookup"><span data-stu-id="bd37e-117">Example - Alerts</span></span>
<span data-ttu-id="bd37e-118">Este exemplo mostra como configurar de modo automático alertas sobre os recursos quando eles são criados para garantir que todos os recursos sejam monitorados corretamente.</span><span class="sxs-lookup"><span data-stu-id="bd37e-118">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="bd37e-119">Criar uma fonte de dados em uma VM para alertar sobre o uso da CPU:</span><span class="sxs-lookup"><span data-stu-id="bd37e-119">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="bd37e-120">Crie uma condição de limite que dispara quando o uso médio de CPU de uma máquina virtual para os últimos 5 minutos está acima de 90% (usando a fonte de dados anterior):</span><span class="sxs-lookup"><span data-stu-id="bd37e-120">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
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

<span data-ttu-id="bd37e-121">Criar uma ação de email:</span><span class="sxs-lookup"><span data-stu-id="bd37e-121">Create an email action:</span></span>
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

<span data-ttu-id="bd37e-122">Criar o alerta:</span><span class="sxs-lookup"><span data-stu-id="bd37e-122">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = client.alert_rules.create_or_update(
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
> [<span data-ttu-id="bd37e-123">Explorar as APIs de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="bd37e-123">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/management)
