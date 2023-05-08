The MITRE ATT&CK matrix is a **publicly accessible knowledge base** for understanding the various **tactics** and **techniques** used by attackers during a cyberattack.
The knowledge base is organized into several categories: **pre-attack**, **initial access**, **execution**, **persistence**, **privilege escalation**, **defense evasion**, **credential access**, **discovery**, **lateral movement**, **collection**, **exfiltration**, and **command and control**.

**Tactics (T)** represent the "why" of an ATT&CK technique or sub-technique. It is the adversary's tactical goal: the reason for performing an action. **For example**, an adversary may want to achieve credential access.

**Techniques (T)** represent "how'" an adversary achieves a tactical goal by performing an action. **For example**, an adversary may dump credentials to achieve credential access.

**Common Knowledge (CK)** in ATT&CK stands for common knowledge, essentially the documented modus operandi of tactics and techniques executed by adversaries.

**Defender for Cloud** uses the MITRE Attack matrix to associate alerts with their perceived intent, helping formalize security domain knowledge.

## Microsoft Defender for Cloud
Microsoft Defender for Cloud is a solution for **cloud security posture management (CSPM)** and **cloud workload protection (CWP)** that finds weak spots across your cloud configuration, helps strengthen the overall security posture of your environment, and can protect workloads across multicloud and hybrid environments from evolving threats.

Defender for Cloud fills **three vital needs** as you manage the security of your resources and workloads in the cloud and on-premises:
1.  **Defender for Cloud secure score continually assesses** your security posture so you can track new security opportunities and precisely report on the progress of your security efforts.
2.  **Defender for Cloud recommendations secures** your workloads with step-by-step actions that protect your workloads from known security risks.
3.  **Defender for Cloud alerts defends** your workloads in real-time so you can react immediately and prevent security events from developing.

Microsoft Defender for Cloud's features covers the **two broad pillars** of cloud security:
1.  **Cloud Security Posture Management (CSPM) - Remediate security issues and watch your security posture improve**
2.  **Cloud Workload Protection (CWP) - Identify unique workload security requirements**

When necessary, Defender for Cloud can automatically deploy a Log Analytics agent to gather security-related data. For Azure machines, deployment is handled directly. For hybrid and multicloud environments, **Microsoft Defender plans are extended to non-Azure machines** with the help of **Azure Arc**. **Cloud Security Posture Management (CSPM) features** are extended to multicloud machines without the need for any agents.

Defender for Cloud helps you detect threats across:
-   **Azure Platform as a Service (PaaS)** services - Detect threats targeting **Azure services**, including **Azure App Service**, **Azure SQL**, **Azure Storage Account**, and **more data services**. You can also perform anomaly detection on your Azure activity logs using the native integration with Microsoft Defender for Cloud Apps (formerly known as Microsoft Cloud App Security).
-   **Azure data services** - Defender for Cloud includes capabilities that help you automatically classify your data in Azure SQL. You can also get assessments for potential vulnerabilities across Azure SQL and Storage services and recommendations for how to mitigate them.
-   **Networks** - Defender for Cloud helps you limit exposure to brute force attacks. By **reducing access to virtual machine ports** and **using just-in-time VM access**, you can harden your network by preventing unnecessary access. You can **set secure access policies on selected ports** for **only authorized users**, **allowed source IP address ranges** or **IP addresses**, and for a **limited amount of time**.

In addition to defending your Azure environment, you can **add Defender for Cloud capabilities to your hybrid cloud environment to protect your non-Azure servers**. To help you focus on what matters the most, you'll get customized threat intelligence and prioritized alerts according to your specific environment.

To **extend protection** to on-premises machines, **deploy Azure Arc** and **enable Defender for Cloud's enhanced security features**.

You can extend the Defender for Cloud protection with the following:
-   **Advanced threat protection features** for virtual machines, Structured Query Language SQL databases, containers, web applications, your network, and more - Protections include securing the management ports of your VMs with just-in-time access and adaptive application controls to create allowlists for what apps should and shouldn't run on your machines.

