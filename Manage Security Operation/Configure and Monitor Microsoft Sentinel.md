Microsoft Sentinel is a scalable, cloud-native, security information event management (SIEM) and security orchestration automated response (SOAR) solution. It delivers intelligent security analytics and threat intelligence across the enterprise, providing a single solution for alert detection, threat visibility, proactive hunting, and threat response.
It enables the following services:
- **Collect data at cloud scale** across all users, devices, applications, and infrastructure, both on-premises and in multiple clouds
- **Detect previously undetected threats**, and minimize false positives using Microsoft's analytics and unparalleled threat intelligence
- **Investigate threats with artificial intelligence**, and hunt for suspicious activities at scale, tapping into years of cyber security work
- **Respond to incidents rapidly** with built-in orchestration and automation of common tasks

## Configure Data connections to Sentinel
To onboard Microsoft Sentinel, you first need to connect to your security sources. It comes with a number of connectors for Microsoft solutions. You can also use common event format, Syslog or REST-API to connect your data sources as well.

The following data connection methods are supported:
- **Service to service integration**: Some services are connected natively, such as AWS and Microsoft services, these services leverage the Azure foundation for out-of-the-box integration, the following solutions can be connected in a few clicks:
- Amazon Web Services - CloudTrail
- Azure Activity
- Azure AD audit logs and sign-ins
- Azure AD Identity Protection
- Azure Advanced Threat Protection
- Azure Information Protection
- Microsoft Defender for Cloud
- Cloud App Security
- Domain name server
- Microsoft 365
- Microsoft Defender ATP
- Microsoft web application firewall
- Windows firewall
- Windows security events

Microsoft Sentinel can be connected to all other data sources that perform real-time log streaming using Syslog protocol, via an agent. The Microsoft Sentinel agent converts CEF formatted logs into a format that can be ingested by Log Analytics and depending on the appliance type, the agent is installed either on the appliance or a dedicated Linux server.

To connect your external appliance to Microsoft Sentinel, the agent must be deployed on a dedicated machine to support the communication between the appliance and Sentinel. You can deploy the agent automatically or manually but the automatic deployment is only available if your dedicated machines is a new VM you're creating in Azure. alternatively, you can deploy the agent manually on existing machines (VM or on-premise).

Prerequisites:
- Active Azure Subscription
- Log Analytics workspace
- Contributor permissions to subscription Sentinel workspace resides
- Contributor or Reader permissions on the resource group the workspace belongs to
- Additional permissions to connect specific data sources
- Paid service

## Workbooks to monitor Sentinel Data
After connecting your data sources, you can monitor data using integration with Azure Monitor Workbooks, which provides versatility in creating custom workbooks.
Work books are intended for **Security operations center (SOC)** engineers and analysts of all tiers to visualize data.

## Correlate alerts into incidents by using analytics rules
Incidents are groups of related alerts that indicate an actionable possible threat you can investigate and resolve.

## Automate and orchestrate common tasks by using playbooks
Playbooks are intended for **Security operations center (SOC)** engineers and analysts of all tiers to **automate** and **simplify tasks**, **including data ingestion**, **enrichment**, **investigation**, and **remediation**.

## Hunt and investigate potential breaches
Sentinel deep investigation tools help you to understand the scope and find the root cause of a potential security threat.

Sentinel supports Jupyter notebooks in Azure Machine Learning workspaces, use notebooks in Microsoft Sentinel to extend the scope of what you can do with Microsoft Sentinel data. For example:  
- Perform analytics that isn't built into Microsoft Sentinel, such as some Python machine learning features.  
- Create data visualizations that aren't built into Microsoft Sentinel, such as custom timelines and process trees.
- Integrate data sources outside of Microsoft Sentinel, such as an on-premises data set.

Notebooks are intended for threat hunters or Tier 2-3 analysts, incident investigators, data scientists, and security researchers. They require a higher learning curve and coding knowledge. They have limited automation support.
Notebooks in Microsoft Sentinel provide:
- Queries to both Microsoft Sentinel and external data
- Features for data enrichment, investigation, visualization, hunting, machine learning, and big data analytics
Notebooks are best for:
- More complex chains of repeatable tasks
- Ad-hoc procedural controls
- Machine learning and custom analysis

Notebooks support rich Python libraries for manipulating and visualizing data. They're useful for documenting and sharing analysis evidence.