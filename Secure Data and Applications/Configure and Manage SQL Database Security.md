Two components of every secure database are authentication and authorization.
**Authentication** is the process of proving the user is who they claim to be. A user connects to a database using a user account. When a user attempts to connect to a database, they provide a user account and authentication information. The user is authenticated using one of the following two authentication methods:
- **SQL authentication** - With this authentication method, the user submits a user account name and associated password to establish a connection. This password is stored in the master database for user accounts linked to a login or stored in the database containing the user accounts not linked to a login.
- **Azure Active Directory Authentication** - With this authentication method, the user submits a user account name and requests that the service use the credential information stored in Azure Active Directory.

You can create user accounts in the master database, and grant permissions in all databases on the server, or you can create them in the database itself (called contained database users). By using contained databases, you obtain enhance portability and scalability.
**Logins and users**: In Azure SQL, a user account in a database can be associated with a login that is stored in the master database or can be a user name that is stored in an individual database.
- A **login** is an individual account in the master database, to which a user account in one or more databases can be linked. With a login, the credential information for the user account is stored with the login.
- A **user account** is an individual account in any database that may be but does not have to be linked to a login. With a user account that is not linked to a login, the credential information is stored with the user account.

**Authorization** to access data and perform various actions are managed using database roles and explicit permissions. Authorization refers to the permissions assigned to a user, and determines what that user is allowed to do. Authorization is controlled by your user account's database role memberships and object-level permissions. As a best practice, you should grant users the least privileges necessary. As a best practice, your application should use a dedicated account to authenticate. This way, you can limit the permissions granted to the application and reduce the risks of malicious activity in case the application code is vulnerable to a SQL injection attack. The recommended approach is to create a contained database user, which allows your app to authenticate directly to the database.
![[Pasted image 20231009104205.png]]

## Configure SQL Database Firewalls
Initially, all access to your Azure SQL Database is blocked by the SQL Database firewall. To access a database server, you must specify one or more server-level IP firewall rules that enable access to your Azure SQL Database.
To selectively grant access to just one of the databases in your Azure SQL Database, you must create a database-level rule for the required database. Specify an IP address range for the database IP firewall rule that is beyond the IP address range specified in the server-level IP firewall rule, and ensure that the IP address of the client falls in the range specified in the database-level rule.
![[Pasted image 20231009104916.png]]

When a computer attempts to connect to your database server from the internet, the firewall first checks the originating IP address of the request against the database-level IP firewall rules for the database that the connection is requesting:
- If the IP address of the request is within one of the ranges specified in the database-level IP firewall rules, the connection is granted to the SQL Database containing the rule.
- If the IP address of the request is not within one of the ranges specified in the database-level IP firewall rules, the firewall checks the server-level IP firewall rules. If the IP address of the request is within one of the ranges specified in the server-level IP firewall rules, the connection is granted. Server-level IP firewall rules apply to all SQL databases on the Azure SQL Database.
- If the IP address of the request is not within the ranges specified in any of the database-level or server-level IP firewall rules, the connection request fails.

To allow applications from Azure to connect to your Azure SQL Database, Azure connections must be enabled. When an application from Azure attempts to connect to your database server, the firewall verifies that Azure connections are allowed. A firewall setting with starting and ending addresses equal to 0.0.0.0 indicates Azure connections are allowed.
This option configures the firewall to allow all connections from Azure including connections from the subscriptions of other customers.

Server-level IP firewall rules enable clients to access your entire Azure SQL Database—that is, all the databases within the same SQL Database server. These rules are stored in the master database.
To create server-level IP firewall rules using the Azure portal or PowerShell, you must be the **subscription owner** or a **subscription contributor**. To create a server-level IP firewall rule using Transact-SQL, you must connect to the SQL Database instance as the server-level principal login or the Azure Active Directory (Azure AD) administrator (which means that a server-level IP firewall rule must have first been created by a user with Azure-level permissions).

Database-level IP firewall rules enable clients to access certain secure databases within the same SQL Database server. You can create these rules for each database (including the master database), and they are stored in the individual databases. You can only create and manage database-level IP firewall rules for master databases and user databases by using Transact-SQL statements, and only after you have configured the first server-level firewall. If you specify an IP address range in the database-level IP firewall rule that is outside the range specified in the server-level IP firewall rule, only those clients that have IP addresses in the database-level range can access the database. You can have a maximum of 128 database-level IP firewall rules for a database.

