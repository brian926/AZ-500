You ensure that your application is registered, so it has a unique identity in Azure AD, then you can manage and control both access to the application and what the application can do.

## Microsoft Identity Platform
Microsoft identity platform is an evolution of the Azure Active Directory (Azure AD) developer platform, that allows developers to build applications that sign in users and get tokens to call APIs.
With the unified Microsoft identity platform (v2.0), you can write code once and authenticate any Microsoft identity into you application.
With the Microsoft identity platform, one can expand their reach to these kinds of users:
- Work and school accounts (Azure AD provisioned accounts)
- Personal accounts (such as Outlook.com or Hotmail.com)
- Your customers who bring their own email or social identity (such as LinkedIn, Facebook, and Google) via MSAL and Azure AD business-to-consumer (B2C)

The following diagram depicts the Microsoft identity experience at a high level, including the app registration experience, software development kits (SDKs), endpoints, and supported identities.
![[Pasted image 20231005093823.png]]

The Microsoft identity platform has two endpoints (v1.0 and v2.0); however, when developing a new application, consider it's highly recommended that you use the v2.0 (default) endpoint to benefit from the latest features and capabilities: 

The Microsoft Authentication Library can be used in many application scenarios, including the following:
- Single-page applications (JavaScript)
- Web app signing in users
- Web application signing in a user and calling a web API on behalf of the user
- Protecting a web API so only authenticated users can access it
- Web API calling another downstream Web API on behalf of the signed-in user
- Desktop application calling a web API on behalf of the signed-in user
- Mobile application calling a web API on behalf of the user who's signed in interactively.
- Desktop/service daemon application calling web API on behalf of itself

|**Library**|**Supported platforms and frameworks**|
|---|---|
|MSAL for Android|Android|
|MSAL Angular|Single-page apps with Angular and Angular.js frameworks|
|MSAL for iOS and macOS|iOS and macOS|
|MSAL Go (Preview)|Windows, macOS, Linux|
|MSAL Java|Windows, macOS, Linux|
|MSAL.js|JavaScript/TypeScript frameworks such as Vue.js, Ember.js, or Durandal.js|
|MSAL.NET|.NET Framework, .NET Core, Xamarin Android, Xamarin iOS, Universal Windows Platform|
|MSAL Node|Web apps with Express, desktop apps with Electron, Cross-platform console apps|
|MSAL Python|Windows, macOS, Linux|
|MSAL React|Single-page apps with React and React-based libraries (Next.js, Gatsby.js)|

Active Directory Authentication Library (ADAL) integrates with the Azure AD for developers (v1.0) endpoint, where MSAL integrates with the Microsoft identity platform. The v1.0 endpoint supports work accounts but not personal accounts. The v2.0 endpoint is unifying Microsoft personal accounts and works accounts into a single authentication system. Additionally, with MSAL, you can also get authentications for Azure AD B2C.

## Explore the Application model
For an identity provide to know that a user has access to a particular app, both the user and the application must be registered with the identity provider. When you register the application with **Azure Active Directory (Azure AD)**, you're providing an identity configuration for your application that allows it to integrate with the Microsoft identity platform.
Registering the app also allows you to:
- Customize the branding of your application in the sign-in dialog box. This branding is important because signing in is the first experience a user will have with your app.
- Decide if you want to allow users to sign in only if they belong to your organization. This architecture is known as a single-tenant application. Or, you can allow users to sign in by using any work or school account, which is known as a multi-tenant application. You can also allow personal Microsoft accounts or a social account from LinkedIn, Google, and so on.
- Request scope permissions. For example, you can request the "**user.read**" scope, which grants permission to read the profile of the signed-in user.
- Define scopes that define access to your web **application programming interface (API)**. Typically, when an app wants to access yourAPI, it will need to request permissions to the scopes you define.
- Share a secret with the Microsoft identity platform that proves the app's identity. Using a secret is relevant in the case where the app is a confidential client application. A confidential client application is an application that can hold credentials securely, like a web client. A trusted back-end server is required to store the credentials.

After the app is registered, it's given a unique identifier that it shares with the Microsoft identity platform when it requests tokens. If the app is a confidential client application, it will also share the secret or the public key depending on whether certificates or secrets were used.
The Microsoft identity platform represents applications by using a model that fulfills two main functions:
- Identify the app by the authentication protocols it supports.
- Provide all the identifiers, **Uniform Resource Locators (URLs)**, secrets, and related information that are needed to authenticate.

The Microsoft identity platform:
- Holds all the data required to support authentication at runtime.
- Holds all the data for deciding what resources an app might need to access, and under what circumstances a given request should be fulfilled.
- Provides infrastructure for implementing app provisioning within the app developer's tenant, and to any other Azure AD tenant.
- Handles user consent during token request time and facilitates the dynamic provisioning of apps across tenants.

Consent is the process of a resource owner granting authorization for a client application to access protected resources, under specific permissions, on behalf of the resource owner. The Microsoft identity platform enables:
- Users and administrators to dynamically grant or deny consent for the app to access resources on their behalf.
- Administrators to ultimately decide what apps are allowed to do and which users can use specific apps, and how the directory resources are accessed.

