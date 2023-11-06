[Plan a Microsoft Entra multifactor authentication deployment](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-getstarted)

Microsoft Entra multifactor authentication helps safeguard access to data and applications, providing another layer of security by using a second form of authentication. Organizations can enable multifactor authentication with [Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview) to make the solution fit their specific needs.

## Choose authentication methods for MFA
There are many methods that can be used for a second-factor authentication. You can choose from the list of available authentication methods, evaluating each in terms of security, usability, and availability.
- [Windows Hello for Business](https://learn.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/hello-overview)
- [Microsoft Authenticator app](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-authenticator-app)
- [FIDO2 security key (preview)](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-passwordless#fido2-security-keys)
- [OATH hardware tokens (preview)](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-oath-tokens#oath-hardware-tokens-preview)
- [OATH software tokens](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-oath-tokens#oath-software-tokens)
- [SMS verification](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-phone-options#mobile-phone-verification)
- [Voice call verification](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-phone-options)

For the best flexibility and usability, use the Microsoft Authenticator app. This authentication method provides the best user experience and multiple modes, such as passwordless, MFA push notifications, and OATH codes. The Microsoft Authenticator app also meets the National Institute of Standards and Technology (NIST) [Authenticator Assurance Level 2 requirements](https://learn.microsoft.com/en-us/entra/standards/nist-authenticator-assurance-level-2).