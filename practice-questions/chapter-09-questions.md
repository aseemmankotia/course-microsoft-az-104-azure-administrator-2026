## Chapter 9: Virtual Networks, DNS, and Network Security — Practice Questions

**Q1.** A subnet has an NSG with these inbound rules: Priority 100 Deny Any from Any; Priority 200 Allow TCP 443 from Internet; Priority 65000 AllowVNetInBound. A client on the internet tries to reach a VM in the subnet on port 443. What happens?

A) Traffic is denied because rule 100 has a lower priority number and is evaluated first
B) Traffic is allowed because rule 200 permits port 443
C) Traffic is allowed because the default AllowVNetInBound rule takes precedence
D) Traffic is denied because there is no matching outbound rule

<details>
<summary>Answer</summary>

**Correct: A**

NSG rules are evaluated in order of priority number, lowest first. Priority 100 (Deny Any) is evaluated before priority 200, and processing stops at the first match — the deny wins.

**Why the others are wrong:**
- Rule 200 never gets evaluated because rule 100 already matched and denied the traffic first
- Default rules (65000+) are only evaluated if no custom rule matches; a custom rule always takes precedence over defaults
- Outbound rules are evaluated independently of inbound rules and don't affect this inbound decision

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** VNet-A is peered with VNet-B, and VNet-B is peered with VNet-C. VNet-A is NOT peered with VNet-C. A VM in VNet-A needs to communicate with a VM in VNet-C. What must you do?

A) Create a direct VNet peering between VNet-A and VNet-C, or route traffic through an NVA/gateway in VNet-B
B) Nothing — peering is transitive so VNet-A can already reach VNet-C through VNet-B
C) Enable 'Use remote gateways' on the VNet-A to VNet-B peering
D) Enable gateway transit on the VNet-B to VNet-C peering

<details>
<summary>Answer</summary>

**Correct: A**

VNet peering is non-transitive. VNet-A cannot reach VNet-C via VNet-B unless a direct peering exists between A and C, or traffic is routed through a network virtual appliance (NVA) or gateway sitting in VNet-B.

**Why the others are wrong:**
- Peering is explicitly non-transitive in Azure — this is one of the most heavily tested facts about VNet peering
- 'Use remote gateways' relates to gateway transit for VPN/ExpressRoute connectivity, not general transitive routing between spoke VNets
- Gateway transit only shares a VPN/ExpressRoute gateway with a peered VNet — it does not create transitive network reachability for regular VM-to-VM traffic

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company wants administrators to RDP and SSH into VMs in a VNet without assigning public IP addresses to any VM and without deploying a jump box VM they must patch and manage. Which service should they use?

A) Azure Firewall with a DNAT rule
B) A Network Security Group with an Allow rule for RDP/SSH from Any
C) Point-to-Site VPN Gateway
D) Azure Bastion

<details>
<summary>Answer</summary>

**Correct: D**

Azure Bastion is a fully managed PaaS service deployed in the VNet that provides RDP/SSH connectivity via the Azure Portal or native client over TLS, without needing public IPs on target VMs or a self-managed jump box.

**Why the others are wrong:**
- Azure Firewall DNAT can forward RDP/SSH but still requires opening a public-facing IP/port and doesn't remove management overhead the way Bastion does
- Allowing RDP/SSH from Any on an NSG exposes VMs directly to brute-force attacks and still requires a public IP on the VM
- Point-to-Site VPN requires client-side VPN software and certificate/configuration management on every admin's machine

</details>

---

**Q4.** You create a new NSG and attach it to a subnet without adding any custom rules. An administrator on a VM in a peered VNet (peering configured with default settings) tries to connect to a VM in this subnet. What is the outcome?

A) Allowed, because the default AllowVNetInBound rule (priority 65000) permits traffic from the entire virtual network address space, which includes peered VNets by default
B) Denied, because DenyAllInBound is the only default rule
C) Denied, because peered VNets are treated as Internet traffic by default
D) Allowed, only if 'Allow gateway transit' is enabled on the peering

<details>
<summary>Answer</summary>

**Correct: A**

The default AllowVNetInBound rule uses the VirtualNetwork service tag, which includes the local VNet's address space plus any peered VNets (as long as peering allows forwarded traffic, which is the default). No custom rule is needed for this to work.

