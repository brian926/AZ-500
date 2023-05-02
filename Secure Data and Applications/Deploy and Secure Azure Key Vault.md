Azure Key Vault is offered in two service tiers - standard and premium.

Access to a key vault is controlled through two interfaces: the **management plane** and the **data plane**.
The management plane is where you manage the Key Vault itself. Operations include creating and deleting key vaults, retrieving Key Vault properties, and updating access policies.
The data plane is where you work with the data stored in a key vault. Add, delete, and modify keys, secrets, and certificates here.

Both planes user Azure AD for authentication. For authorization, the management plane uses RBAC, and the data plane can use either RBAC or a Key Vault access policy.
When you create a Key Vault in an Azure subscription, its automatically associated with the Azure AD tenant of the subscription. 
Applications can access Key Vault in two ways:
- **User plus application access** - The application access Key Vault on behalf of a signed-in user. Example of this type of access include Azure PowerShell and the Azure portal
- **Application-only access** - Application runs as daemon service or background job

## Deploy and manage Key Vault certificates

Key Vault certificates support provides for management of your x509 certificates and enables:

-   A certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate. Includes both self-signed and CA-generated certificates.
-   A Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.
-   A certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.
-   Certificate owners to provide contact information for notification about lifecycle events of expiration and renewal of certificate.
-   Automatic renewal with selected issuers - Key Vault partner X509 certificate providers and CAs.

When a Key Vault certificate is created, an addressable key and secret are also created with the same name. The Key Vault key allows key operations and the Key Vault secret allows retrieval of the certificate value as a secret. A Key Vault certificate also contains public x509 certificate metadata.

When a Key Vault certificate is created, it can be retrieved from the addressable secret with the private key in either PFX or PEM format. However, the policy used to create the certificate must indicate that the key is exportable. If the policy indicates non-exportable, then the private key isn't a part of the value when retrieved as a secret.
The addressable key becomes more relevant with non-exportable Key Vault certificates. The addressable Key Vault key’s operations are mapped from the `keyusage` field of the Key Vault certificate policy used to create the Key Vault certificate. If a Key Vault certificate expires, it’s addressable key and secret become inoperable.

Two types of key are supported – RSA or RSA HSM with certificates. Exportable is only allowed with RSA, and is not supported by RSA HSM.

## Create Key Vault Keys

Cryptographic keys in Key Vault are represented as JSON Web Key (JWK) objects. There are two types of keys, depending on how they were created.

-   **Soft keys**: A key processed in software by Key Vault, but is encrypted at rest using a system key that is in an Hardware Security Module (HSM). Clients may import an existing RSA or EC (Elliptic Curve) key, or request that Key Vault generate one.
-   **Hard keys**: A key processed in an HSM (Hardware Security Module). These keys are protected in one of the Key Vault HSM Security Worlds (there's one Security World per geography to maintain isolation). Clients may import an RSA or EC key, in soft form or by exporting from a compatible HSM device. Clients may also request Key Vault to generate a key.

## Customer Managed keys

Secrets can be rotated in several ways:
-   As part of a manual process
-   Programmatically by using REST API calls
-   Through an Azure Automation script

## Enable Key Vault secrets

Key Vault provides secure storage of secrets, such as passwords and database connection strings. Key Vault APIs accept and return secret values as strings. Internally, Key Vault stores and manages secrets as sequences of octets (8-bit bytes), with a maximum size of 25k bytes each. The values for Key Vault Secrets are:
-   Name-value pair - **Name must be unique in the Vault**
-   Value can be any UTF-8 string - max of 25 KB in size
-   Manual or certificate creation
-   Activation date
-   Expiration date

## Key Vaults safety and recovery featues

There are two prmiary functions to back up keys, certificates, and secrets from the Key Vault
- Azure Key Vault Soft-delete
- Key Vault Backup

