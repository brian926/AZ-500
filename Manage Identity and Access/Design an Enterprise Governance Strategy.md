Enterprise Governance is the process of setting strategic tools, systems, and process into motion to keep your systems secure and running well.

## Review the Shared Responsibility Model
The following figure depicts the various responsibility zones.
![[Pasted image 20231019083912.png]]

For all cloud deployment types, you own your data and identities. You're responsible for helping secure your data and identities, your on-premises resources, and the cloud components you control (which vary by service type).

Regardless of the deployment type, **you always retain responsibility for the following:**
- Data
- Endpoints
- Accounts
- Access management

## Review Azure Hierarchy of Systems
**Azure Resource Manager** is the deployment and management service for Azure. It provides a consistent management layer that allows you to create, update, and delete resources in your Azure subscription. You can use its access control, auditing, and tagging features to help secure and organize your resources after deployment.

When you take actions through the portal, Azure PowerShell, the Azure CLI, REST APIs, or client software development kits (SDKs), the Resource Manager API handles your request. Because the same API handles all requests, you get consistent results and capabilities from all the different tools. Functionality initially released through APIs should be represented in the portal within 180 days of the initial release.
![[Pasted image 20231019084117.png]]

Azure provides four levels of scope: management groups, subscriptions, resource groups, and resources. The following image shows an example of these layers. Though not labeled as such, the blue cubes are resources.
![[Pasted image 20231019084133.png]]

You apply management settings at any of these levels of scope. The level you select determines how widely the setting is applied. Lower levels inherit settings from higher levels. For example, when you apply a policy to the subscription, the policy is applied to all resource groups and resources in your subscription. When you apply a policy on the resource group, that policy is applied to the resource group and all its resources. However, another resource group doesn't have that policy assignment.

You can deploy templates to management groups, subscriptions, or resource groups.

There are some important factors to consider when defining your resource group:
- All the resources in your group should share the same lifecycle. You deploy, update, and delete them together. If one resource, such as a database server, needs to exist on a different deployment cycle it should be in another resource group.
- Each resource can only exist in one resource group.
- You can add or remove a resource to a resource group at any time.
- You can move a resource from one resource group to another group.
- A resource group can contain resources that are located in different regions.
- A resource group can be used to scope access control for administrative actions.
- A resource can interact with resources in other resource groups. This interaction is common when the two resources are related but don't share the same lifecycle (for example, web apps connecting to a database).

Management groups are an Azure resource to create flexible and very maintainable hierarchies within the structure of your environment. Management groups exist above the subscription level thus allowing subscriptions to be grouped together. This grouping facilitates applying policies and RBAC permissions to those management groups. Policies and RBAC permissions are inherited to all resources in the management group. Management groups give you enterprise-grade management at a large scale no matter what type of subscriptions you might have. All subscriptions within a single management group must trust the same Microsoft Entra tenant.

Management group hierarchies can be up to six levels deep. This provides you with the flexibility to create a hierarchy that combines several of these strategies to meet your organizational needs. For example, the diagram below shows an organizational hierarchy that combines a business unit strategy with a geographic strategy.
![[Pasted image 20231019084532.png]]

The value of management groups
**Group your subscriptions**.
- Provide user access to multiple subscriptions
- Allows for new organizational models and logically grouping of resources.
- Allows for single assignment of controls that applies to all subscriptions.
- Provides aggregated views above the subscription level.
**Mirror your organization's structure**.
- Create a flexible hierarchy that can be updated quickly.
- The hierarchy does not need to model the organization's billing hierarchy.
- The structure can easily scale up or down depending on your needs.
**Apply policies or access controls to any service**.
- Create one RBAC assignment on the management group, which will inherit that access to all the subscriptions.
- Use Azure Resource Manager integrations that allow integrations with other Azure services: Azure Cost Management, Privileged Identity Management, and Microsoft Defender for Cloud.

