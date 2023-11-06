[Plan a Conditional Access deployment](https://learn.microsoft.com/en-us/entra/identity/conditional-access/plan-conditional-access)

[Microsoft Entra Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview) analyses signals such as user, device, and location to automate decisions and enforce organizational access policies for resources.
Microsoft provides [security defaults](https://learn.microsoft.com/en-us/entra/fundamentals/security-defaults) that ensure a basic level of security enabled in tenants that don't have Microsoft Entra ID P1 or P2. With Conditional Access, you can create policies that provide the same protection as security defaults, but with granularity. Conditional Access and security defaults aren't meant to be combined as creating Conditional Access policies will prevent you from enabling security defaults.

## Conditional Access policy components
Conditional Access policies answer questions about who can access your resources, what resources they can access, and under what conditions. Policies can be designed to grant access, limit access with session controls, or to block access. You [build a Conditional Access policy](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-policies) by defining the if-then statements

### Apply Conditional Access policies to every app
**Ensure that every app has at least one Conditional Access policy applied**. From a security perspective it's better to create a policy that encompasses **All cloud apps**, and then exclude applications that you don't want the policy to apply to. This practice ensures you don't need to update Conditional Access policies every time you onboard a new application.