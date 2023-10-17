Identity Protection is a tool that allows organizations to automate the detection and remediation of identity-based risks, investigate risks using data in the portal, and export risk detection data to third-party utilities for further analysis.

## Explore Azure AD Identity Protection
Identity Protection is a tool that allows organizations to accomplish three key tasks:
- Automate the detection and remediation of identity-based risks.
- Investigate risks using data in the portal.
- Export risk detection data to third-party utilities for further analysis.

Risk detections in Azure AD Identity Protection include any identified suspicious actions related to user accounts in the directory. The signals generated that are fed to Identity Protection, can be further fed into tools like Conditional Access to make access decisions, or fed back to a security information and event management (SIEM) tool for further investigation based on your organization's enforced policies.

Azure Active Directory Identity Protection includes three default policies that administrators can choose to enable. These policies include limited customization but are applicable to most organizations. All the policies allow for excluding users such as your emergency access or break-glass administrator accounts.
![[Pasted image 20231016141851.png]]

Identity Protection can help organizations roll out Azure Multi-Factor Authentication using a Conditional Access policy requiring registration at sign-in. Multi-factor authentication is one of the self-remediation methods for risk events within Identity Protection. Self-remediation allows your users to act on their own to reduce helpdesk call volume.

Identity Protection analyzes signals from each sign-in, both real-time and offline, and calculates a risk score based on the probability that the sign-in wasn't performed by the user. Administrators can decide based on this risk score signal to enforce organizational requirements. Administrators can choose to block access, allow access, or allow access but require multi-factor authentication.

If risk is detected, users can perform multi-factor authentication to self-remediate and close the risky sign-in event to prevent unnecessary noise for administrators.

Administrators can also choose to create a custom Conditional Access policy, including sign-in risk as an assignment condition.

## Configure Risk Event Detections
To protect your users, you can configure risk-based policies in Azure Active Directory (Azure AD) that automatically respond to risky behaviors.
Some of the following actions may trigger Azure AD Identity Protection risk detection:  
- Users with leaked credentials.
- Sign-ins from anonymous IP addresses.
- Impossible travel to atypical locations.
- Sign-ins from infected devices.
- Sign-ins from IP addresses with suspicious activity.

The following three policies are available in Azure AD Identity Protection to protect users and respond to suspicious activity. You can choose to turn the policy enforcement on or off, select users or groups for the policy to apply to, and decide if you want to block access at sign-in or prompt for additional action.

The insight you get for a detected risk detection is tied to your Azure AD subscription.  
- **User risk policy** - Identifies and responds to user accounts that may have compromised credentials. Can prompt the user to create a new password.
- **Sign-in risk policy** - Identifies and responds to suspicious sign-in attempts. Can prompt the user to provide additional forms of verification using Azure AD Multi-Factor Authentication.
- **MFA registration policy** - Makes sure users are registered for Azure AD Multi-Factor Authentication. If a sign-in risk policy prompts for MFA, the user must already be registered for Azure AD Multi-Factor Authentication.

When you enable a policy user or sign-in risk policy, you can also choose the threshold for risk level - _**low and above**_, _medium and above_, or _**high**_. 

## Implement User Risk Policy
Identity Protection can calculate what it believes is normal for a user's behavior and use that to base decisions for their risk. User risk is a calculation of probability that an identity has been compromised. Administrators can decide based on this risk score signal to enforce organizational requirements. Administrators can choose to block access, allow access, or allow access but require a password change using Azure AD self-service password reset.

Configuration of **User Risk Policy** can be applied to
- User sign-ins
- Automatically respond based on a specific user’s risk level
- Provide the condition (risk level) and action (block or allow)
- Use a high threshold during policy roll out
- Use a low threshold for greater security

With the information provided by the risky users report, administrators can find:
- Which users are at risk, have had risk remediated, or have had risk dismissed?
- Details about detections
- History of all risky sign-ins
- Risk history

Administrators can then choose to act on these events. Administrators can choose to:
- Reset the user password
- Confirm user compromise
- Dismiss user risk
- Block user from signing in
- Investigate further using Azure ATP

