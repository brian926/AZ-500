Processed events that Microsoft Defender for Cloud produces are published to the Azure activity log. Azure Monitor offers a consolidated pipeline for routing any of your monitoring data into a SIEM tool. This pipe uses the Azure Monitor single pipeline for getting  access to the monitoring data from you Azure environment.

Security Center automatically collects, analyzes, and integrates log data from your Azure resources to detect real threats and reduce false positives.

Azure Event Hubs is a streaming platform and event ingestion service that can transform and store data by using any real-time analytics provider of batching/storage adapters.
There are several tiers of monitoring data:
- Application monitoring data - Data about performance and functionality of the code you have written and are running on Azure. Application monitoring data is usually collected in one of the following ways
	- By instrumenting your code with an SDK such as the *Application Insight SDK*
	- By running a monitoring agent that listens for new application logs on the machine running your application, such as the *Windows Azure Diagnostic Agent* or *Linux Azure Diagnostic Agent*
- Guest OS Monitoring Data - Data about the operating system on which your application is running. To collect this type of data, you need to install an agent such as the *Windows Azure Diagnostic Agent* or *Linux Azure Diagnostic Agent*
- Azure resource monitoring data - Data about the operation of an Azure resource. This data can be collected using resource diagnostic settings
- Azure tenant monitoring data - Data about the operation of tenant-level Azure services, such as Azure Active Directory. This data can be collected using a tenant diagnostic setting
Data from any tier can be sent into an event hub, where it can be pulled into a tool.

Some of the features of Microsoft Sentinel are:
-   **More than 100 built-in alert rules**
    -   Sentinel's alert rule wizard to create your own.
    -   Alerts can be triggered by a single event or based on a threshold, or by correlating different datasets or by using built-in machine learning algorithms.
-   **Jupyter Notebooks** that use a growing collection of hunting queries, exploratory queries, and python libraries.
-   **Investigation graph** for visualizing and traversing the connections between entities like users, assets, applications, or URLs and related activities like logins, data transfers, or application usage to rapidly understand the scope and impact of an incident.

## Configure and Monitor metrics and logs
Azure Monitor Metrics is a feature of Azure Monitor that collects numeric data from monitored resources into a time series database. Metrics are numerical values that are collected at regular intervals and describe some aspect of a system at a particular time.

There are multiple types of metrics supported by Azure Monitor Metrics:
-   **Native metrics** use tools in Azure Monitor for analysis and alerting.
    -   Platform metrics are collected from Azure resources. They require no configuration and have no cost.
    -   Custom metrics are collected from different sources that you configure, including applications and agents running on virtual machines.
-   **Prometheus metrics** (preview) are collected from Kubernetes clusters, including Azure Kubernetes Service (AKS), and use industry-standard tools for analyzing and alerting, such as PromQL and Grafana.

Azure Managed Grafana is a data visualization platform built on top of the Grafana software by Grafana Labs. Helps you combine metrics, logs, and traces into a single user interface. It provides with the following integration features:
-   Built-in support for Azure Monitor and Azure Data Explorer
-   User authentication and access control using Azure Active Directory identities
-   Direct import of existing charts from the Azure portal
Managed Grafana bring together all your telemetry data into one place. It uses *Azure Active Directory (Azure AD)'s centralized identity management*, which allows you to control which users can use a Grafana instance, and you can use managed identities to access Azure data stores, such as Azure Monitor.

Azure Monitor collects metrics from the following sources. After these metrics are collected in the Azure Monitor metric database, they can be evaluated together regardless of their source:
-   **Azure resources:** Platform metrics are created by Azure resources and give you visibility into their health and performance. Each type of resource creates a distinct set of metrics without any configuration required. Platform metrics are collected from Azure resources at a one-minute frequency unless specified otherwise in the metric's definition.
-   **Applications:** Application Insights creates metrics for your monitored applications to help you detect performance issues and track trends in how your application is used. Values include Server response time and Browser exceptions.
-   **Virtual machine agents:** Metrics are collected from the guest operating system of a virtual machine. You can enable guest operating system (OS) metrics for Windows virtual machines using the Windows diagnostic extension and Linux virtual machines by using the InfluxData Telegraf agent.
-   **Custom metrics:** You can define metrics in addition to the standard metrics that are automatically available. You can define custom metrics in your application that are monitored by Application Insights. You can also create custom metrics for an Azure service by using the custom metrics Application Programming Interface (API).
-   **Kubernetes clusters:** Kubernetes clusters typically send metric data to a local Prometheus server that you must maintain. Azure Monitor managed service for Prometheus provides a managed service that collects metrics from Kubernetes clusters and stores them in Azure Monitor Metrics.
A common type of log entry is an event, which is collected sporadically. Events are created by an application or service and typically include enough information to provide complete context on their own.

