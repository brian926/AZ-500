## Network Micro-Segmentation

Micro-segmentation is a way to create secure zones in data centers and Azure deployments that allow you to isolate workloads and protect them individually. Security policies in a virtual environment can be assigned to virtual connections that can move with an application if the network is reconfigured – making the security policy persistent.

**A best practice recommendation is to adopt a Zero Trust strategy based on user, device, and application identities.** In contrast to network access controls that are based on elements such as source and destination IP address, protocols, and port numbers, Zero Trust enforces and validates access control at “access time”. 

- **Azure Network Security Groups** can be used for basic layer 3 & 4 access controls between Azure Virtual Networks, their subnets, and the Internet.
- **Application Security Groups** enable you to define fine-grained network security policies based on workloads, centralized on applications, instead of explicit IP addresses.
- **Azure Web Application Firewall** and the **Azure Firewall** can be used for more advanced network access controls that require application layer support.
- **Local Admin Password Solution (LAPS)** or a third-party Privileged Access Management can set strong local admin passwords and just in time access to them.

## Azure Network Conponents

Azure supports **dedicated WAN link connectivity** to your on-premises network and an Azure Virtual Network with ExpressRoute. The link between Azure and your site uses a dedicated connection that does not go over the public Internet.

## Azure DDoS Protection

Azure DDoS protection provides the following service tiers:

- Basic: Automatically enabled as part of the Azure platform, always-on traffic monitoring and real-time mitigation of common network-level attacks
- Standard: Provides additional mitigation capabilities over Basic. Protection policies are tuned through dedicated traffic monitoring and machine learning algorithms.

DDoS Protection Standard monitors actual traffic utilization and constantly compares it agaisnt the thresholds define in the DDoS policy and when threshold exceeded DDoS mitigation is automatically initiated.
Azure Monitor retains metric data for DDoS Protection Standard for 30 days.

DDoS Protection Standard can mitigate the following types of attacks:

- **Volumetric attacks**: The attack's goal is to flood the network layer with a substantial amount of seemingly legitimate traffic. It includes UDP floods, amplification floods, and other spoofed-packet floods. DDoS Protection Standard mitigates these potential multi-gigabyte attacks by absorbing and scrubbing them, with Azure's global network scale, automatically.
- **Protocol attacks**: These attacks render a target inaccessible, by exploiting a weakness in the layer 3 and layer 4 protocol stack. It includes, SYN flood attacks, reflection attacks, and other protocol attacks. DDoS Protection Standard mitigates these attacks, differentiating between malicious and legitimate traffic, by interacting with the client, and blocking malicious traffic.
- **Resource (application) layer attacks**: These attacks target web application packets, to disrupt the transmission of data between hosts. The attacks include HTTP protocol violations, SQL injection, cross-site scripting, and other layer 7 attacks. Use a Web Application Firewall, such as the Azure Application Gateway web application firewall, as well as DDoS Protection Standard to provide defense against these attacks. There are also third-party web application firewall offerings available in the Azure Marketplace.

## Azure Firewall
**Azure Firewall** is a managed, cloud-based network security service that protects Azure Virtual Network resources.

Azure firewall features include

- Built-in high availability: Because high availability is built in, no additional load balancers are required and there’s nothing you need to configure.
- Unrestricted cloud scalability: Azure Firewall can scale up as much as you need, to accommodate changing network traffic flows so you don't need to budget for your peak traffic.
- Application Fully Qualified Domain Name (FQDN) filtering rules: You can limit outbound HTTP/S traffic to a specified list of FQDNs, including wild cards. This feature does not require SSL termination.
- Network traffic filtering rules: You can centrally create allow or deny network filtering rules by source and destination IP address, port, and protocol. Azure Firewall is fully stateful, so it can distinguish legitimate packets for different types of connections. Rules are enforced and logged across multiple subscriptions and virtual networks.
- Qualified domain tags: Fully Qualified Domain Names (FQDN) tags make it easier for you to allow well known Azure service network traffic through your firewall.
- Outbound Source Network Address Translation (OSNAT) support: All outbound virtual network traffic IP addresses are translated to the Azure Firewall public IP.
- Inbound Destination Network Address Translation (DNAT) support: Inbound network traffic to your firewall public IP address is translated and filtered to the private IP addresses on your virtual networks.
- Azure Monitor logging: All events are integrated with Azure Monitor, allowing you to archive logs to a storage account, stream events to your Event Hub, or send them to Azure Monitor logs.

Grouping the features above into logical groups, Azure Firewall has three rule types: **NAT rules, network rules, application rules**.

The application order precedence for the rules are that networks rules are applied first, then application rules. Rules are terminating, which means if a match is found in network rules, then application rules are not processed. If there’s no network rule match, and if the packet protocol is HTTP/HTTPS, the packet is then evaluated by the application rules. If no match continues to be found, then the packet is evaluated against the infrastructure rule collection. If there’s still no match, then the packet is denied by default.

Threat intelligence-based filtering can be enabled for your firewall to alert and deny traffic from/to known malicious IP addresses and domains.
You can configure NAT rules,network rules, and applications rules on Azure Firewall. Rule collections are processed according to the rule type in priority order, lower numbers to higher numbers from 100 to 65,000.

## VPN Forced Tunneling
Forced tunneling lets you redirect, or force, all internet-bound traffic back to your on-premises location via a site-to-site VPN tunnel for inspection and auditing. Without forced tunneling, internet-bound traffic from VMs in Azure always traverses from the Azure network infrastructure directly to the internet.
You configure forced tunneling in Azure via virtual network **User Defined Routes (UDR)**. Redirecting traffic to an on-premises site is expressed as a default route to the Azure VPN gateway.

## User Defined Routes and Network Virtual Applicances
A User Defined Routes (UDR) is a custom route in Azure that overrides Azure's default system routes or adds routes to a subnet's route table.