The **Defender plans** of Microsoft Defender for Cloud offer comprehensive defenses for the **compute**, **data**, and **service layers** of your environment:
-   Microsoft Defender for Servers
-   Microsoft Defender for Storage
-   Microsoft Defender for Structured Query Language (SQL)
-   Microsoft Defender for Containers
-   Microsoft Defender for App Service
-   Microsoft Defender for Key Vault
-   Microsoft Defender for Resource Manager
-   Microsoft Defender for Domain Name System (DNS)
-   Microsoft Defender for open-source relational databases
-   Microsoft Defender for Azure Cosmos Database (DB)
-   Defender Cloud Security Posture Management (CSPM)
    -   Security governance and regulatory compliance
    -   Cloud security explorer
    -   Attack path analysis
    -   Agentless scanning for machines
-   Defender for DevOps

## Security Posture
In Defender for Cloud, the posture management features provide the following:
1.  **Hardening guidance** - to help you efficiently and effectively improve your security
2.  **Visibility** - to help you understand your current security situation

As soon as you open Defender for Cloud for the first time, Defender for Cloud:
-   **Generates a secure score** for your subscriptions based on an assessment of your connected resources compared with the guidance in the **Microsoft cloud security benchmark**. 
-   **Provides hardening recommendations** based on any **identified security misconfigurations** and **weaknesses**. 
-   **Analyzes and secure's your attack paths** through the cloud security graph, which is a graph-based context engine that exists within Defender for Cloud. The cloud security graph collects data from your multicloud environment and other data sources. The data collected is then used to build a graph representing your multicloud environment.

 Attack path analysis is a **graph-based algorithm that scans the cloud security graph**. The **scans expose exploitable paths attackers may use to breach your environment to reach your high-impact assets**. Attack path analysis exposes those attack paths and suggests recommendations as to how best to remediate the issues that will break the attack path and prevent a successful breach.

## Workload Protections
**The Cloud workload dashboard includes the following sections:**
1.  **Microsoft Defender for Cloud coverage** - Here you can see the resources types in your subscription that are eligible for protection by Defender for Cloud. Wherever relevant, you can upgrade here as well. 
2.  **Security alerts** - When Defender for Cloud detects a threat in any area of your environment, it generates an alert. These alerts describe details of the affected resources, suggested remediation steps, and in some cases an option to **trigger a logic app** in response. 
3.  **Advanced protection** - Defender for Cloud includes many advanced threat protection capabilities for virtual machines, **Structured Query Language (SQL)** databases, containers, web applications, your network, and more. In this advanced protection section, you can see the status of the resources in your selected subscriptions for each of these protections.
4.  **Insights** - This rolling pane of news, suggested reading, and high priority alerts gives Defender for Cloud's insights into pressing security matters that are relevant to you and your subscription. Whether it's a list of high severity **Common Vulnerabilities and Exposures (CVEs)** discovered on your VMs by a vulnerability analysis tool, or a new blog post by a member of the Defender for Cloud team, you'll find it here in the Insights panel.

## Deploy Microsoft Defender for Cloud
When you open Defender for Cloud in the Azure portal for the first time or if you enable it through the Application Programming Interface (API), Defender for Cloud is **enabled for free on all your Azure subscriptions**. Defender for Cloud provides foundational **cloud security and posture management (CSPM)** features by default. The foundational CSPM includes a **secure score**, **security policy and basic recommendations**, and **network security assessment** to help you **protect your Azure resources**.

Defender for cloud **offers foundational multicloud CSPM capabilities for free**. These capabilities are automatically enabled by default on any subscription or account that has been onboarded to Defender for Cloud. The foundational CSPM includes asset discovery, continuous assessment and security recommendations for posture hardening, compliance with Microsoft Cloud Security Benchmark (MCSB), and a Secure score which measure the current status of your organization’s posture.

The optional Defender CSPM plan provides advanced posture management capabilities such as **Attack path analysis**, **Cloud security explorer**, **advanced threat hunting**, **security governance capabilities**, and also tools to assess your security compliance with a wide range of benchmarks, regulatory standards, and any custom security policies required in your organization, industry, or region.

