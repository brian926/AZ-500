Azure Active Directory (Azure AD) is Microsoft's cloud-based identity and access management service, which helps employee's sign in and access resources in:
- External resources, such as Microsoft 365, the Azure portal, and other SaaS applications
- Internal resources, such as apps on your corporate network and intranet, along with any cloud apps developed by your own organization.

## Azure Active Directory
Azure Active Directory (Azure AD) is a cloud-based identity and access management service. 
Azure AD pard licenses are built on top of your existing free directory. 
- Azure Active Directory Free - Provides user and group management, on-premises directory sync, basic reports, self-service password change for cloud users, and SSO across Azure, 365 and other SaaS apps
- Azure Active Directory Premium P1 - In addition to Free features, lets hybrid users access both on-premises and cloud resources.
- Azure Active Directory Premium P2 - In addition to Free and P1, also offers Azure Active Directory Identity Protection.
- Pay As You Go - Get additional feature licenses

## Self-managed ADD Services, AAD, and managed ADD Domain Services
Although the three Active Directory-based identity solutions share a common name and tech, they're designed to provide services that meet different customer demands.
1. Azure Active Directory (Azure AD) - Cloud based identity and mobile device management that provides user account and authentication services for resources such as Microsoft 365, Azure Portal, or SaaS app
	- Can sync with an on-premises AD DS env to provide a single identity to users that works natively in the cloud
2. Active Directory Domain Services (AD DS) - Enterprise-ready lightweight directory access protocol (LDAP) server that provides key features such as identity and authentication, computer object management, group policy, and trusts.
	- AD DS is a central component with on-premises IT env and provides core user account authentication and computer management features
3. Azure Active Directory Domain Services (Azure AD DS) - Provides managed domain services with a subset of fully compatible traditional AD DS features such as domain join, group policy, LDSP, and Kerberos / New Technology LAN Manager (NTLM) authentication
	- Azure AD DS integrates with Azure AD, which can sync with an on-premises AD DS env.

## Azure AD DS and self-managed AD DS
If you have applications that services that need access to traditional authentication mechanisms such as Kerberos or NTLM, there are two ways to provide Active Directory Domain Services in the Cloud:
- A *managed domain* that you create using Azure Active Directory Domain Services (Azure AD SD). Microsoft creates and manages the required resources
- A *self-managed* domain that you create and configure using traditional resources such as virtual machines (VMs), Windows Server guest OS, and Active Directory Domain Services (AD DS). You then continue to admin these resources.

With Azure AD DS, the core service components are deployed and maintained for you by Microsoft as *managed* domain experience. You don't deploy, manage, patch, and secure the AD DS infrastructure for components like the VMs, Windows Server OS, or domain controllers (DCs).
When you deploy and run a self-managed AD DS environment, you must maintain all of the associated infrastructure and directory components. Common deployment models for a self-managed AD DS environment that provides identity to applications and services in the cloud include the following:
- Standalone cloud-only AD DS - Azure VMs are configured as domain controllers, and a separate, cloud-only AD DS environment is created. This AD DS environment doesn't integrate with an on-premises AD DS environment. A different set of credentials is used to sign in and administer VMs in the cloud
- Resource forest deployment - Azure VMs are configured as domain controllers, and an AD DS domain that's part of an existing forest is created. A trust relationship is then configured to an on-premises AD DS environment. Other Azure VMs can domain-join this resource forest in the cloud. User authentication runs over a VPN/ExpressRoute connection to the on-premises AD DS environment.
- Extend on-premises domain to Azure - An Azure virtual network connects to an on-premises network using a VPN/ExpressRoute connection. Azure VMs connect to this Azure virtual network, which lets them domain-join to the on-premises AD DS environment
	- An alternative is to create Azure VMs and promote them as replica domain controllers from the on-premises AD DS domain. These domain controllers replicate over a VPN/ExpressRoute connection to the on-premises AD DS environment. The on-premises AD DS domain is effectively extended into Azure.

## Azure AD DS and Azure AD
Azure AD lets you manage the identity of devices used by the org and control access to corporate resources from those devices. 
Azure AD joined devices give you the following benefits:
- Single sign-on (SSO) to applications secured by Azure AD
- Enterprise policy-compliant roaming of user settings across devices
- Access to the Windows Store for Business using corporate credentials
- Windows Hello for Business
- Restricted access to apps and resources from devices compliant with corporate policy
Devices can be joined to Azure AD with or without a hybrid deployment that includes an on-premises AD DS environment.
On an Azure AD-joined or registered device, user authentication happens using modern OAuth/OpenID Connect-based protocols.

With Azure AD DS-joined devices, applications can use the Kerberos and New Technology LAN Manager (NTLM) protocols for authentication, so can support legacy applications migrated to run on Azure VMs as part of a lift-and-shift strategy.

If on-premises AD DS and Azure AD are configured for federated authentication using Active Directory Federation Services (ADFS), then there's no (current/valid) password hash available in Azure DS. Azure AD user accounts created before fed auth was implemented might have an old password hash that doesn't match a hash of their on-premises password. Hence Azure AD DS won't validate the user's credentials.

## Roles in Azure AD
Azure AD built-in roles fall into the following three broad categories
1. Azure AD-specific roles - Roles grant permissions to manage resources within Azure AD only
2. Service-specific roles - built service-specific roles that grant permissions to manage all features within the service.
3. Cross-service roles - Roles that span services, two global roles are Global Administrator and Global Reader.