## Configure Azure Policies
Azure Policy is a service you use to create, assign, and manage policies. These policies enforce different rules and effects over your resources so that those resources stay compliant with your corporate standards and service level agreements. Azure Policy meets this need by evaluating your resources for noncompliance with assigned policies.
**There are three main pillars in the functionalities of Azure policy**.
![[Pasted image 20231019084718.png]]
The **first pillar** is around **real-time enforcement and compliance assessment**. Each policy also provides compliance assessment on all your existing resources to bring a state of compliance for each resource. The data then powers the compliance view which aggregates results across all of the applied policies. Policies can be used to ensure that resource groups are getting tagged properly and automatically inheriting those tags from the resource group down to the resources.

The **second pillar** of policy is **applying policies at scale** by leveraging Management Groups. By assigning policy to a management group one can impact hundreds of subscriptions and all its reach resources through a single policy assignment. There also is the concept called **policy initiative** that allows you to group policies together so that you can view the aggregated compliance result. At the initiative level there's also a concept called exclusion where one can exclude either the child management group, subscription, resource group, or resources from the policy assignment.

The **third pillar** of your policy is **remediation by leveraging a remediation policy** that will automatically remediate the non-compliant resource so that your environment always stays compliant. For existing resources, they will be flagged as non-compliant but they won't automatically be changed because there can be impact to the environment. Azure policy is a free service to use.

Azure Policy has several permissions, known as operations, in two resource providers:
- **Microsoft.Authorization**
- **Microsoft.PolicyInsights**

Many built-in roles grant permissions to Azure Policy resources. The **Resource Policy Contributor** role includes most Azure Policy operations. The **Owner** role has full rights. Both **Contributor** and **Reader** can use all Azure Policy read operations, but Contributor can also trigger remediation.

If none of the built-in roles have the required permissions, create a custom role. Azure has by default, security policies that work across subscriptions or on management groups. If these policies need to be augmented with your own organizational policies, new policies can be created.

The approach to creating a custom policy follows these steps:
- Identify your business requirements
- Map each requirement to an Azure resource property
- Map the property to an alias
- Determine which effect to use
- Compose the policy definition

The steps for composing and implementing a policy in Azure Policy begins with creating:
- **Policy definition** - Every policy definition has conditions under which it's enforced. And, it has a defined effect that takes place if the conditions are met.
- **Policy assignment** - A policy definition that has been assigned to take place within a specific scope. This scope could range from a management group to an individual resource. The term scope refers to all the resources, resource groups, subscriptions, or management groups that the policy definition is assigned to.
- **Policy parameters** - They help simplify your policy management by reducing the number of policy definitions you must create. You can define parameters when creating a policy definition to make it more generic.

In order to easily track compliance for multiple resources, create and assign an **Initiative definition**. With an initiative definition, you can group several policy definitions to achieve one overarching goal. An initiative evaluates resources within scope of the assignment for compliance to the included policies.

## Enable Azure role-based access control (RBAC)
RBAC is an authorization system built on Azure Resource Manager that provides fine-grained access management of Azure resources. Microsoft Entra ID and Role Based Access Control (RBAC) make it simple for you to carry out these goals. After you extend your on-premises Active Directory to the cloud by using Microsoft Entra Connect, your employees can use and manage their Azure subscriptions by using their existing work identities. These Azure subscriptions automatically connect to Microsoft Entra ID for SSO and access management. When you disable an on-premises Active Directory account, it automatically loses access to all Azure subscriptions connected with Microsoft Entra ID.

**Each Azure subscription is associated with one Microsoft Entra directory**. Users, groups, and applications in that directory can manage resources in the Azure subscription. Grant access by assigning the appropriate RBAC role to users, groups, and applications at a certain scope. The scope of a role assignment can be a subscription, a resource group, or a single resource. A role assigned at a parent scope also grants access to the child scopes contained within it.