## Implement Sign-In Risk Policy
Sign-in risk represents the probability that a given authentication request isn't authorized by the identity owner.

When configuring location as a condition, organizations can choose to include or exclude locations. These named locations may include the public IPv4 network information, country or region, or even unknown areas that don't map to specific countries or regions. Only IP ranges can be marked as a trusted location. When including **any location**, this option includes any IP address on the internet not just configured named locations. When selecting **any location**, administrators can choose to exclude **all trusted** or **selected locations**.

Conditional Access policies by default apply to browser-based applications and applications that utilize modern authentication protocols. In addition to these applications, administrators can choose to include Exchange ActiveSync clients and other clients that utilize legacy protocols.
- **Browser** - These include web-based applications that use protocols like SAML, WS-Federation, OpenID Connect, or services registered as an OAuth confidential client.
- **Mobile apps and desktop clients** - These access policies are commonly used when requiring a managed device, blocking legacy authentication, and blocking web applications but allowing mobile or desktop app.

The risky sign-ins report contains filterable data for up to the past 30 days (1 month).
With the information provided by the risky sign-ins report, administrators can find:
- Which sign-ins are classified as at risk, confirmed compromised, confirmed safe, dismissed, or remediated.
- Real-time and aggregate risk levels associated with sign-in attempts.
- Detection types triggered
- Conditional Access policies applied
- MFA details
- Device information
- Application information
- Location information
Administrators can then choose to take action on these events. Administrators can choose to:
- Confirm sign-in compromise
- Confirm sign-in safe

## Explore multifactor authentication settings
To prevent repeated MFA attempts as part of an attack, the account lockout settings let you specify how many failed attempts to allow before the account becomes locked out for a period of time. The account lockout settings are only applied when a pin code is entered for the MFA prompt. The following settings are available:
- Number of MFA denials to trigger account lockout
- Minutes until account lockout counter is reset
- Minutes until account is automatically unblocked

Fraud Alerts:
- **Block user when fraud is reported** - Configure the fraud alert feature so that your users can report fraudulent attempts to access their resources. Users can report fraud attempts by using the mobile app or through their phone. Block user when fraud is reported: If a user reports fraud, their account is blocked for 90 days or until an administrator unblocks their account. An administrator can review sign-ins by using the sign-in report and take appropriate action to prevent future fraud. An administrator can then unblock the user's account.
- **Code to report fraud during initial greeting** - Code to report fraud during initial greeting: When users receive a phone call to perform two-step verification, they normally press # to confirm their sign-in. To report fraud, the user enters a code before pressing #. This code is 0 by default, but you can customize it.

Trusted IPs is a feature to allow federated users or IP address ranges to bypass two-step authentication. Notice there are two selections in this screenshot.
Which selections you can make depends on whether you have managed or federated tenants.
- **Managed tenants**. For managed tenants, you can specify IP ranges that can skip MFA.
- **Federated tenants**. For federated tenants, you can specify IP ranges and you can also exempt AD FS claims users.

## Configure Conditional Access Conditions
Conditional access is a capability of Azure AD (with an Azure AD Premium license) that enables you to enforce controls on the access to apps in your environment based on specific conditions from a central location. With Azure AD conditional access, you can factor how a resource is being accessed into an access control decision. By using conditional access policies, you can apply the correct access controls under the required conditions.

Conditional access comes with six conditions: user/group, cloud application, device state, location (IP range), client application, and sign-in risk. You can use combinations of these conditions to get the exact conditional access policy you need. Notice on this image the conditions determine the access control from the previous topic.

With access controls, you can either Block Access altogether or Grant Access with more requirements by selecting the desired controls. You can have several options:

- Require MFA from Azure AD or an on-premises MFA (combined with AD FS).
- Grant access to only trusted devices.
- Require a domain-joined device.
- Require mobile devices to use Intune app protection policies.

Requiring more account verification through MFA is a common conditional access scenario. While users may be able to sign in to most of your organization’s cloud apps, you may want more verification for things like your email system, or apps that contain personnel records or sensitive information. In Azure AD, you can accomplish this with a conditional access policy