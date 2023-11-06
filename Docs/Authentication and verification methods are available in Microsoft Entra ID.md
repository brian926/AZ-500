[Authentication and verification methods are available in Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods)

Microsoft recommends passwordless authentication methods such as Windows Hello, FIDO2 security keys, and the Microsoft Authenticator app because they provide the most secure sign-in experience. Although a user can sign-in using other common methods such as a username and password, passwords should be replaced with more secure authentication methods.

![[Pasted image 20231106134339.png]]

Microsoft Entra multifactor authentication adds additional security over only using a password when a user signs in. The user can be prompted for additional forms of authentication, such as to respond to a push notification, enter a code from a software or hardware token, or respond to a text message or phone call.

To simplify the user on-boarding experience and register for both MFA and self-service password reset (SSPR), we recommend you [enable combined security information registration](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-registration-mfa-sspr-combined). For resiliency, we recommend that you require users to register multiple authentication methods. When one method isn't available for a user during sign-in or SSPR, they can choose to authenticate with another method.