The following diagram depicts how the classic subscription administrator roles, RBAC roles, and Microsoft Entra administrator roles are related at a high level. Roles assigned at a higher scope, like a subscription, are inherited by child scopes, like service instances.
![[Pasted image 20231020085259.png]]

## Compare and Contrast Azure RBAC vs Azure Policies
There are a few key differences between Azure Policy and **Azure role-based access control (Azure RBAC)**. Azure Policy evaluates the state by examining properties on resources that are represented in Resource Manager and properties of some Resource Providers. Azure Policy ensures that the resource state is compliant with your business rules without concern for who made the change or who has permission to make a change. Azure Policy, through the DenyAction effect, can also block specific actions on resources. Some Azure Policy resources, such as **policy definitions**, **initiative definitions**, and **assignments**, are visible to all users. This design enables transparency to all users and services regarding what policy rules are set in their environment.

Azure RBAC focuses on managing **user actions** at different scopes. If control of an action is required based on user information, then Azure RBAC is the correct tool to use. Even if an individual has access to perform an action, if the result is a non-compliant resource, Azure Policy still blocks the create or update task.  

The combination of **Azure role-based access control (Azure RBAC)** and Azure Policy provides full-scope control in Azure.

Azure Policy has several permissions, known as **operations**, in **two Resource Providers**:
1. Microsoft.Authorization  
2. Microsoft.PolicyInsights

Many built-in roles grant permission to Azure Policy resources. The **Resource Policy Contributor role** includes most Azure Policy operations. **The owner has full rights**. Both **Contributor** and **Reader** have access to all read Azure Policy operations.

A **contributor** may trigger resource remediation but can't create or update definitions and assignments. **User Access Administrator** is necessary to grant the managed identity on **deployIfNotExists** or **modify** the assignment's necessary permissions.

Role-Based Access Control (RBAC) vs Azure Policy:
![[Pasted image 20231020085645.png]]

## Configure built-in roles
Azure role-based access control (RBAC) has several Azure built-in roles that you can assign to users, groups, service principals, and managed identities. Role assignments are the way you control access to Azure resources. If the built-in roles don't meet the specific needs of your organization, you can create your own Azure custom roles.

The four general built-in roles are:

|**Built-in Role**|**Description**|
|---|---|
|**Contributor**|Grants full access to manage all resources, but does not allow you to assign roles in Azure RBAC, manage assignments in Azure Blueprints, or share image galleries.|
|**Owner**|Grants full access to manage all resources, including the ability to assign roles in Azure RBAC.|
|**Reader**|View all resources, but does not allow you to make any changes.|
|**User Access Administrator**|Lets you manage user access to Azure resources.|

Custom roles can be shared between subscriptions that trust the same Microsoft Entra directory. 

The following list describes the limits for custom roles.
- Each directory can have up to **5000** custom roles.
- Azure Germany and Azure China 21Vianet can have up to 2000 custom roles for each directory.
- You cannot set AssignableScopes to the root scope ("/").
- You can only define one management group in AssignableScopes of a custom role. Adding a management group to AssignableScopes is currently in preview.
- Custom roles with DataActions cannot be assigned at the management group scope.
- Azure Resource Manager doesn't validate the management group's existence in the role definition's assignable scope.

## Enable Resource Locks
As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources. You can set the lock level to **CanNotDelete or ReadOnly**. In the portal, the locks are called **Delete and Read-only** respectively.
- **CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.
- **ReadOnly** means authorized users can read a resource, but they can't delete or update the resource. Applying this lock is similar to restricting all authorized users to the permissions granted by the Reader role.

 To create or delete management locks, you must have access to **`Microsoft.Authorization/*`** or `Microsoft.Authorization/locks/*` actions. Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.

## Deploy Azure Blueprints
Azure Blueprints enables cloud architects and central information technology groups to define a repeatable set of Azure resources that implements and adheres to an organization's standards, patterns, and requirements.
The Azure Blueprints service is supported by the globally distributed Azure Cosmos Data Base. Blueprint objects are replicated in multiple Azure regions. This replication provides **low latency**, **high availability**, and **consistent access** to your blueprint objects, regardless of which region Blueprints deploys your resources to.