In the Microsoft identity platform, an **application object** describes an application. At deployment time, the Microsoft identity platform uses the application object as a blueprint to create a service principal, which represents a concrete instance of an application within a directory or tenant. The service principal defines what the app can actually do in a specific target directory, who can use it, what resources it has access to, and so on. The Microsoft identity platform creates a service principal from an application object through consent.
The following diagram shows a simplified Microsoft identity platform provisioning flow driven by consent. It shows **two tenants**: _**A**_ and _**B**_.
- _**Tenant A**_ owns the application.
- _**Tenant B**_ is instantiating the application via a service principal. ![[Pasted image 20231005100017.png]]
In this provisioning flow:
1. A user from tenant B attempts to sign in with the app. The authorization endpoint requests a token for the application.
2. The user credentials are acquired and verified for authentication.
3. The user is prompted to provide consent for the app to gain access to tenant B.
4. The Microsoft identity platform uses the application object in tenant A as a blueprint for creating a service principal in tenant B.
5. The user receives the requested token.

You can repeat this process for more tenants. Tenant A retains the blueprint for the **app (application object)**. Users and admins of all the other tenants where the app is given consent keep control over what the application is allowed to do via the corresponding service principal object in each tenant.

## Register an application with App Registration
For the most secure operation, register your app with the Microsoft identity platform.
Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure portal. Registration integrates your app with the Microsoft identity platform and establishes the information that it uses to get tokens, including:
- **Application ID**: A unique identifier assigned by the Microsoft identity platform.
- **Redirect URI/URL**: One or more endpoints at which your app will receive responses from the Microsoft identity platform. (For native and mobile apps, this is a URI assigned by the Microsoft identity platform.)
- **Application Secret**: A password or a public/private key pair that your app uses to authenticate with the Microsoft identity platform. (Not needed for native or mobile apps.)

## Configure Microsoft Graph permissions
Microsoft Graph exposes granular permissions that control the access that apps have to resources, like users, groups, and mail.
Microsoft Graph has two types of permissions:
- **Delegated permissions** are used by apps that have a signed-in user present. For these apps, either the user or an administrator consents to the permissions that the app requests, and the app can act as the signed-in user when making calls to Microsoft Graph. Some delegated permissions can be consented by non-administrative users, but some higher-privileged permissions require administrator consent.
- **Application permissions** are used by apps that run without a signed-in user present; for example, apps that run as background services or daemons. Application permissions can only be consented by an administrator.

Effective permissions are the permissions that your app will have when making requests to Microsoft Graph. It is important to understand the difference between the delegated and application permissions that your app is granted and its effective permissions when making calls to Microsoft Graph.
For delegated permissions, the effective permissions of your app will be the intersection of the delegated permissions the app has been granted (via consent) and the privileges of the currently signed-in user. Your app can never have more privileges than the signed-in user. Within organizations, the privileges of the signed-user can be determined by policy or by membership in one or more admin roles.

For example, assume your app has been granted the User.ReadWrite.All delegated permission. This permission nominally grants your app permission to read and update the profile of every user in an organization. If the signed-in user is a global administrator, your app will be able to update the profile of every user in the organization. However, if the signed-in user is not in an administrator role, your app will be able to update only the profile of the signed-in user. It will not be able to update the profiles of other users in the organization because the user that it has permission to act on behalf of does not have those privileges. For application permissions, the effective permissions of your app will be the full level of privileges implied by the permission. For example, an app that has the User.ReadWrite.All application permission can update the profile of every user in the organization.

You can use Microsoft Graph Security API to connect Microsoft security products, services, and partners to streamline security operations and improve threat protection, detection, and response capabilities. The Microsoft Graph Security API is an intermediary service (or broker) that provides a single programmatic interface to connect multiple Microsoft Graph Security provides (also called security providers or providers). The Microsoft Graph Security API federates requests to all providers in the Microsoft Graph Security ecosystem. This is based on the security provider consent provided by the application, as shown in the following diagram. The consent workflow only applies to non-Microsoft providers. 
![[Pasted image 20231005101108.png]]
The following is a description of the flow:
1. The application user signs in to the provider application to view the consent form from the provider. This consent form experience or UI is owned by the provider and applies to non-Microsoft providers only to get explicit consent from their customers to send requests to Microsoft Graph Security API.
2. The client consent is stored on the provider side.
3. The provider consent service calls the Microsoft Graph Security API to inform consent approval for the respective customer.
4. The application sends a request to the Microsoft Graph Security API.
5. The Microsoft Graph Security API checks for the consent information for this customer mapped to various providers.
6. The Microsoft Graph Security API calls all those providers the customer has given explicit consent to via the provider consent experience.
7. The response is returned from all the consented providers for that client.
8. The result set response is returned to the application.
9. If the customer has not consented to any provider, no results from those providers are included in the response.