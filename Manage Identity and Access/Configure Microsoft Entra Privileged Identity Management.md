Azure AD Privileged Identity Management (PIM) allows you to manage, control, and monitor access to the most important resources in your organization. You can give just-in-time access and just-enough-access to users to allow them to do their tasks.

## Explore the Zero Trust Model
Based on the principle of “never trust, always verify,” Zero Trust helps secure corporate resources by eliminating unknown and unmanaged devices and limiting lateral movement. Implementing a true Zero Trust model requires that all components—user identity, device, network, and applications—be validated and proven trustworthy

In an ideal Zero Trust environment, the following four elements are necessary:
- Strong identity authentication everywhere (user verification via authentication)
- Devices are enrolled in device management, and their health is validated
- Least-privilege user rights (access is limited to only what is needed)
- The health of services is verified (future goal)

Representation of the primary elements that contribute to Zero Trust
![[Pasted image 20231018104218.png]]
Security policy enforcement is at the center of a Zero Trust architecture. This includes Multi-Factor authentication with conditional access that takes into account user account risk, device status, and other criteria and policies that you set.

Identities, devices (also called endpoints), data, applications, network, and other infrastructure components are all configured with appropriate security. Policies that are configured for each of these components are coordinated with your overall Zero Trust strategy.

To address this new world of computing, Microsoft highly recommends the Zero Trust security model, which is based on these guiding principles:
- **Verify explicitly** - Always authenticate and authorize based on all available data points.
- **Use least privilege access** - Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.
- **Assume breach** - Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses.

Below is a simplified reference architecture for our approach to implementing Zero Trust. The primary components of this process are Intune for device management and device security policy configuration, Azure AD conditional access for device health validation, and Azure AD for user and device inventory.

The system works with Intune, pushing device configuration requirements to the managed devices. The device then generates a statement of health, which is stored in Azure AD. When the device user requests access to a resource, the device health state is verified as part of the authentication exchange with Azure AD.
![[Pasted image 20231018104321.png]]

## Review the Evolution of Identity Management
**Microsoft Identity Manager** or MIM helps organizations manage the users, credentials, policies, and access within their organizations and hybrid environments. MIM enables Active Directory Domain Services to have the right users and access rights for on-premises apps. Azure AD Connect can then make those users and permissions available in Azure AD for Microsoft 365 and cloud-hosted apps.

Identity management approaches have evolved from traditional, to advanced, to optimal.
**Traditional identity approaches**
- On-premises identity providers.
- No single sign-on is present between on-premises and cloud apps.
- Visibility into identity risk is very limited.
**Advanced identity approaches**
- Conditional access policies gate access and provide remediation actions. 
- Analytics improve visibility into identity risk.
**Optimal identity approaches**
- Passwordless authentication is enabled.
- User, location, devices, and behavior are analyzed in real time.
- Continuous protection to identity risk.

Steps for a passwordless world:
- **Enforce MFA** — Conform to the fast identity online (FIDO) 2.0 standard, so you can require a PIN and a biometric for authentication rather than a password. Windows Hello is one good example, but choose the MFA method that works for your organization.
- **Reduce legacy authentication workflows** — Place apps that require passwords into a separate user access portal and migrate users to modern authentication flows most of the time. At Microsoft only 10 percent of our users enter a password on a given day.
- **Remove passwords** — Create consistency across Active Directory Domain Services and Azure Active Directory (Azure AD) to enable administrators to remove passwords from identity directory.

## Deploy Azure AD Privileged Identity Management
Privileged Identity Management (PIM) is a service in Azure Active Directory (Azure AD) that enables you to manage, control, and monitor access to important resources in your organization. These resources include resources in Azure AD, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune.

Here are some of the key features of Privileged Identity Management:
- Provide just-in-time privileged access to Azure AD and Azure resources
- Assign time-bound access to resources using start and end dates
- Require approval to activate privileged roles
- Enforce multi-factor authentication to activate any role
- Use justification to understand why users activate
- Get notifications when privileged roles are activated
- Conduct access reviews to ensure users still need roles
- Download audit history for internal or external audit
- Prevents removal of the last active Global Administrator and Privileged Role Administrator role assignments

For Azure AD roles in Privileged Identity Management, only a user who is in the Privileged **Role Administrator** or **Global Administrator role** can manage assignments for other administrators. Global Administrators, Security Administrators, Global Readers, and Security Readers can also view assignments to Azure AD roles in Privileged Identity Management.

## Configure privileged Identity Management Scope
The Privileged Identity Management (PIM) role assignments give you a secure way to grant access to resources in your organization.
PIM keeps you informed by sending you and other participants email notifications. These emails might also include links to relevant tasks, such as activating, approving, or denying a request.

The assignment process starts by assigning roles to members. To grant access to a resource, the administrator assigns roles to users, groups, service principals, or managed identities. The assignment includes the following data:
- The members or owners to assign the role.
- The scope of the assignment. The scope limits the assigned role to a particular set of resources.
- The type of the assignment
    - Eligible assignments require the member of the role to perform an action to use the role. Actions might include activation or requesting approval from designated approvers.
    - Active assignments don't require the member to perform any action to use the role. Members assigned as active have the privileges assigned to the role.
- The duration of the assignment, using start and end dates or permanent. For eligible assignments, the members can activate or request approval during the start and end dates. For active assignments, the members can use the assigned role during this period of time.

If users have been made eligible for a role, then they must activate the role assignment before using the role. To activate the role, users select a specific activation duration within the maximum (configured by administrators) and the reason for the activation request.
If the role requires approval to activate, a notification will appear in the upper right corner of the user's browser, informing them the request is pending approval. If approval isn't required, the member can start using the role.

