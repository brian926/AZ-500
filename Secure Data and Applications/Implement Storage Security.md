## Define Data Sovereignty
Data sovereignty is the concept that information, which has been converted and stored in binary digital form, is subject to the laws of the country or region in which it is located. Many of the current concerns that surround data sovereignty relate to enforcing privacy regulations and preventing data stored in a foreign country or region from being subpoenaed by the host coutnry or region's government.

Azure operates in multiple geographies around the world, an Azure Geography is a defined area of the world that contains at least one Azure Region, which is an area within a geography, containing one or more datacenters.
Each Azure region is paired with another region within the same geography, forming a regional pair. Across the region pairs Azure serializes platform updates (or planning maintenance), so that only one paired region is updated at a time.
![[Pasted image 20231008164853.png]]

## Configure Azure Storage Access
Every request made against a secured resource in the Blob, File, Queue, or Table service must be authorized. Authorization ensures that resources in your storage account are accessible only when you want them to be, and only to those users or applications to whom you grant access.

Options for authorizing requests to Azure Storage include:
- **Azure AD** - Azure Storage provides integration with Azure Active Directory (Azure AD) for identity-based authorization of requests to the Blob and Queue services. With Azure AD, you can use role-based access control (RBAC) to grant access to blob and queue resources to users, groups, or applications. You can grant permissions that are scoped to the level of an individual container or queue. Authorizing access to blob and queue data with Azure AD provides superior security and ease of use over other authorization options. When you use Azure AD to authorize requests make from your applications, you avoid having to store your account access key with your code, as you do with Shared Key authorization. While you can continue to use Shared Key authorization with your blob and queue applications, Microsoft recommends moving to Azure AD where possible.
- **Azure Active Directory Domain Services (Azure AD DS) authorization** for Azure Files. Azure Files supports identity-based authorization over Server Message Block (SMB) through Azure AD DS. You can use RBAC for fine-grained control over a client's access to Azure Files resources in a storage account
- **Shared Key** - Shared Key authorization relies on your account access keys and other parameters to produce an encrypted signature string that is passed on via the request in the Authorization header.
- **Shared Access Signatures** - A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. You can provide a shared access signature to clients who should not be trusted with your storage account key but to whom you wish to delegate access to certain storage account resources. By distributing a shared access signature URI to these clients, you can grant them access to a resource for a specified period of time, with a specified set of permissions. The URI query parameters comprising the SAS token incorporate all of the information necessary to grant controlled access to a storage resource. A client who is in possession of the SAS can make a request against Azure Storage with just the SAS URI, and the information contained in the SAS token is used to authorize the request.
- **Anonymous access to containers and blobs** - You can enable anonymous, public read access to a container and its blobs in Azure Blob storage. By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access. For more fine-grained control, look to using the shared access signature, described above.

Authenticating and authorizing access to blob and queue data with Azure AD provides superior security and ease of use over other authorization options.

## Deploy Shared Access Signatures
For untrusted clients, use a **shared access signature** (SAS), which is a string that contains a security token that can be attached to a URI. Use a shared access signature to delegate access to storage objects and specify constraints, such as permissions and the time range of access.

Types of shared access signatures:
- Use **service-level** shared access signature to allow access to specific resources in a storage account
- Use an **account-level** shared access signature to allow access to anything that a service-level shared access signature can allow, plus additional resources and abilities.
- A **user delegation SAS** is secured with Azure AD credentials. This type of SAS is supported for the Blob service only and can be used to grant access to containers and blobs.
Additionally, a service SAS can reference a stored access policy that provides an additional level of control over a set of signatures, including the ability to modify or revoke access to the resource if necessary.

One would typically use a shared access signature for a service where users read and write their data to your storage account. Accounts that store user data have two typical designs:
- Clients upload and download data through a front-end proxy service, which performs authentication. This front-end proxy service has the advantage of allowing validation of business rules. But if the service must handle large amounts of data or high-volume transactions, you might find it complicated or expensive to scale this service to match demand. ![[Pasted image 20231009100940.png]]
- A lightweight service authenticates the client as needed. Then it generates a shared access signature. After receiving the shared access signature, the client can access storage account resources directly. The shared access signature defines the client's permissions and access interval. The shared access signature reduces the need to route all data through the front-end proxy service. ![[Pasted image 20231009100952.png]]

## Manage Azure AD Storage Authentication
Azure Storage also supports using Azure Active Directory to authorize requests to blob data. With Azure AD, you can use Azure role-based access control to grant permissions to a security principal. The security principal is authenticated by Azure AD to return an OAuth 2.0 token. the token can then be used to authorize a request against the Blob service.
- To authorize requests against Azure Storage with Azure AD provides superior security and ease of use over Shared Key authorization.
- Authorization with Azure AD is available for all general-purpose and Blob storage accounts in all public regions and national clouds. Only storage accounts created with the Azure Resource Manager deployment model support Azure AD authorization.
- Blob storage additionally supports creating shared access signatures (SAS) that is signed with Azure AD credentials.
![[Pasted image 20231009101559.png]]

