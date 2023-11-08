[Compare Private Endpoints and Service Endpoints](https://learn.microsoft.com/en-us/azure/virtual-network/vnet-integration-for-azure-services#compare-private-endpoints-and-service-endpoints)

## Compare Private Endpoints and Service Endpoints
Rather than looking only at their differences, it's worth pointing out that both service endpoints and private endpoints have characteristics in common.

Both features are used for more granular control over the firewall on the target service. For example, restricting access to SQL Server databases or storage accounts. The operation is different for both though, as discussed in more detail in the previous sections.

Both approaches overcome the problem of [Source Network Address Translation (SNAT) port exhaustion](https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-outbound-connections#scenarios). You may find exhaustion when you're tunneling traffic through a Network Virtual Appliance (NVA) or service with SNAT port limitations. When you use service endpoints or private endpoints, the traffic takes an optimized path directly to the target service. Both approaches can benefit bandwidth intensive applications since both latency and cost are reduced.

In both cases, you can still ensure that traffic into the target service passes through a network firewall or NVA. This procedure is different for both approaches. When using service endpoints, you should configure the service endpoint on the **firewall** subnet, rather than the subnet where the source service is deployed. When using private endpoints you put a User Defined Route (UDR) for the private endpoint's IP address on the **source** subnet. Not in the subnet of the private endpoint.

To compare and understand the differences, see the following table.

|Consideration|Service Endpoints|Private Endpoints|
|---|---|---|
|Service scope at which level the configuration applies|Entire service (for example, _all_ SQL Servers or Storage accounts of _all_ customers)|Individual instance (for example, a specific SQL Server instance or Storage account _you_ own)|
|In-Built Data Exfiltration Protection - ability to move/copy data from protected PaaS resource to other unprotected PaaS resource by malicious insider|No|Yes|
|Private Access to PaaS resource from on-premises|No|Yes|
|NSG configuration required for Service Access|Yes (using Service Tags)|No|
|Service can be reached without using any public IP address|No|Yes|
|Azure-to-Azure traffic stays on the Azure backbone network|Yes|Yes|
|Service can disable its public IP address|No|Yes|
|You can easily restrict traffic coming from an Azure Virtual Network|Yes (allow access from specific subnets and or use NSGs)|Yes|
|You can easily restrict traffic coming from on-premises (VPN/ExpressRoute)|N/A**|Yes|
|Requires DNS changes|No|Yes (see [DNS configuration](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-dns))|
|Impacts the cost of your solution|No|Yes (see [Private link pricing](https://azure.microsoft.com/pricing/details/private-link/))|
|Impacts the [composite SLA](https://learn.microsoft.com/en-us/azure/architecture/framework/resiliency/business-metrics#composite-slas) of your solution|No|Yes (Private link service itself has a [99.99% SLA](https://azure.microsoft.com/support/legal/sla/private-link/))|
|Setup and maintenance|Simple to set up with less management overhead|Extra effort is required|
|Limits|No limit on the total number of service endpoints in a virtual network. Azure services may enforce limits on the number of subnets used for securing the resource. (see [virtual network FAQ](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#are-there-any-limits-on-how-many-service-endpoints-i-can-set-up-from-my-virtual-network))|Yes (see [Private Link limits](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#private-link-limits))|