When you enable the enhanced security features (paid), Defender for Cloud can provide unified security management and threat protection across your hybrid cloud workloads, including:
-   **Microsoft Defender for Endpoint** - Microsoft Defender for Servers includes Microsoft Defender for Endpoint for comprehensive endpoint detection and response (EDR).
-   **Vulnerability assessment for virtual machines, container registries, and SQL resources** - Easily enable vulnerability assessment solutions to discover, manage, and resolve vulnerabilities. View, investigate, and remediate the findings directly from within Defender for Cloud.
-   **Multicloud security** - Connect your accounts from Amazon Web Services (AWS) and Google Cloud Platform (GCP) to protect resources and workloads on those platforms with a range of Microsoft Defender for Cloud security features.
-   **Hybrid security** – Get a unified view of security across all of your on-premises and cloud workloads. Apply security policies and continuously assess the security of your hybrid cloud workloads to ensure compliance with security standards. Collect, search, and analyze security data from multiple sources, including firewalls and other partner solutions.
-   **Threat protection alerts** - Advanced behavioral analytics and the Microsoft Intelligent Security Graph provide an edge over evolving cyber-attacks. Built-in behavioral analytics and machine learning can identify attacks and zero-day exploits. Monitor networks, machines, data stores (SQL servers hosted inside and outside Azure, Azure SQL databases, Azure SQL Managed Instance, and Azure Storage), and cloud services for incoming attacks and post-breach activity. Streamline investigation with interactive tools and contextual threat intelligence.
-   **Track compliance with a range of standards** - Defender for Cloud continuously assesses your hybrid cloud environment to analyze the risk factors according to the controls and best practices in the Microsoft cloud security benchmark. When you enable enhanced security features, you can apply a range of other industry standards, regulatory standards, and benchmarks according to your organization's needs. Add standards and track your compliance with them from the regulatory compliance dashboard.
-   **Access and application controls** - Block malware and other unwanted applications by applying machine learning-powered recommendations adapted to your specific workloads to create allowlists and blocklists. Reduce the network attack surface with just-in-time, controlled access to management ports on Azure VMs. Access and application control drastically reduce exposure to brute force and other network attacks.
-   **Container security features** - Benefit from vulnerability management and real-time threat protection in your containerized environments. Charges are based on the number of unique container images pushed to your connected registry. After an image has been scanned once, you won't be charged for it again unless it's modified and pushed once more.
-   **Breadth threat protection for resources connected to Azure** - Cloud-native threat protection for the Azure services common to all of your resources: Azure Resource Manager, Azure Domain Name System (DNS), Azure network layer, and Azure Key Vault. Defender for Cloud has unique visibility into the Azure management layer and the Azure DNS layer and can therefore protect cloud resources that are connected to those layers.
-   **Manage your Cloud Security Posture Management (CSPM)** - CSPM offers you the ability to remediate security issues and review your security posture through the tools provided.
    These tools include:
    -   **Security governance and regulatory compliance**
        -   Security governance and regulatory compliance refer to the policies and processes which organizations have in place to ensure that they comply with laws, rules, and regulations put in place by external bodies (government) that control activity in a given jurisdiction. Defender for Cloud allows you to view your regulatory compliance through the regulatory compliance dashboard. Defender for Cloud continuously assesses your hybrid cloud environment to analyze the risk factors according to the controls and best practices in the standards you've applied to your subscriptions. The dashboard reflects the status of your compliance with these standards.
    -   **Cloud security graph**
        -   The cloud security graph is a **graph-based context engine** that exists within Defender for Cloud. The cloud security graph collects data from your multicloud environment and other data sources. You can also query the graph using the cloud security explorer.
    -   **Attack path analysis**
        -   Attack path analysis helps you to **address the security issues that pose immediate threats with the greatest potential of being exploited in your environment**. Defender for Cloud analyzes which security issues are part of potential attack paths that attackers could use to breach your environment. It also highlights the security recommendations that need to be resolved in order to mitigate the issue.
    -   **Agentless scanning for machines**
        -   Microsoft Defender for Cloud maximizes coverage on OS posture issues and extends beyond the reach of agent-based assessments. With agentless scanning for VMs, you can get frictionless, wide, and instant visibility on actionable posture issues without installed agents, network connectivity requirements, or machine performance impact. **Agentless scanning for VMs provides vulnerability assessment and software inventory** powered by Defender vulnerability management in Azure and Amazon AWS environments. Agentless scanning is available in Defender Cloud Security Posture Management (CSPM) and Defender for Servers.

