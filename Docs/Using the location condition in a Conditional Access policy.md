[Using the location condition in a Conditional Access policy](https://learn.microsoft.com/en-us/entra/identity/conditional-access/location-condition#ip-address-ranges)

Organizations can use these locations for common tasks like:
- Requiring multifactor authentication for users accessing a service when they're off the corporate network.
- Blocking access for users accessing a service from specific countries or regions your organization never operates from.

The location found using the public IP address a client provides to Microsoft Entra ID or GPS coordinates provided by the Microsoft Authenticator app. Conditional Access policies by default apply to all IPv4 and IPv6 addresses.

#### Trusted locations
Locations such as your organization's public network ranges can be marked as trusted. This marking is used by features in several ways.
- Conditional Access policies can include or exclude these locations.
- Sign-ins from trusted named locations improve the accuracy of Microsoft Entra ID Protection's risk calculation, lowering a user's sign-in risk when they authenticate from a location marked as trusted.
- Locations marked as trusted can't be deleted. Remove the trusted designation before attempting to delete