**How is it different from Azure Resource Manager templates?**
The service design helps with environment setup. This setup often includes **resource groups**, **policies**, **role assignments**, and **Resource Manager template deployments** assigned to a subscription in a single audited and tracked operation. A blueprint is a package to bring each artifact type together and allows you to compose and version that package into a continuous integration and pipeline.

Nearly everything that you want to include for deployment in Blueprints is also with a Resource Manager template. However, a Resource Manager template is a document that doesn't exist natively in Azure – it's stored either locally or in source control. The template gets used for deployments of one or more Azure resources, but once those resources deploy, there's no active connection or relationship to the template.

Blueprints save the relationship between the blueprint definition and the blueprint assignment. This connection supports improved tracking and auditing of deployments. Blueprints can upgrade several subscriptions governed by the exact blueprint.

There's no need to choose between a Resource Manager template and a blueprint. Each blueprint can consist of zero or more Resource Manager template artifacts. This support means that previous efforts to develop and maintain a library of Resource Manager templates are reusable in Blueprints.

**How it's different from Azure Policy**
A blueprint is a package or container for composing focus-specific standards, patterns, and requirements for implementing Azure cloud services, security, and design reused to maintain consistency and compliance.

An Azure policy is a **default allow** and **explicit deny** system focused on resource properties during deployment and for existing resources. It supports cloud governance by validating that help within a subscription adhere to requirements and standards.

Including an Azure policy in a blueprint enables the creation of the correct pattern or design during the assignment of the blueprint. The policy inclusion ensures that only **approved** or **expected changes** can be made to the environment to protect ongoing compliance with the intent of the blueprint.

An Azure policy is available as one of many artifacts in a blueprint definition. Blueprints also support using parameters with **policies** and **initiatives**.

A blueprint is composed of _**artifacts**_. Azure Blueprints currently supports the following resources as artifacts:

|**Resource**|**Hierarchy options**|**Description**|
|---|---|---|
|Resource Groups|Subscription|Create a new resource group for use by other artifacts within the blueprint. These placeholder resource groups enable you to organize resources exactly how you want them structured and provide a scope limiter for included policy and role assignment artifacts and ARM templates.|
|ARM template|Subscription, Resource Group|Templates, including nested and linked templates, are used to compose complex environments. Example environments: a SharePoint farm, Azure Automation State Configuration, or a Log Analytics workspace.|
|Policy Assignment|Subscription, Resource Group|Allows assignment of a policy or initiative to the subscription the blueprint is assigned to. The policy or initiative must be within the scope of the blueprint definition location. If the policy or initiative has parameters, these parameters are assigned at the creation of the blueprint or during blueprint assignment.|
|Role Assignment|Subscription, Resource Group|Add an existing user or group to a built-in role to make sure the right people always have the right access to your resources. Role assignments can be defined for the entire subscription or nested to a specific resource group included in the blueprint.|

When creating a blueprint definition, you'll define where the blueprint is saved. Blueprints can be saved to a **management group** or **subscription** that you have **Contributor access** to. If the location is a management group, the blueprint is available to assign to any child subscription of that management group.

Blueprints can pass parameters to either a **policy/initiative** or an **ARM template**. When adding either _**artifact**_ to a blueprint, the author decides to provide a defined value for each blueprint assignment or to allow each blueprint assignment to provide a value at assignment time. This flexibility provides the option to define a pre-determined value for all uses of the blueprint or to enable that decision to be made at the time of assignment.

## Design an Azure Subscription Management Plan
Organization and governance design considerations: 
Subscriptions serve as boundaries for Azure Policy assignments.
- For example, secure workloads like **Payment Card Industry (PCI)** workloads typically require other policies in order to achieve compliance. Instead of using a management group to collate workloads that require PCI compliance, you can achieve the same isolation with a subscription, without having too many management groups with a few subscriptions.
    - If you need to group together many subscriptions of the same workload archetype, create them under a management group.
