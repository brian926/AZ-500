[Azure Custom Roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/custom-roles)

If the [Azure built-in roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles) don't meet the specific needs of your organization, you can create your own custom roles. Just like built-in roles, you can assign custom roles to users, groups, and service principals at management group, subscription, and resource group scopes.

Custom roles can be shared between subscriptions that trust the same Microsoft Entra tenant. There is a limit of **5,000** custom roles per tenant.

## Custom role properties

The following table describes what the custom role properties mean.

|Property|Required|Type|Description|
|---|---|---|---|
|`Name`  <br>`roleName`|Yes|String|The display name of the custom role. While a role definition is a management group or subscription-level resource, a role definition can be used in multiple subscriptions that share the same Microsoft Entra tenant. This display name must be unique at the scope of the Microsoft Entra tenant. Can include letters, numbers, spaces, and special characters. Maximum number of characters is 512.|
|`Id`  <br>`name`|Yes|String|The unique ID of the custom role. For Azure PowerShell and Azure CLI, this ID is automatically generated when you create a new role.|
|`IsCustom`  <br>`roleType`|Yes|String|Indicates whether this is a custom role. Set to `true` or `CustomRole` for custom roles. Set to `false` or `BuiltInRole` for built-in roles.|
|`Description`  <br>`description`|Yes|String|The description of the custom role. Can include letters, numbers, spaces, and special characters. Maximum number of characters is 2048.|
|`Actions`  <br>`actions`|Yes|String[]|An array of strings that specifies the control plane actions that the role allows to be performed. For more information, see [Actions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#actions).|
|`NotActions`  <br>`notActions`|No|String[]|An array of strings that specifies the control plane actions that are excluded from the allowed `Actions`. For more information, see [NotActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#notactions).|
|`DataActions`  <br>`dataActions`|No|String[]|An array of strings that specifies the data plane actions that the role allows to be performed to your data within that object. If you create a custom role with `DataActions`, that role can't be assigned at management group scope. For more information, see [DataActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#dataactions).|
|`NotDataActions`  <br>`notDataActions`|No|String[]|An array of strings that specifies the data plane actions that are excluded from the allowed `DataActions`. For more information, see [NotDataActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#notdataactions).|
|`AssignableScopes`  <br>`assignableScopes`|Yes|String[]|An array of strings that specifies the scopes that the custom role is available for assignment. Maximum number of `AssignableScopes` is 2,000. For more information, see [AssignableScopes](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#assignablescopes).|

Permission strings are case-insensitive. When you create your custom roles, the convention is to match the case that you see for permissions in [Azure resource provider operations](https://learn.microsoft.com/en-us/azure/role-based-access-control/resource-provider-operations).## Custom role properties

The following table describes what the custom role properties mean.

|Property|Required|Type|Description|
|---|---|---|---|
|`Name`  <br>`roleName`|Yes|String|The display name of the custom role. While a role definition is a management group or subscription-level resource, a role definition can be used in multiple subscriptions that share the same Microsoft Entra tenant. This display name must be unique at the scope of the Microsoft Entra tenant. Can include letters, numbers, spaces, and special characters. Maximum number of characters is 512.|
|`Id`  <br>`name`|Yes|String|The unique ID of the custom role. For Azure PowerShell and Azure CLI, this ID is automatically generated when you create a new role.|
|`IsCustom`  <br>`roleType`|Yes|String|Indicates whether this is a custom role. Set to `true` or `CustomRole` for custom roles. Set to `false` or `BuiltInRole` for built-in roles.|
|`Description`  <br>`description`|Yes|String|The description of the custom role. Can include letters, numbers, spaces, and special characters. Maximum number of characters is 2048.|
|`Actions`  <br>`actions`|Yes|String[]|An array of strings that specifies the control plane actions that the role allows to be performed. For more information, see [Actions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#actions).|
|`NotActions`  <br>`notActions`|No|String[]|An array of strings that specifies the control plane actions that are excluded from the allowed `Actions`. For more information, see [NotActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#notactions).|
|`DataActions`  <br>`dataActions`|No|String[]|An array of strings that specifies the data plane actions that the role allows to be performed to your data within that object. If you create a custom role with `DataActions`, that role can't be assigned at management group scope. For more information, see [DataActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#dataactions).|
|`NotDataActions`  <br>`notDataActions`|No|String[]|An array of strings that specifies the data plane actions that are excluded from the allowed `DataActions`. For more information, see [NotDataActions](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#notdataactions).|
|`AssignableScopes`  <br>`assignableScopes`|Yes|String[]|An array of strings that specifies the scopes that the custom role is available for assignment. Maximum number of `AssignableScopes` is 2,000. For more information, see [AssignableScopes](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-definitions#assignablescopes).|

Permission strings are case-insensitive. When you create your custom roles, the convention is to match the case that you see for permissions in [Azure resource provider operations](https://learn.microsoft.com/en-us/azure/role-based-access-control/resource-provider-operations).