Data in Azure Monitor Logs is retrieved using a log query written with the Kusto query language, which allows you to quickly retrieve, consolidate, and analyze collected data.

## Enable Log Analytics
Log Analytics is the primary tool in the Azure portal for writing log queries and interactively analyzing their results. Even if a log query is used elsewhere in Azure Monitor, you'll typically write and test the query first using Log Analytics.

At the center of Log Analytics is the Log Analytics workspace, which is hosted in Azure. Log Analytics collects data in the workspace from connected sources by configuring data sources and adding solutions to your subscription. Data sources and solutions each create different record types, each with its own set of properties.

You require a Log Analytics workspace if you intend on collecting data from the following sources:
-   Azure resources in your subscription
-   On-premises computers monitored by System Center Operations Manager
-   Device collections from Configuration Manager
-   Diagnostics or log data from Azure storage

## Manage connected sources for log analytics
Windows and Linux agents send collected data from different sources to your Log Analytics workspace in Azure Monitor, as well as any unique logs or metrics as defined in a monitoring solution. The Log Analytics agent also supports insights and other services in Azure Monitor such as Azure Monitor for VMs, Microsoft Defender for Cloud, and Azure Automation.

The Azure diagnostics extension in Azure Monitor can also be used to collect monitoring data from the guest operating system of Azure virtual machines.
The key differences to consider are:
-   Azure Diagnostics Extension can be used only with Azure virtual machines. The Log Analytics agent can be used with virtual machines in Azure, other clouds, and on-premises.
-   Azure Diagnostics extension sends data to Azure Storage, Azure Monitor Metrics (Windows only) and Event Hubs. The Log Analytics agent collects data to Azure Monitor Logs.
-   The Log Analytics agent is required for solutions, Azure Monitor for VMs, and other services such as Microsoft Defender for Cloud.

The Log Analytics agent sends data to a Log Analytics workspace in Azure Monitor. The Windows agent can be multihomed to send data to multiple workspaces and System Center Operations Manager management groups. The Linux agent can send to only a single destination.

## Enable Azure Monitor Alerts
Alert rules in Azure Monitor use action groups, which contain unique sets of recipients and actions that can be shared across multiple rules.

Alert rules are separated from alerts and the actions taken when an alert fires. The alert rule captures the target and criteria for alerting. The alert rule can be in an enabled or a disabled state. Alerts only fire when enabled.

The following are key attributes of an alert rule:
-   **Target Resource**: Defines the scope and signals available for alerting. A target can be any Azure resource. Example targets: a virtual machine, a storage account, a virtual machine scale set, a Log Analytics workspace, or an Application Insights resource. For certain resources (like virtual machines), you can specify multiple resources as the target of the alert rule.
-   **Signal**: Emitted by the target resource. Signals can be of the following types: metric, activity log, Application Insights, and log.
-   **Criteria**: A combination of signal and logic applied on a target resource. Examples:
    -   Percentage CPU > 70%
    -   Server Response Time > 4 ms
    -   Result count of a log query > 100
-   **Alert Name**: A specific name for the alert rule configured by the user.
-   **Alert Description**: A description for the alert rule configured by the user.
-   **Severity**: The severity of the alert after the criteria specified in the alert rule is met. Severity can range from 0 to 4.
    -   Sev 0 = Critical
    -   Sev 1 = Error
    -   Sev 2 = Warning
    -   Sev 3 = Informational
    -   Sev 4 = Verbose
-   **Action**: A specific action taken when the alert is fired.

## Diagnostic Logging
Azure Monitor diagnostic logs are logs produced by an Azure service that provide rich, frequently collected data about the operation of that service. Azure Monitor makes two types of diagnostic logs available:
-   **Tenant logs**. These logs come from tenant-level services that exist outside an Azure subscription, such as Azure Active Directory (Azure AD).
-   **Resource logs**. These logs come from Azure services that deploy resources within an Azure subscription, such as Network Security Groups (NSGs) or storage accounts.
The content of these logs varies by Azure service and resource type.

These logs differ from the **activity log**. The activity log provides insight into the operations, such as creating a VM or deleting a logic app, that Azure Resource Manager performed on resources in your subscription using. The activity log is a subscription-level log. Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, such as getting a secret from a key vault.

These logs also differ from **guest operating system (OS)–level diagnostic logs**. Guest OS diagnostic logs are those collected by an agent running inside a VM or other supported resource type. Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, whereas guest OS–level diagnostic logs capture data from the OS and applications running on a VM.