When a security principal (a user, group, or application) attempts to access a queue resource, the request must be authorized. With Azure AD, access to a resource is a two-step process. First, the security principal's identity is authenticated, and an OAuth 2.0 token is returned. Next, the token is passed as part of a request to the Queue service and used by the service to authorize access to the specified resource.

The authentication step requires that an application request an OAuth 2.0 access token at runtime. If an application is running from within an Azure entity, such as an Azure VM, a Virtual Machine Scale Set, or an Azure Functions app, it can use a managed identity to access queues.

The authorization step requires one or more Azure roles to be assigned to the security principal. Azure Storage provides Azure roles that encompass common sets of permissions for queue data. The roles that are assigned to a security principal determine the permissions that that principal will have.

Native and web applications that request the Azure Queue service can also authorize access with Azure AD.

## Implement Storage Service Encryption
Azure Storage provides a comprehensive set of security capabilities that together enable developers to build secure applications:
- All data (including metadata) written to Azure Storage is automatically encrypted using Storage Service Encryption (SSE).
- Azure Active Directory (Azure AD) and Role-Based Access Control (RBAC) are supported for Azure Storage for both resource management operations and data operations, as follows:
    - You can assign RBAC roles scoped to the storage account to security principals and use Azure AD to authorize resource management operations such as key management.
    - Azure AD integration is supported for blob and queue data operations. You can assign RBAC roles scoped to a subscription, resource group, storage account, or an individual container or queue to a security principal or a managed identity for Azure resources.
- Data can be secured in transit between an application and Azure by using Client-Side Encryption, HTTPS, or SMB 3.0.
- OS and data disks used by Azure virtual machines can be encrypted using Azure Disk Encryption.
- Delegated access to the data objects in Azure Storage can be granted using a shared access signature.

Azure Storage automatically encrypts your data when persisting it to the cloud. Data in Azure Storage is encrypted and decrypted transparently using 256-bit AES encryption, one of the strongest block ciphers available, and is FIPS 140-2 compliant. Azure Storage encryption is similar to BitLocker encryption on Windows.
Azure Storage encryption is enabled for all new and existing storage accounts and cannot be disabled.
All Azure Storage resources are encrypted, including blobs, disks, files, queues, and tables. All object metadata is also encrypted. Encryption does not affect Azure Storage performance. There is no additional cost for Azure Storage encryption.

You can rely on Microsoft-managed keys for the encryption of your storage account, or you can manage encryption with your own keys. If you choose to manage encryption with your own keys, you have two options:
- You can specify a _customer-managed_ key to use for encrypting and decrypting all data in the storage account. A customer-managed key is used to encrypt all data in all services in your storage account.
- You can specify a _customer-provided_ key on Blob storage operations. A client making a read or write request against Blob storage can include an encryption key on the request for granular control over how blob data is encrypted and decrypted.

The following table compares key management options for Azure Storage encryption.

|**Microsoft-managed keys**|**Customer-managed keys**|**Customer-provided keys**|
|---|---|---|---|
|Encryption/decryption operations|Azure|Azure|Azure|
|Azure Storage services supported|All|Blob storage, Azure Files|Blob storage|
|Key storage|Microsoft key store|Azure Key Vault|Azure Key Vault or any other key store|
|Key rotation responsibility|Microsoft|Customer|Customer|
|Key usage|Microsoft|Azure portal, Storage Resource Provider REST API, Azure Storage management libraries, PowerShell, CLI|Azure Storage REST API (Blob storage), Azure Storage client libraries|
|Key access|Microsoft only|Microsoft, Customer|Customer only|

## Configure Blob Data Retention Policies
Immutable storage for Azure Blob storage enables users to store business-critical data objects in a WORM (Write Once, Read Many) state. This state makes data non- erasable and non-modifiable for a user-specified interval. For the duration of the retention interval, blobs can be created and read, but cannot be modified or deleted. Immutable storage is available for general-purpose v2 and Blob storage accounts in all Azure regions.