## Enable and Monitor Database Auditing
Auditing for Azure SQL Database and Azure Synapse Analytics tracks database events and writes them to an audit log in your Azure storage account, Log Analytics workspace or Event Hubs.

You can use SQL database auditing to:
- **Retain** an audit trail of selected events. You can define categories of database actions to be audited.
- **Report** on database activity. You can use pre-configured reports and a dashboard to get started quickly with activity and event reporting.
- **Analyze** reports. You can find suspicious events, unusual activity, and trends.

An auditing policy can be defined for a specific database or as a default server policy:
- A server policy applies to all existing and newly created databases on the server.
- If server auditing is enabled, it always applies to the database. The database will be audited, regardless of the database auditing settings.
- Enabling auditing on the database or data warehouse, in addition to enabling it on the server, does not override or change any of the settings of the server auditing. Both audits will exist side by side. In other words, the database is audited twice in parallel; once by the server policy and once by the database policy.

## Implement data discovery and classification
Data Discovery & Classification is part of the Advanced Data Security offering, which is a unified package for advanced SQL security capabilities. You can access and manage Data Discovery & Classification via the central **SQL Advanced Data Security** section of the Azure portal.
![[Pasted image 20231009105908.png]]

Data exists in one of three basic states: at **rest**, in **process**, and in **transit**. All three states require unique technical solutions for data classification, but the applied principles of data classification should be the same for each. Data that is classified as confidential needs to stay confidential when at rest, in process, or in transit.
Data can also be either **structured** or **unstructured**. Typical classification processes for structured data found in databases and spreadsheets are less complex and time-consuming to manage than those for unstructured data such as documents, source code, and email.

Data encryption at rest is a mandatory step toward data privacy, compliance, and data sovereignty.

|**Best practice**|**Solution**|
|---|---|
|Apply disk encryption to help safeguard your data.|Use Microsoft Azure Disk Encryption, which enables IT administrators to encrypt both Windows infrastructure as a service (IaaS) and Linux IaaS virtual machine (VM) disks. Disk encryption combines the industry-standard BitLocker feature and the Linux DM-Crypt feature to provide volume encryption for the operating system (OS) and the data disks. ‎Azure Storage and Azure SQL Database encrypt data at rest by default, and many services offer encryption as an option. You can use Azure Key Vault to maintain control of keys that access and encrypt your data.|
|Use encryption to help mitigate risks related to unauthorized data access.|Encrypt your drives before you write sensitive data to them.|
Organizations that don’t enforce data encryption are risk greater exposure to data-integrity issues.

For data moving between your on-premises infrastructure and Azure, consider appropriate safeguards such as HTTPS or VPN. When sending encrypted traffic between an Azure virtual network and an on-premises location over the public internet, use Azure VPN Gateway.

The following table lists best practices specific to using Azure VPN Gateway, SSL/TLS, and HTTPS.

|**Best practice**|**Solution**|
|---|---|
|Secure access from multiple workstations located on-premises to an Azure virtual network|Use site-to-site VPN.|
|Secure access from an individual workstation located on-premises to an Azure virtual network|Use point-to-site VPN.|
|Move larger data sets over a dedicated high-speed wide area network (WAN) link|Use Azure ExpressRoute. If you choose to use ExpressRoute, you can also encrypt the data at the application level by using SSL/TLS or other protocols for added protection.|
|Interact with Azure Storage through the Azure portal|All transactions occur via HTTPS. You can also use Storage REST API over HTTPS to interact with Azure Storage and Azure SQL Database.|

Organizations that fail to protect data in transit are more susceptible to man-in-the-middle attacks, eavesdropping, and session hijacking.

Discovering and classifying this data can play a pivotal role in your organizational information protection stature. It can serve as infrastructure for:
- Helping meet data privacy standards and regulatory compliance requirements.
- Addressing various security scenarios such as monitoring, auditing, and alerting on anomalous access to sensitive data.
- Controlling access to and hardening the security of databases containing highly sensitive data.

Classifications have two metadata attributes:
- **Labels** - These are the main classification attributes used to define the sensitivity level of the data stored in the column.
- **Information Types** - These provide additional granularity into the type of data stored in the column.
SQL data discovery and classification comes with a built-in set of sensitivity labels and information types, and discovery logic.

Definition and customization of your classification taxonomy takes place in one central location for your entire Azure Tenant. That location is in Microsoft Defender for Cloud, as part of your Security Policy. Only a user with **administrative** rights on the Tenant root management group can perform this task.

## Microsoft Defender for SQL