Delegated approvers receive email notifications when a role request is pending their approval. Approvers can view, approve or deny these pending requests in PIM. After the request has been approved, the member can start using the role.

After administrators set up the time-bound owner or member assignments, the first question you might ask is, what happens if an assignment expires? In this new version, we provide two options for this scenario:
- **Extend** – When a role assignment nears expiration, the user can use Privileged Identity Management to request an extension for the role assignment
- **Renew** – When a role assignment has already expired, the user can use Privileged Identity Management to request a renewal for the role assignment
Both user-initiated actions require approval from a **Global Administrator** or **Privileged Role Administrator**. Admins don't need to be in the business of managing assignment expirations. You can wait for the extension or renewal requests to arrive for simple approval or denial.

Privileged Identity Management supports the following scenarios:
**Privileged Role Administrator permissions**
- Enable approval for specific roles
- Specify approver users or groups to approve requests
- View request and approval history for all privileged roles
**Approver permissions**
- View pending approvals (requests)
- Approve or reject requests for role elevation (single and bulk)
- Provide justification for my approval or rejection
**Eligible role user permissions**
- Request activation of a role that requires approval
- View the status of your request to activate
- Complete your task in Azure AD if activation was approved

## Implement Privileged Identity Management Onboarding
The first **Global Administrator** to use PIM in your instance of Microsoft Entra ID is automatically assigned the **Security Administrator** and **Privileged Role Administrator** roles in the directory. This person must be an eligible Microsoft Entra user. Only privileged role administrators can manage the Microsoft Entra directory role assignments of users. In addition, you can choose to run the security wizard that walks you through the initial discovery and assignment experience.

Users or members of a group assigned to the Owner or User Access Administrator roles, and Global Administrators that enable subscription management in Microsoft Entra ID, are Resource Administrators. These administrators can assign roles, configure role settings, and review access by using PIM for Azure resources.

No one else in your Microsoft Entra organization gets write access by default, though, including other Global administrators. Other Global administrators, Security administrators, and Security readers have read-only access to Privileged Identity Management. To grant access to Privileged Identity Management, the first user can assign others to the **Privileged Role Administrator** role.

## Explore Privileged Identity Management Configuration Settings
Activation Settings:
- **Activation duration**. Set the maximum time, in hours, that a role stays active before it expires. This value can be from one to 24 hours.
- **Require multifactor authentication on activation**. You can require users who are eligible for a role to prove who they are using Microsoft Entra multifactor authentication (MFA) before they can activate. Multifactor authentication ensures that the user is who they say they are with reasonable certainty. Enforcing this option protects critical resources in situations when the user account might have been compromised.
- **Require justification**. You can require that users enter a business justification when they activate.
- **Require approval to activate**. If setting multiple approvers, approval completes as soon as one of them approves or denies. You can't require approval from at least two users.

Assignment Settings:
- **Allow permanent eligible assignment**. Global admins and Privileged role admins can assign permanent eligible assignment. They can also require that all eligible assignments have a specified start and end date.
- **Allow permanent active assignment**. Global admins and Privileged role admins can assign active eligible assignment. They can also require that all active assignments have a specified start and end date.

Notification settings
- Notifications can be sent when members are assigned as eligible in a role, assigned as active in a role, and when the role is activated.
- Notifications can be sent to Admins, Requestors, and Approvers

## Implement a Privileged Identity Management Workflow
By configuring Microsoft Entra PIM to manage our elevated access roles in Microsoft Entra ID, we now have JIT access for more than 28 configurable privileged roles. We can also monitor access, audit account elevations, and receive additional alerts through a management dashboard in the Azure portal.

Elevated access includes job roles that need greater access, including support, resource administrators, resource owners, service administrators, and global administrators. We manage role-based access at the resource level. Because elevated access accounts could be misused if they’re compromised, we rationalize new requests for elevated access and perform regular re-attestation for elevated roles.
Diagram of elevated access workflow:
![[Pasted image 20231019075545.png]]

Permanent administrators have persistent elevated role connections; whereas eligible administrators have privileged access only when they need it. The eligible administrator role is inactive until the employee needs access, then they complete an activation process and become an active administrator for a set amount of time.

Microsoft Entra PIM uses administrative roles, such as tenant admin and global admin, to manage temporary access to various roles. With Microsoft Entra PIM, you can manage the administrators by adding or removing permanent or eligible administrators to each role. Microsoft Entra PIM includes several built-in Microsoft Entra roles as well as Azure that we manage.

To activate a role, an eligible admin will initialize Microsoft Entra PIM in the Azure portal and request a time-limited role activation. The activation is requested using the Activate my role option in Microsoft Entra PIM. Users requesting activation must satisfy conditional access policies to ensure that they are coming from authorized devices and locations, and their identities must be verified through multifactor authentication.

To help secure transactions while enabling mobility, we use Microsoft Entra PIM to customize role activation variables in Azure, including the number of sign-in attempts, the length of time the role is activated after sign-in, and the type of credentials required (such as single sign-in or multifactor authentication).

We can track how employees and admins are using their privileged roles by viewing the audit history or by setting up a regular access review. Both options are available through the PIM dashboard in the Azure portal.

The PIM audit log tracks changes in privileged role assignments and role activation history. We use the audit log to view all user assignments and activations within a specified period. The audit history helps us determine, in real time, which accounts haven’t signed in recently, or if employees have changed roles.

Access reviews can be performed by an assigned reviewer, or employees can review themselves. This is an effective way to monitor who still needs access, and who can be removed.