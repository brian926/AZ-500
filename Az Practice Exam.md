**Q: You have a workload in Azure that uses a VM named VM1 in a Resource Group named RG1. You need to create and assign an identity to VM1 that will be used to access Azure resources and other VMs must be able to use the same identity. Which PowerShell script should you run?**
**A:** Only user-assigned managed identities can be changed by different Azure resources. Once a managed identity is created, you need to update the VM to use the identity by passing its resource ID.
```PowerShell
New-AzUserAssignedIdentity -ResourceGroupName RG1 -Name VMID $vm = Get-AzVM -ResourceGroupName RG1 -Name VM1 Update-AzVM -ResourceGroupName RG1 -VM $vm -IdentityType UserAssigned -IdentityID "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/RG1/providers/Microsoft.ManagedIdentity/userAssignedIdentities/VMID"
```
- [[Configure Application Security Features#Enable Managed Identities|Enabled Manage Identities]]

**Q: You're configuring Azure AD risk policies and need to configure a policy that minimizes the impact on user experience while following the Zero Trust architecture. Your users are not registered for multi-factor authentication (MFA), and self-service password reset (SSPR) is disabled, what should you do?**
**A:** *Set the user risk policy threshold to high*. Choosing a high threshold reduces the number of times a policy is triggered and minimizes the impact on users. 
- [[Deploy Microsoft Entra ID Protection#Implement User Risk Policy|Implement User Risk Policy]]

**Q: You need to configure passwordless authentication, which role should you assign to complete the task?**
**A:** *Global Administrator*. Configuring authentication methods require Global Administrator privileges.
- [[Secure Azure Solutions with Microsoft Entra ID#Investigate Roles in Microsoft Entra ID|Investigate Roles in Microsoft Entra]]

**Q: You have an Azure AD tenant and all the users in the tenant have Windows devices that are Azure AD-joined. You need to implement Azure AD Multi-Factor Authentication (MFA) and the solution must ensure that Azure MFA can be used without internet access or mobile network availability. Which authentication method should you use?**
**A:** *Windows Hello for Business*. When you configure Azure AD MFA, you can configure authentication to use Windows Hello for Business. With this method, users will sign in by using a biometric factor such as a fingerprint or require a PIN to be entered on the device. With Windows Hello for Business, validation is performed locally. Internet access or a mobile network are not needed nor required.

**Q: You plan to deploy Microsoft Entra Verified ID and need to identify which administrative roles are required for the solution. Which three roles should you identify?**
**A:** *Authentication Policy Administrator*, *Application Administrator*, and *Contributor*. The Authentication Policy Administrator role can configure policies and create and manage verified credentials. The Application Administrator role is used to complete app registrations, including granting admin consent. The Contributor role is required to manage all the resoucres in the subscription.

**Q: You need to prevent users from a domain named contoso.com from being invited to the tenant, what should you do?**
**A:** *Edit the Collaboration restrictions settings*. After you edit the Collaboration restrictions settings, if you try to invite a user from a blocked domain, you cannot. By default, the Allow invitations to be sent to any domain settings is enabled.
- [[Secure Azure Solutions with Microsoft Entra ID]]

**Q: You need to provide an administrator with the ability to manage custom RBAC roles, what role should you assign to the administrator?**
**A:** *User Access Administrator*. User Access Administrator is the least privileged role that grants access to `Microsoft.Authorization/roleDefinition/write`.
- [[Secure Azure Solutions with Microsoft Entra ID]]

**Q: You have resource group named RG1 that contains an Azure VM named VM1. A user named User1 is assigned the Contributor role for RG1. You need to prevent User1 from modifying the properties of VM1, what should you do?**
**A:** *Apply a read-only lock to the RG1 scope*. A read-only lock on a resource group that contains a VM prevents all users from starting or restarting the VM.
- [[Design an Enterprise Governance Strategy]]

**Q: You have an Azure subscription named Sub1 that is linked to an Azure AD tenant, that tenant contains a user named Admin1. Sub1 contains an Azure Policy definition assignment named Assignment1. The definition includes the deployIfNotExists effect. You need to grant Admin1 permission to include a remediation task for Assignment1, what role should you assign to Admin1?**
**A:** *Resource Policy Contributor*. Resource Policy Contributor grants permissions to create and modify resource policy, create support ticket, and read resources and hierarchy.
- [[Design an Enterprise Governance Strategy#Compare and Contrast Azure RBAC vs Azure Policies|Compare and contrast Azure RBAC vs Azure policies]]

**Q: You have an Azure virtual network named VNet1 that is in a resource group named RG1. VNet1 contains the following two subnets:**
- Subnet1: 10.0.1.0/24
- Subnet2: 10.0.2.0/24
**You need to configure access to a storage account named sa1 in resource group RG2 and ensure that sa1 can only be accessed from Subnet2. What should you run?**
**A:** The correct CLI command adds a rule to allow access from the 10.0.2.0/24 subnet to the storage account
`az storage account network-rule add --resource-group "RG2" --account-name "SA1" --ip-address "10.0.2.0/24" az storage account update --default-action deny --name sa1 --resource-group RG2`
- [[Configure Network Security]]

**Q: You have an Azure subscription that contains a VM named VM1 and a storage account named storage1. You need to ensure that VM1 can access storage1 over the Azure backbone network, what should you implement?**
**A:** *service endpoints*. Service endpoints route the traffic inside of Azure backbone, allowing access to the entire service, for example, all Microsoft SQL servers or the storage accounts of all customers.

**Q: You have an Azure subscription that contains a web app named WebApp1 and a virtual network named VNet1, which contains the following subnets**
- Subnet1: Connected to a virtual machine
- Subnet2: Has a `Microsoft.Storage` service endpoint
- Subnet3: Has subnet delegation to the `Microsoft.Sql/managedInstances` service
- Subnet4: Has no additional configurations
**You need to integrate WebApp1 with VNet1, which subnets can you connect to WebApp1?**
**A:** *Subnet2 and Subnet4 only*. You can integrate a web app only to a dedicated subnet of a virtual network that does not have any connected resources. The subnet can have service endpoints, but subnet delegation should either not be configured or must be configured to the `Microsoft.Web/serverFarms` service, otherwise you will get the following error: Subnet is missing a delegation to Microsoft.Web/serverFarms. Please add the delegation and try again.
- [[Configure Application Security Features]]

**Q: You host a web app on an Azure VM and users access the app through a public load balancer. You need to offload SSL traffic to the web app at the edge, what should you do?**
**A:** *Configure Azure Front Door and switch access to the app via an internal load balancer*. Front Door allows for SSL offloading at the edge and can route traffic to an internal load balancer.
- [[Configure Network Security]]

**Q: You are implementing an Azure Kubernetes Service (AKS) cluster for a production workload and need to ensure that the cluster meets the following requirements**
- Provides the highest networking performance possible
- Manages ingress traffic by using Kubernetes tools
**What should you use?**
**A:** *CNI networking with ingress resources and controllers*. CNI networking provides the best performance since it does not require IP forwarding and UDR, and ingress controllers can be managed from within Kubernetes.
- [[Enable Containers Security]]

**Q: You have an Azure container registry named ACR1 and a user named User1 and need to ensure that User1 can administer images in ACR1. Which two roles should you assign to User1?**
**A:** *AcrPush* and *AcrDelete*. To administer images in ACR1, a user must be able to push and pull images to ACR1 and delete images from ACR1.
- [[Enable Containers Security]]

**Q: You have an Azure Kubernetes Service (AKS) cluster named AKS1 and a user named User1, and you need to ensure that User1 has access to AKS1 secrets. Which role should you assign to User1?**
**A:** *Azure Kuvernetes Service RBAC Write*. Azure Kubernetes Service RBAC Writer has access to secrets, 
- [[Enable Containers Security]]

**Q: Company has an Azure subscription and Amazon Web Services (AWS) account. You plan to deploy Kubernetes to AWS and need to ensure that you can use Azure Monitor Container Insights to monitor container workload performance. What should you deploy first?**
**A:** *Azure Acr-enabled Kubernetes*. Azure Acr-enabled Kubernetes is the only configuration that includes Kubernetes and can be deployed to AWS.
- [[Configure and Manage Azure Monitor]]

**Q: You have a VM named VM1 that is configured with just-in-time (JIT) VM access. You need to request access to VM1, which PowerShell cmdlet should you run?**
**A:** The `start-AzJitNetworkAccesspolicy` PowerShell cmdlet is used to request access to a JIT-enabled virtual machine.
- [[Enable and Manage Microsoft Defender for Cloud]]

**Q: You have an Azure Blob storage account named sa1 and an app named App1. A binary file named File1 is stored in sa1. You need to share File1 with a customer and the solution must limit access to the IP address that the customer used when completing a purchasing flow in App1, Other uses must be prevented from accessing File1, what should you configure?**
**A:** *a SAS token that includes the `signedIP` field*. Configuring a SAS token that includes the `signedIP` field specifies an IP address or a range of IP addresses from which to accept requests.
- [[Configure Network Security]]

**Q: You have an Azure Storage account and plan to prevent the use of shared keys by using Azure Policy. Which two access methods will continue to work?**
**A:** *Storage Blob Data Reader role* and *user delegation*. The Storage Blob Data Reader role uses Azure AD to authenticate. User delegation SAS is a method that uses Azure AD to generate a SAS. Both methods work whether the shared keys are allowed or prevented.
- [[Implement Storage Security]]

**Q: You have an application that will secure share files hosted in Azure Blob storage to external users. The external users will not use Azure AD to authenticate. You plan to share more than 1,000 files and need to restrict access to only a single IP address for each file. What should you do?**
**A:** *Generate a service SAS that includes the signedIP field*. Using the Generate a service SAS that includes the signedIP field allows a SAS to be generated by using an account key, and each SAS can be configured with an allowed IP address.
- [[Implement Storage Security]]

**Q: You create an Azure policy by using the following snippet**
```json
"then": { 
	"effect": "", 
	"details": [{ 
		"field": "Microsoft.Storage/storageAccounts/networkAcls.ipRules", 
		"value": [{ 
			"action": "Allow", 
			"value": "134.5.0.0/21" 
		}] 
	}] 
}
```
**You need to ensure that the policy is applied whenever a new storage account is created or updated. There is no managed identity assigned to the policy initiative, which effect should you use?**
**A:** *Append*. `Append` is used to add fields to existing properties.
- [[Design an Enterprise Governance Strategy]]

**Q: You need to ensure that all resources created in the subscription have a tag named CostCenter and an associated value. You create a custom policy that uses the following snippet**
```json
"if": { 
	"allOf": [{ 
			"field": "type", 
			"equals": "Microsoft.Resources/subscriptions/resourceGroups" 
		}, 
		{ 
			"field": "tags['CostCenter']", 
			"exists": false 
		} 
	] 
}, 
"then": { 
	"effect": "" 
}
```
**Which effect should you use in line 13?
**A:** *Deny*. We want to deny the creation or modification of a resource if the CostCenter tag is not present.
- [[Design an Enterprise Governance Strategy]]

**Q: You are evaluating the Azure Policy configurations to identify any required custom initiatives and polices. You need to run workloads in Azure that are compliant with the following requlations:**
- FedRAMP High
- PCI DSS 3.2.1
- GDPR
- ISO 27001:2013
**For which regulation should you create custom initiatives?**
**A:** *GDRP*. To run workloads that are compliant with GDPR, custom initiatives should be created. GDPR compliance initiatives are not yet available in Azure.
- [[Design an Enterprise Governance Strategy]]

**Q: You have the following security policy deployed to an Azure subscription**
```json
policyRule: { 
	if: { 
		allOf: [ 
			{ 
				field: "type", 
				equals: "Microsoft.Storage/storageAccounts" 
			}, 
			{ 
				field: "Microsoft.Storage/storageAccounts/allowSharedKeyAccess", 
				equals: "true" 
			} 
		] 
	}, 
	then: { 
		effect: "Deny" 
	} 
}
```
**You successfully deploy a new storage account. Which statements is true?**
**A:** *Usage of Azure AD authentication is enforced*. Enforcing Azure AD authentication prevents using shared keys, and leaves only data plane RBAC as an authentication option. 
- [[Design an Enterprise Governance Strategy]]

**Q: You need to recommend a solution that uses crawling technology of Microsoft to discover and actively scan assets within an online infrastructure, and must also discover new connections over time. What should you include in the recommendation?**
**A:** *Microsoft Defender External Attack Surface Management (EASM)*. Defender EASM applies crawling technology to Microsoft to discover assets that are related to your known online infrastructure and actively scans these assets to discover new connections over time.
- [[Enable and Manage Microsoft Defender for Cloud]]

**Q: You configure Microsoft Sentinel to connect to different data sources and are unable to configure a connector that uses an Azure Function API connection. Which permissions should you change?**
**A:** *read and write permissions for Azure Functions*. You need to have read and write permissions to Azure Functions to configure a connector that uses an Azure Functions API connection.
- [[Configure and Monitor Microsoft Sentinel]]

**Q: You have a data connector for Microsoft Sentinel and need to configure the connector to collect logs from Conditional Access in Azure AD. Which log should you connect to Microsoft Sentinel?**
**A:** *sign-in logs*. Sign-in logs include information about sign-ins and how resources are used by your users.
- [[Configure and Monitor Microsoft Sentinel]]

**Q: You plan to deploy storage accounts and limit the use of shared access key access by using Azure Policy. Which two effects in an Azure policy will audit any attempts to use shared access keys?**
**A:** *Audit* and *Deny*. `Audit` and `Deny` will both audit any attempts to use storage account shared keys.
- [[Design an Enterprise Governance Strategy]]

**Q: You have an Azure key vault and need to ensure that a user can read and write keys to the Key Vault. Which role should you assign to the user?**
**A:** *Key Vault Crypto Officer*. Key Vault Crypto Officer has all the permissions to the secrets in the Key Vault.
- [[Deploy and Secure Azure Key Vault]]

**Q: You need to delegate the ability to configure sign-in risk policies, which role should you assign?**
**A:** *Conditional Access Administrator*. Security administrators have permissions to manage security-related features in the Microsoft 365 Defender portal, Microsoft Entra Identity Protection, Microsoft Entra authentication, Azure Information Protection (AIP), and Microsoft 365 Defender portal.
- [[Create an access review of Azure resource and Microsoft Entra roles in PIM]]
- [[Least privileged Roles by task in Microsoft Entra ID]]
- [[Authentication and verification methods are available in Microsoft Entra ID]]
- [[Secure Azure Solutions with Microsoft Entra ID#Investigate Roles in Microsoft Entra ID|Investigate Roles in Microsoft Entra]]

**Q: Users have both Windows and non-Windows devices. All users have smart phones. You plan on implement Microsoft Entra Multi-Factor Authentication (MFA) and need to ensure that MFA is used to authenticate users to Azure resources without any additional cost. Which three MFA method should you implement?**
**A:** *SMS verification*, *the Microsoft Authenticator app*, and *voice call verification*. The Microsoft Authenticator app, SMS verification, and voice call verification only require a smart phone. Because all users already have smart phones, those three options don’t require any additional cost.
- [[Plan a Microsoft Entra multifactor authentication deployment]]

**Q: You need to ensure that users signing into the Azure Portal are prompted to sign in every 48 hours, what should you configure?**
**A:** *Conditional Access Sign-in frequency*. Sign-in frequency defines the time period before a user is asked to sign in again when attempting to access a resource.
- [[Plan a Conditional Access deployment]]
- [[Conditional Access Session]]
- [[Deploy Microsoft Entra ID Protection#Configure Conditional Access Conditions|Configure Conditional Access Conditions]]

**Q: You use Azure Blueprints to deploy resources to a resource group named RG1. After the deployment, you try to add a disk to a VM created by using Blueprints, but you get an access denied error. You open RG1 and check your access and you notice that you are listed as part of the Virtual Machine Contributor role for RG1, and there are no deny assignments or classic administrators in the resource group scope. Why are you unable to manage the VM?**
**A:** *Blueprints created a deny assignment for the VM resource*. Blueprints must have created a deny assignment at the resource level.
- [[Design an Enterprise Governance Strategy]]

**Q: You create a role by using the following JSON**
```json
{ 
	"Name": "Virtual Machine Operator", 
	"Id": "88888888-8888-8888-8888-888888888888", 
	"IsCustom": true, "Description": "Can monitor and restart virtual machines.",
	"Actions": [ 
		"Microsoft.Storage/*/read", 
		"Microsoft.Network/*/read", 
		"Microsoft.Compute/virtualMachines/start/action",
		"Microsoft.Compute/virtualMachines/restart/action", 
		"Microsoft.Authorization/*/read", 
		"Microsoft.ResourceHealth/availabilityStatuses/read",
		"Microsoft.Resources/subscriptions/resourceGroups/read",
		"Microsoft.Insights/alertRules/*", 
		"Microsoft.Insights/diagnosticSettings/*", 
		"Microsoft.Support/*" 
	], 
	"NotActions": [], 
	"DataActions": [], 
	"NotDataActions": [], 
	"AssignableScopes": ["/subscriptions/*"] 
}
```
**A user that is part of the new role reports that they are unable to restart a VM by using a PowerShell script, what should you do to ensure that the user can restart the VM?**
**A:** *Add `Microsoft.Compute/*/read` to the list of `Actions` in the role.* The role needs read access to VMs to restart them.
- [[Design an Enterprise Governance Strategy]]
- [[Azure Custom roles]]

**Q: You create a Microsoft Entra app registration and need to consent to the use of a given API in your app for all users. What should you add to your app registration?**
**A:** *a permission*. A permission allows the application to use a given API.
- [[Configure Application Security Features]]

**Q: You need to provide an administrator with the ability to manage custom RBAC roles. Which role should you assign to the administrator?**
**A:** *User Access Administrator*. User Access Administrator is the least privileged role that grants access to `Microsoft.Authorization/roleDefinition/write`.
- [[Secure Azure Solutions with Microsoft Entra ID]]

**Q: You have an Azure subscription named Sub1 that is linked to a Microsoft Entra tenant. The tenant contains a user named Admin1 and Sub1 contains an Azure Policy definition assighment named Assignment1. The definition includes the deployIfNotExists effect. You need to grant Admin1 permission to include a remediation task for Assignment1, which role should you assign to Admin1?**
**A:** *Resource Policy Contributor*. Resource Policy Contributor grants permissions to create and modify resource policy, create support ticket, and read resources and hierarchy.
- [[Design an Enterprise Governance Strategy#Compare and Contrast Azure RBAC vs Azure Policies|Compare and Contrast Azure RBAC vs Azure Policies]]

**Q: You have an Azure subscription that contains Microsoft Entra tenant and an Azure web app named App1. A user named User1 needs permission to manage App1, which role should you assign to User1?**
**A:** *Cloud Application Administrator*. Since App1 is an app in Azure, this role provides administrative permissions to App1.
- [[Secure Azure Solutions with Microsoft Entra ID]]

**Q: You have an Azure VNet named VNet1 in a resource group named RG1. VNet contains the following subnets:**
- Subnet1: 10.0.1.0/24
- Subnet2: 10.0.2.0/24
**You need to configure access to a storage account named sa1 in a resource group named RG2 and you must ensure that sa1 can only be accessed from Subnet2. What should you run?**
**A:** The correct CLI command adds a rule to allow access from the 10.0.2.0/24 subnet to the storage account.
`az storage account network-rule add --resource-group "RG2" --account-name "SA1" --ip-address "10.0.2.0/24" az storage account update --default-action deny --name sa1 --resource-group RG2`
- [[Configure Network Security]]

**Q: You have an Azure App Service web app named App1 and users authenticate to App1 by using Microsoft Entra. You plan to implement network security controls for App1 and need to ensure that only authenticated users from your corporate network can sign in to App1. The solution must not require the configuration of virtual network rules, which two actions should you perform?**
**A:** *Configure App Service authentication* and *Configure network conditions to Conditional Access*. You can configure the network conditions to Conditional Access, ensuring that the location is determined by the public IP address a client provides to Microsoft Entra or the GPS coordinates provided by the Microsoft Authenticator app. You need to configure App Service authentication, specifically the Action to take when request is not authenticated option.
- [[Deploy Microsoft Entra ID Protection]]
- [[Configure Network Security]]
- [[Authentication and authorization in Azure App Service and Azure Functions]]
- [[Using the location condition in a Conditional Access policy]]

**Q: You have a VNet that contains an Azure Kubernetes Service (AKS) workload and an internal load balancer. Multiple VNets are managed by multiple teams and you are unable to change any of the IP addresses. You need to ensure that clients from VNets in your Azure Subscription can access the AKS cluster by using the internal load balancer, what should you do?**
**A:** *Create a private link service on the virtual network and instruct users to access the cluster by using a private link endpoint in their virtual networks.* A private link service will allow access from outside the virtual network to an endpoint by using NAT. Since you do not control the IP addressing for other virtual networks, this ensures connectivity even if IP addresses overlap. Once a private link service is used in the load balancer, other users can create a private endpoint on virtual networks to access the load balancer. 
- [[Configure Network Security#Deploy Private Links|Deploy Private Links]]

**Q: You have an Azure subscription that contains the following resources:**
- Storage accounts
- Virtual Machines
- Azure Firewall
- Azure Key Vault
- Azure SQL Databases
**Which three resources support service endpoints?**
**A:** *Azure Key Vault*, *Azure SQL Databases*, and *storage accounts*. You can configure service endpoints for Azure Storage, Key Vault, and Azure SQL Database.
- [[Configure Network Security]]

**Q: You have a VM named VM1 and a storage account named storage1 and you need to ensure that VM1 can access storage1 over the Azure backbone network. What should you implement?**
**A:** *service endpoints*. Service endpoints route the traffic inside of Azure backbone, allowing access to the entire service, for example, all Microsoft SQL servers or the storage accounts of all customers.
- [[Integrate Azure Services with Virtual Networks for Network Isolation#Compare Private Endpoints and Service Endpoints|Compare Private Endpoints and Service Endpoints]]

**Q: You have a VNet named VNet1 which contains the following subnets:**
- Subnet1: Has a connected virtual machine
- Subnet2: Has a `Microsoft.Storage` service endpoint
- Subnet3: Has subnet delegation to the `Microsoft.Web/serverFarms` service
- Subnet4: Has no additional configurations
**You need to deploy an Azure SQL managed instance named managed1 to VNet1, which subnets can you connect managed1?**
**A:** *Subnet2, Subnet3, and Subnet4 only*. You can deploy an SQL managed instance to a dedicated virtual network subnet that does not have any resource connected. The subnet can have a service endpoint or can be delegated for a different service. For this scenario, you can deploy managed1 to Subnet2, Subnet3, and Subnet4 only. You cannot deploy managed1 to Subnet1 because Subnet1 has a connected virtual machine.
- [[Configure Network Security]]
- [[Connectivity Architecture for Azure SQL Managed Instance]]

**Q: You have an Azure App Service web app named App1 and need to configure network controls for App1. App1 must only allow user access through Azure Front Door, which two components should you implement?**
**A:** *access restrictions based on service tag* and *header filters*. Traffic from Front Door to the app originates from a well-known set of IP ranges defined in the `AzureFrontDoor.Backend` service tag. This includes every Front Door. To ensure traffic only originates from your specific instance, you will need to further filter the incoming requests based on the unique HTTP header that Front Door sends.
- [[Configure Network Security]]
- [[Set up Azure App Service access restrictions]]

**Q: You have a VM named VM1 which runs a web app named App1. You need to protect App1 by implementing Web Application Firewall (WAF), what resource should you deploy?**
**A:** *Azure Application Gateway*. WAF is a tier of Application Gateway. If you want to deploy WAF, you must deploy Application Gateway and select the WAF or WAF V2 tier.
- [[Configure Network Security#Implement an Azure Application Gateway|Implement an Azure Application Gateway]]
- [[What is Azure Application Gateway]]

**Q: **
**A:**

**Q: **
**A:**