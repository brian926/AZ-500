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

**Q: **
**A:**

**Q: **
**A:**

**Q: **
**A:**

**Q: **
**A:**

**Q: **
**A:**