- Subscriptions serve as a scale unit so component workloads can scale within platform subscription limits. Make sure you consider subscription resource limits as you design your workloads.
- Subscriptions provide a management boundary for governance and isolation that clearly separates concerns.
- Create separate platform subscriptions for management (monitoring), connectivity, and identity when they're required.
    - Establish a dedicated management subscription in your platform management group to support global management capabilities like Azure Monitor Log Analytics workspaces and Azure Automation runbooks.
        - Establish a dedicated identity subscription in your platform management group to host Windows Server Active Directory domain controllers when needed.
        - Establish a dedicated connectivity subscription in your platform management group to host an **Azure Virtual WAN hub**, **private Domain Name System (DNS)**, **ExpressRoute circuit**, and other networking resources. A dedicated subscription ensures that all your foundation network resources are billed together and isolated from other workloads.
        - Use subscriptions as a democratized unit of management aligned with your business needs and priorities.
- Use manual processes to limit Microsoft Entra tenants to only Enterprise Agreement enrollment subscriptions. Using a manual process prevents the creation of Microsoft Developer Network subscriptions at the root management group scope.
    - For support, submit an Azure Support ticket.

Quota and capacity design considerations:
Azure regions might have a finite number of resources. As a result, available capacity and **Stock-keeping units (SKUs)** should be tracked for Azure adoptions involving a large number of resources.
- Consider limits and quotas within the Azure platform for each service your workloads require.
- Consider the availability of required SKUs within your chosen Azure regions. The availability of certain SKUs for given resources like VMs can be different from one region to another.
- Consider that subscription quotas aren't capacity guarantees and are applied on a per-region basis.
- Consider reusing unused or decommissioned subscriptions as per the guidance in **Should we create a new Azure Subscription every time or can we, and should we, reuse Azure Subscriptions? - Azure landing zones FAQ.**

Each Azure subscription is linked to a single Microsoft Entra tenant, which acts as an **identity provider (IdP)** for your Azure subscription. The Microsoft Entra tenant is used to authenticate users, services, and devices.

The Microsoft Entra tenant linked to your Azure subscription can be changed by any user with the required permissions.

With Azure landing zones, you can set requirements to prevent users from transferring subscriptions to your organization's Microsoft Entra tenant. **Review the process in Manage Azure subscription policies**.

Configure your subscription policy by providing a list of exempted users. Exempted users are permitted to bypass restrictions set in the policy.
- Consider whether users with Visual Studio/MSDN Azure subscriptions should be allowed to transfer their subscription to or from your Microsoft Entra tenant.
- Tenant transfer settings are only configurable by users with the Microsoft Entra Global Administrator role assigned. These users and must have elevated access to change the policy.
    - You can only specify individual user accounts as exempted users, not Microsoft Entra groups.
- All users with access to Azure can view the policy defined for your Microsoft Entra tenant.
    - Users can't view your exempted users list.
    - Users can view the global administrators within your Microsoft Entra tenant.
- Azure subscriptions transferred into a Microsoft Entra tenant are placed into the default management group for that tenant.
- If approved by your organization, your application team can define a process to allow Azure subscriptions to be transferred to or from a Microsoft Entra tenant.

Establish Cost Management Design Consideration:
Cost transparency is a critical management challenge every large enterprise organization faces. This section of the article explores key aspects of achieving cost transparency across large Azure environments.
- Chargeback models, like Azure App Service Environment and Azure Kubernetes Service, might need to be shared to achieve higher density. Shared **platform as a service (PaaS)** resources can be affected by Chargeback models.
- Use a shutdown schedule for nonproduction workloads to optimize costs.
- Use Azure Advisor to check recommendations for optimizing costs.
- Establish a charge back model for better distribution of cost across your organization.
- Implement policy to prevent the deployment of resources not authorized to be deployed in your organization's environment.
- Establish a regular schedule and cadence to review cost and right size resources for workloads.