## Azure Arc
Azure Arc allows you to manage the following resource types hosted outside of Azure:
-   **Servers**: Manage Windows and Linux physical servers and virtual machines hosted outside of Azure.
-   **Kubernetes clusters**: Attach and configure Kubernetes clusters running anywhere with multiple supported distributions.
-   **Azure data services**: Run Azure data services on-premises, at the edge, and in public clouds using Kubernetes and the infrastructure of your choice. SQL Managed Instance and PostgreSQL server (preview) services are currently available.
-   **SQL Server**: Extend Azure services to SQL Server instances hosted outside of Azure.
-   **Virtual machines (preview)**: Provision, resize, delete, and manage virtual machines based on VMware vSphere or Azure Stack **hyper-converged infrastructure (HCI)** and enable VM self-service through role-based access.

## Microsoft Cloud Security Benchmark
The **Microsoft cloud security benchmark (MCSB)** provides **prescriptive best practices** and **recommendations** to help improve the security of workloads, data, and services on Azure and your multi-cloud environment, focusing on cloud-centric control areas with input from a set of holistic Microsoft and industry security guidance that includes:
-   **Cloud Adoption Framework**: Guidance on **security**, including **strategy**, **roles** and **responsibilities**, **Azure Top 10 Security Best Practices**, and **reference implementation**.
-   **Azure Well-Architected Framework**: Guidance on securing your workloads on Azure.
-   **The Chief Information Security Officer (CISO) Workshop**: Program guidance and reference strategies to accelerate security modernization using Zero Trust principles.
-   **Other industry and cloud service provider's security best practice standards and framework**

**Comprehensive multi-cloud security framework**: Organizations often have to build an internal security standard to reconcile security controls across multiple cloud platforms to meet security and compliance requirements on each of them. This often requires security teams to repeat the same implementation, monitoring, and assessment across the different cloud environments (**often for different compliance standards**). This creates unnecessary overhead, cost, and effort. To address this concern, we enhanced the **Azure Security Benchmark (ASB)** to the **Microsoft cloud security benchmark (MCSB)** to help you quickly work with different clouds by:
-   Providing a single control framework to easily meet the security controls across clouds
-   Providing consistent user experience for monitoring and enforcing the multi-cloud security benchmark in Defender for Cloud
-   Staying aligned with Industry Standards (e.g., Center for Internet Security, National Institute of Standards and Technology, Payment Card Industry)

## Microsoft Defender for Cloud Policies
A security initiative is a **collection of Azure Policy definitions** or **rules that are grouped together towards a specific goal or purpose**. Security initiatives simplify the management of your policies by **grouping a set of policies together**, **logically**, as a **single item**.
A security initiative defines the desired configuration of your workloads and helps ensure you comply with the security requirements of your company or regulators.
Like security policies, Defender for Cloud initiatives are also created in Azure Policy. You can use **Azure Policy** to manage your policies, build initiatives, and assign initiatives to multiple subscriptions or entire management groups.

The default initiative automatically assigned to every subscription in Microsoft Defender for Cloud is the Microsoft cloud security benchmark. This benchmark is the Microsoft-authored set of guidelines for security and compliance best practices based on common compliance frameworks. This widely respected benchmark builds on the controls from the **Center for Internet Security (CIS)** and the **National Institute of Standards and Technology (NIST)** with a focus on cloud-centric security.