Time-based vs Legal Hold Policies:
- **Time-based retention policy support**: Users can set policies to store data for a specified interval. When a time-based retention policy is set, blobs can be created and read, but not modified or deleted. After the retention period has expired, blobs can be deleted but not overwritten. When a time-based retention policy is applied on a container, all blobs in the container will stay in the immutable state for the duration of the effective retention period. The effective retention period for blobs is equal to the difference between the blob's creation time and the user-specified retention interval. Because users can extend the retention interval, immutable storage uses the most recent value of the user-specified retention interval to calculate the effective retention period.
- **Legal hold policy support**: If the retention interval is not known, users can set legal holds to store immutable data until the legal hold is cleared. When a legal hold policy is set, blobs can be created and read, but not modified or deleted. Each legal hold is associated with a user-defined alphanumeric tag (such as a case ID, event name, etc.) that is used as an identifier string. Legal holds are temporary holds that can be used for legal investigation purposes or general protection policies. Each legal hold policy needs to be associated with one or more tags. Tags are used as a named identifier, such as a case ID or event, to categorize and describe the purpose of the hold.

Other immutable storage features:
- **Support for all blob tiers**: WORM policies are independent of the Azure Blob storage tier and apply to all the tiers: hot, cool, and archive. Users can transition data to the most cost-optimized tier for their workloads while maintaining data immutability.
- **Container-level configuration**: Users can configure time-based retention policies and legal hold tags at the container level. By using simple container-level settings, users can create and lock time-based retention policies, extend retention intervals, set and clear legal holds, and more. These policies apply to all the blobs in the container, both existing and new.
- **Audit logging support**: Each container includes a policy audit log. It shows up to seven time-based retention commands for locked time-based retention policies and contains the user ID, command type, time stamps, and retention interval. For legal holds, the log contains the user ID, command type, time stamps, and legal hold tags. This log is retained for the lifetime of the policy, in accordance with the SEC 17a-4(f) regulatory guidelines. The Azure Activity Log shows a more comprehensive log of all the control plane activities; while enabling Azure Resource Logs retains and shows data plane operations. It is the user's responsibility to store those logs persistently, as might be required for regulatory or other purposes.

## Configure Azure files authentication
Azure Files supports identity-based authentication over Server Message Block (SMB) through on-premises Active Directory Domain Services (AD DS) and Azure Active Directory Domain Services (Azure AD DS).
Azure Files enforces authorization on user access to both the share and the directory/file levels. Share-level permission assignment can be performed on Azure Active Directory (Azure AD) users or groups managed through the role-based access control (RBAC) model. With RBAC, the credentials you use for file access should be available or synced to Azure AD. You can assign built-in RBAC roles like Storage File Data SMB Share Reader to users or groups in Azure AD to grant read access to an Azure file share.
At the directory/file level, Azure Files supports preserving, inheriting, and enforcing Windows DACLs just like any Windows file servers. You can choose to keep Windows DACLs when copying data over SMB between your existing file share and your Azure file shares. Whether you plan to enforce authorization or not, you can use Azure file shares to back up ACLs along with your data.

Identity-based authentication for Azure Files offers several benefits over using Shared Key authentication:
- Extend the traditional identity-based file share access experience to the cloud with on-premises AD DS and Azure AD DS. Azure Files supports using both on-premises AD DS or Azure AD DS credentials to access Azure file shares over SMB from either on-premises AD DS or Azure AD DS domain-joined VMs.
- Enforce granular access control on Azure file shares. You can grant permissions to a specific identity at the share, directory, or file level. For example, suppose that you have several teams using a single Azure file share for project collaboration. You can grant all teams access to non-sensitive directories while limiting access to directories containing sensitive financial data to your Finance team only.
- Back up Windows ACLs (also known as NTFS) along with your data. You can use Azure file shares to back up your existing on-premises file shares. Azure Files preserves your ACLs along with your data when you back up a file share to Azure file shares over SMB.

Identity-based authentication data flow:
![[Pasted image 20231009102702.png]]

Azure file shares leverages Kerberos protocol for authenticating with either on-premises AD DS or Azure AD DS. When an identity associated with a user or application running on a client attempts to access data in Azure file shares, the request is sent to the domain service, either AD DS or Azure AD DS, to authenticate the identity. If authentication is successful, it returns a Kerberos token. The client sends a request that includes the Kerberos token and Azure file shares use that token to authorize the request. Azure file shares only receive the Kerberos token, not access credentials.

Azure Files supports preserving directory or file level ACLs when copying data to Azure file shares. You can copy ACLs on a directory or file to Azure file shares using either Azure File Sync or common file movement toolsets. For example, you can use robocopy with the /copy:s flag to copy data as well as ACLs to an Azure file share. ACLs are preserved by default, you are not required to enable identity-based authentication on your storage account to preserve ACLs.

## Enable the Secure Transfer required property
You can configure your storage account to accept requests from secure connections only by setting the Secure transfer required property for the storage account. When you require secure transfer, any requests originating from an insecure connection are rejected.
Connecting to an Azure File share over SMB without encryption fails when secure transfer is required for the storage account.
**By default, the Secure transfer required property is enabled when you create a storage account**. Azure Storage doesn't support HTTPS for **custom domain names**, this option is not applied when you're using a custom domain name.

