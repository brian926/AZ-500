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

**Q: **
**A:**

**Q: **
**A:**

**Q: **
**A:**