An Azure Policy definition, created in Azure Policy, is a **rule about specific security conditions you want to be controlled**. Built-in definitions include things like **controlling what type of resources can be deployed** or **enforcing the use of tags on all resources**. You can also create your own custom policy definitions.

To implement these policy definitions (**whether built-in** or **custom**), you'll need to assign them. You can assign any of these policies through the **Azure portal**, **PowerShell**, or **Azure CLI**. Policies can be disabled or enabled from Azure Policy.

There are different types of policies in Azure Policy. Defender for Cloud mainly uses '**Audit**' policies that **check specific conditions** and **configurations** and **then report on compliance**. There are also "**Enforce**' policies that can be used to **apply security settings**.

## View and Edit Security Policies
Defender for Cloud uses **Azure role-based access control (Azure RBAC)**, which provides built-in roles you can assign to **Azure users**, **groups**, and **services**. When users open Defender for Cloud, they see only information related to the resources they can access. Users are assigned the owner, contributor, or reader role to the resource's subscription.

There are two specific roles for Defender for Cloud:
1.  **Security Administrator**: Has the same view rights as security reader. Can also update the security policy and dismiss alerts.
2.  **Security reader**: Has rights to view Defender for Cloud items such as recommendations, alerts, policy, and health. Can't make changes.

## Microsoft Defender Cloud Recommendations
**Recommendations** are actions for you to take to secure and harden your resources. Each recommendation provides you with the following information:
-   A short description of the issue
-   The remediation steps to carry out in order to implement the recommendation
-   The affected resources

The recommendation details shown are:

1.  For supported recommendations, the top toolbar shows any or all of the following buttons:
    -   Enforce and Deny
    -   View the policy definition to go directly to the Azure Policy entry for the underlying policy.
    -   **Open query** - You can view the detailed information about the affected resources using Azure Resource Graph Explorer.
2.  **Severity indicator**
3.  **Freshness interval**
4.  **Count of exempted resources** if exemptions exist for a recommendation; this shows the number of resources that have been exempted with a link to view the specific resources.
5.  **Mapping to MITRE ATT&CK tactics and techniques** if a recommendation has defined tactics and techniques, select the icon for links to the relevant pages on MITRE's site. This applies only to Azure-scored recommendations.
6.  **Description** - A short description of the security issue.
7.  When relevant, the details page also includes a table of related recommendations:
    The relationship types are:
    -   **Prerequisite** - A recommendation that must be completed before the selected recommendation
    -   **Alternative** - A different recommendation that provides another way of achieving the goals of the selected recommendation
    -   **Dependent** - A recommendation for which the selected recommendation is a prerequisite
8. **Remediation steps** - A description of the manual steps required to remediate the security issue on the affected resources. For recommendations with the Fix option, you can **select View remediation logic** before applying the suggested fix to your resources.
9.  **Affected resources** - Your resources are grouped into tabs:
    -   **Healthy resources** – Relevant resources that either aren't impacted or on which you have already remediated the issue.
    -   **Unhealthy resources** – Resources that are still impacted by the identified issue.
    -   **Not applicable resources** – Resources for which the recommendation can't give a definitive answer. The not applicable tab also includes reasons for each resource.
10.  Action buttons to remediate the recommendation or trigger a logic app.

## Secure Score
Defender for Cloud continually assesses your cross-cloud resources for security issues. It then **aggregates all the findings into a single score** so that you can tell, at a glance, your current security situation: the **higher the score**, the **lower the identified risk level**.

To increase your security, review Defender for Cloud's **recommendations page** and remediate the recommendation by implementing the remediation instructions for each issue. **Recommendations are grouped into security controls**. Each control is a **logical group of related security recommendations** and **reflects your vulnerable attack surfaces**. Your score only improves when you _**remediate all**_ of the recommendations for a _**single resource within a control**_. To see how well your organization is securing each individual attack surface, review the scores for each security control.
To get all the possible points for security control, all of your **resources must comply with all of the security recommendations within the security control**.