## Deploy Azure AD Domain Services
Azure Active Directory Domain Services (Azure AD DS) provides managed domain services such as domain join, group policy, lightweight directory access protocol (LDAP), and Kerberos/New Technology LAN Manager (NTLM) authentication. You use these domain services without the need to deploy, manage, and patch domain controllers (DCs) in the cloud.
Azure AD DS integrates with your existing Azure AD tenant. This integration lets users sign in to services and applications connected to the managed domain using their existing credentials.

When you create an Azure AD DS managed domain, you define a unique namespace. This namespace is the domain name, such as _aaddscontoso.com_. Two Windows Server domain controllers (DCs) are then deployed into your selected Azure region. This deployment of DCs is known as a replica set.

You don't need to manage, configure, or update these DCs. The Azure platform handles the DCs as part of the managed domain, including backups and encryption at rest using Azure Disk Encryption.

A managed domain is configured to perform a one-way synchronization from Azure AD to provide access to a central set of users, groups, and credentials. You can create resources directly in the managed domain, but they aren't synchronized back to Azure AD. Applications, services, and VMs in Azure that connect to the managed domain can then use common AD DS features such as domain join, group policy, LDAP, and Kerberos/NTLM authentication.

In a hybrid environment with an on-premises AD DS environment, Azure AD Connect synchronizes identity information with Azure AD, which is then synchronized to the managed domain.

Azure AD DS replicates identity information from Azure AD, so it works with Azure AD tenants that are cloud-only or synchronized with an on-premises AD DS environment. The same set of Azure AD DS features exists for both environments.

-   If you have an existing on-premises AD DS environment, you can synchronize user account information to provide a consistent identity for users.
-   For cloud-only environments, you don't need a traditional on-premises AD DS environment to use the centralized identity services of Azure AD DS.

You can expand a managed domain to have more than one replica set per Azure AD tenant. Replica sets can be added to any peered virtual network in any Azure region that supports Azure AD DS.

To provide identity services to applications and VMs in the cloud, Azure AD DS is fully compatible with a traditional AD DS environment for operations such as domain-join, secure LDAP (LDAPS), Group Policy, DNS management, and LDAP bind and read support. LDAP write support is available for objects created in the managed domain but not resources synchronized from Azure AD.

The following features of Azure AD DS simplify deployment and management operations:
-   Simplified deployment experience: Azure AD DS is enabled for your Azure AD tenant using a single wizard in the Azure portal.
-   Integrated with Azure AD: User accounts, group memberships, and credentials are automatically available from your Azure AD tenant. New users, groups, or changes to attributes from your Azure AD tenant or your on-premises AD DS environment are automatically synchronized to Azure AD DS.
    -   Accounts in external directories linked to your Azure AD aren't available in Azure AD DS. Credentials aren't available for those external directories, so they can't be synchronized into a managed domain.
-   Use your corporate credentials/passwords: Passwords for users in Azure AD DS are the same as in your Azure AD tenant. Users can use their corporate credentials to domain-join machines, sign in interactively or over a remote desktop, and authenticate against the managed domain.
-   NTLM and Kerberos authentication: With support for NTLM and Kerberos authentication, you can deploy applications that rely on Windows-integrated authentication.
-   High availability: Azure AD DS includes multiple domain controllers, which provide high availability for your managed domain. This high availability guarantees service uptime and resilience to failures.
    -   In regions that support Azure Availability Zones, these domain controllers are distributed across zones for additional resiliency.
    -   Replica sets can also be used to provide geographical disaster recovery for legacy applications if an Azure region goes offline.

Some key aspects of a managed domain include the following:
-   The managed domain is a stand-alone domain. It isn't an extension of an on-premises domain.
    -   If needed, you can create one-way outbound forest trusts from Azure AD DS to an on-premises AD DS environment.
-   Your IT team doesn't need to manage, patch, or monitor domain controllers for this managed domain.

## Azure AD Groups
Azure Active Directory (Azure AD) provides several ways to manage access to resources, applications, and tasks. With Azure AD groups, you can grant access and permissions to a group of users instead of each individual user.

Some groups can't be managed in the Azure AD portal:
-   Groups synced from on-premises Active Directory can be managed only in on-premises Active Directory.
-   Distribution lists and mail-enabled security groups are managed only in Exchange admin center or Microsoft 365 admin center. You must sign in to the Exchange admin center or Microsoft 365 admin center to manage these groups.

There are **two group types** and **three group membership types**.
Group Types:
- **Security**: Used to manage user and computer access to shared resources.
- **Microsoft 365**: Provides collaboration opportunities by giving group members access to a shared mailbox, calendar, files, SharePoint sites, and more.
Membership Types:
-   **Assigned**: Lets you add specific users as members of a group and have unique permissions.
-   **Dynamic user**: Lets you use dynamic membership rules to automatically add and remove members. If a member's attributes change, the system looks at your dynamic group rules for the directory to see if the member meets the rule requirements (is added), or no longer meets the rules requirements (is removed).
-   **Dynamic device**: Lets you use dynamic group rules to automatically add and remove devices. If a device's attributes change, the system looks at your dynamic group rules for the directory to see if the device meets the rule requirements (is added), or no longer meets the rules requirements (is removed).

## Azure AD Admin Units
An administrative unit is an Azure AD resource that can be a container for other Azure AD resources. An administrative unit can contain only users and groups. Administrative units restrict permissions in a role to any portion of your organization that you define.

## Passwordless Authentication
Microsoft global Azure and Azure Government offer the following **three** passwordless authentication options that integrate with Azure Active Directory (Azure AD):
1.  Windows Hello for Business
2.  Microsoft Authenticator
3.  Fast Identity Online2 (**FIDO2**) security keys