**Why the others are wrong:**
- DenyAllInBound (priority 65500) is only evaluated if no higher-priority rule, including default rules above it, matches first
- Peered VNets are included in the VirtualNetwork service tag by default, not treated as Internet
- Gateway transit relates to sharing a VPN/ExpressRoute gateway, not to whether the VirtualNetwork service tag includes peered address spaces

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A company hosts an internal web app on a VM and wants other VMs in the same VNet to resolve 'app.internal.contoso.com' to that VM's private IP without managing DNS records manually. Which Azure DNS configuration should they use?

A) Create an Azure DNS public zone and add an A record pointing to the VM's private IP
B) Configure Azure DNS Traffic Manager with a weighted routing method
C) Create an Azure Private DNS zone, link it to the VNet, and enable auto registration
D) Use the VM's default Azure-provided DNS name only

<details>
<summary>Answer</summary>

**Correct: C**

A Private DNS zone linked to a VNet with auto-registration enabled automatically creates and maintains A records for VMs in that VNet as they are created, updated, or deleted — no manual record management required.

**Why the others are wrong:**
- Public DNS zones are for internet-facing name resolution and cannot resolve to private IPs for internal-only clients securely; also records still must be created manually
- Traffic Manager is a DNS-based traffic load balancer for distributing traffic across endpoints/regions, not for internal name resolution to a single VM
- Azure-provided DNS names are auto-generated (e.g., vmname.internal.cloudapp.net) and don't support a custom domain like contoso.com

</details>

---

**Q6.** A company needs to allow outbound traffic only to specific fully qualified domain names (FQDNs) like *.contoso.com, and requires centralized logging and threat intelligence-based filtering across multiple VNets in different subscriptions. Which solution meets these requirements?

A) Network Security Groups applied to each subnet
B) Application Security Groups
C) Azure Firewall with a firewall policy applied across the VNets
D) Azure DDoS Protection Standard

<details>
<summary>Answer</summary>

**Correct: C**

Azure Firewall supports FQDN-based filtering (application rules), threat intelligence-based filtering, and centralized policy management via Firewall Policy that can be applied across multiple VNets and subscriptions.

**Why the others are wrong:**
- NSGs filter by IP/port/protocol (L3/L4) only — they have no concept of FQDN filtering or threat intelligence
- ASGs are just logical groupings of NICs used as source/destination in NSG rules; they provide no filtering logic themselves and no FQDN or threat intel capability
- DDoS Protection Standard protects against volumetric/network-layer attacks; it does not do FQDN filtering or centralized policy for outbound traffic

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** You need to deploy Azure Bastion into a virtual network. Which of the following meets Microsoft's current requirements for the AzureBastionSubnet?

A) Any subnet name, with an address prefix of at least /29
B) A subnet named 'GatewaySubnet' with an address prefix of at least /27
C) A subnet named 'AzureBastionSubnet' with an address prefix of at least /24
D) A subnet named 'AzureBastionSubnet' with an address prefix of at least /26

<details>
<summary>Answer</summary>

**Correct: D**

Azure Bastion must be deployed in a dedicated subnet named exactly 'AzureBastionSubnet', and Microsoft's current guidance requires a minimum size of /26 to support Bastion's scaling and feature set.

**Why the others are wrong:**
- The subnet name must be exactly 'AzureBastionSubnet' — using a different name will prevent Bastion deployment
- 'GatewaySubnet' is reserved for VPN/ExpressRoute virtual network gateways, not Bastion
- /24 is larger than required; while it would technically work, /26 is the documented minimum, and the exam tests the minimum requirement, not an oversized one

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the primary purpose of an Application Security Group (ASG) in Azure networking?

A) To provide stateful Layer 7 firewall inspection for application traffic
B) To load balance traffic across application instances
C) To group virtual machine NICs logically by application role so they can be referenced as a single unit in NSG rules instead of individual IP addresses
D) To encrypt traffic between application tiers automatically

<details>
<summary>Answer</summary>

**Correct: C**

An ASG lets you group VM NICs (e.g., all 'WebServers' or all 'SQLServers') and use that group name as the source or destination in NSG rules, simplifying rule management as the environment scales instead of hardcoding individual IPs.

**Why the others are wrong:**
- ASGs provide no Layer 7 inspection or filtering logic on their own — that capability belongs to Azure Firewall or a WAF
- Load balancing is handled by Azure Load Balancer or Application Gateway, not ASGs
- ASGs have no encryption function; they are purely a logical grouping construct for NSG rule targeting

</details>

---