Organization and Governance Recommendations:
- Treat subscriptions as a unit of management aligned with your business needs and priorities.
- Make subscription owners aware of their roles and responsibilities.
    - Do a quarterly or yearly access review for Microsoft Entra Privileged Identity Management to ensure that privileges don't proliferate as users move within your organization.
    - Take full ownership of budget spending and resources.
    - Ensure policy compliance and remediate when necessary.
- Reference the following principles as you identify requirements for new subscriptions:
    - **Scale limits**: Subscriptions serve as a scale unit for component workloads to scale within platform subscription limits. Large specialized workloads like **high-performance computing**, **Internet of Things (IoT)**, and **System Analysis Program Development (SAP)** should use separate subscriptions to avoid running up against these limits.
    - **Management boundary**: Subscriptions provide a management boundary for governance and isolation, allowing a clear separation of concerns. Different environments, such as development, test, and production, are often removed from a management perspective.
    - **Policy boundary**: Subscriptions serve as a boundary for the Azure Policy assignments. For example, secure workloads like PCI typically require other policies in order to achieve compliance. The other overhead doesn't get considered if you use a separate subscription. Development environments have more relaxed policy requirements than production environments.
    - **Target network topology**: You can't share virtual networks across subscriptions, but you can connect them with different technologies like **virtual network peerin**g or **Azure ExpressRoute**. When deciding if you need a new subscription, consider which workloads need to communicate with each other.
- Group subscriptions together under management groups, which are aligned with your management group structure and policy requirements. Grouping subscriptions ensures that subscriptions with the same set of policies and Azure role assignments all come from a management group.
- Establish a dedicated management subscription in your **Platform** management group to support global management capabilities like Azure Monitor Log Analytics workspaces and Azure Automation runbooks.
- Establish a dedicated identity subscription in your **Platform** management group to host Windows Server Active Directory domain controllers when necessary.
- Establish a dedicated connectivity subscription in your **Platform** management group to host an **Azure Virtual WAN hub**, **private Domain Name System (DNS)**, **ExpressRoute circuit**, and other networking resources. A dedicated subscription ensures that all your foundation network resources are billed together and isolated from other workloads.
- Avoid a rigid subscription model. Instead, use a set of flexible criteria to group subscriptions across your organization. This flexibility ensures that as your organization's structure and workload composition changes, you can create new subscription groups instead of using a fixed set of existing subscriptions. One size doesn't fit all for subscriptions, and what works for one business unit might not work for another. Some applications might coexist within the same landing zone subscription, while others might require their own subscription.

Quota and Capacity Recommendations:
- Use subscriptions as scale units, and scale out resources and subscriptions as required. Your workload can then use the required resources for scaling out without hitting subscription limits in the Azure platform.
- Use reserved instances to manage capacity in some regions. Your workload can then have the required capacity for high demand resources in a specific region.
- Establish a dashboard with custom views to monitor used capacity levels, and set up alerts if capacity is approaching critical levels (90 percent CPU usage).
- Raise support requests for quota increases under subscription provisioning, such as for total available VM cores within a subscription. Ensure that your quota limits are set before your workloads exceed the default limits.
- Ensure that any required services and features are available within your chosen deployment regions.

Automation recommendations:
- Build a Subscription vending process to automate the creation of Subscriptions for application teams via a request workflow as described in **Subscription vending**.

Tenant transfer restriction recommendations:
- Configure the following settings to prevent users from transferring Azure subscriptions to or from your Microsoft Entra tenant:
    - Set Subscription leaving Microsoft Entra directory to Permit no one.
    - Set Subscription entering Microsoft Entra directory to Permit no one.
- Configure a limited list of exempted users.
    - Include members from an Azure PlatformOps (platform operations) team.
    - Include break-glass accounts in the list of exempted users.

