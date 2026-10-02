## Chapter 10: Load Balancing, Routing, and Hybrid Connectivity — Practice Questions

**Q1.** A company runs a web application with multiple backend pools that must be routed based on URL path (/images/* vs /api/*), and traffic must be inspected for SQL injection and XSS attacks. Which solution BEST meets these requirements?

A) Application Gateway v2 with WAF and path-based routing rules
B) Azure Load Balancer Standard with multiple frontend IPs
C) Public IP with NSG rules restricting traffic by URL
D) Internal Load Balancer with HTTP health probes

<details>
<summary>Answer</summary>

**Correct: A**

Application Gateway operates at Layer 7, supports URL path-based routing to different backend pools, and the WAF_v2 SKU inspects HTTP traffic for OWASP threats like SQLi and XSS.

**Why the others are wrong:**
- Load Balancer operates at Layer 4 (TCP/UDP) and cannot inspect or route based on URL path or HTTP payload.
- NSGs filter based on IP/port/protocol 5-tuples, not URL paths or application-layer content.
- Internal Load Balancer is still Layer 4 and has no WAF or path-based routing capability.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company needs to connect an Azure VNet to on-premises via a Site-to-Site VPN requiring at least 1.25 Gbps aggregate throughput with BGP support. Which VPN Gateway SKU should they choose?

A) Basic
B) VpnGw3
C) VpnGw1
D) VpnGw2 with Basic Public IP

<details>
<summary>Answer</summary>

**Correct: B**

VpnGw3 provides ~1.25 Gbps aggregate throughput and supports BGP, meeting the stated requirement.

**Why the others are wrong:**
- Basic SKU caps at 100 Mbps, does not support BGP, and has been retired for new deployments.
- VpnGw1 caps at ~650 Mbps, below the 1.25 Gbps requirement.
- Basic Public IP SKU cannot be attached to a Standard VPN Gateway configuration and is also retired; VPN Gateways require Standard Public IPs.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company wants to restrict access to an Azure Storage account so that traffic from a specific VNet subnet stays on the Azure backbone, but they do not need to eliminate the storage account's public endpoint entirely. Which feature should they configure?

A) Private Endpoint
B) Service Endpoint
C) NSG service tag
D) VPN Gateway

<details>
<summary>Answer</summary>

**Correct: B**

Service Endpoints extend VNet identity to the storage service over the Azure backbone while the service retains its public IP; access can be scoped by subnet without removing the public endpoint.

**Why the others are wrong:**
- Private Endpoint assigns a private IP from the VNet and effectively removes reliance on the public endpoint — exceeds the stated requirement.
- NSG service tags only filter traffic at the network layer using IP ranges; they don't provide the Azure-backbone routing optimization service endpoints give.
- VPN Gateway is for hybrid on-prem connectivity, unrelated to securing PaaS service access from a VNet.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company needs to load balance traffic between three VMs in the same VNet for an internal database tier, with no exposure to the internet. Which configuration is correct?

A) Load Balancer Standard with an internal (private) frontend IP
B) Load Balancer Standard with a public frontend IP
C) Application Gateway with a public frontend IP
D) Public IP with Basic SKU assigned directly to each VM

<details>
<summary>Answer</summary>

**Correct: A**

An internal Load Balancer uses a private frontend IP from the VNet address space, distributing Layer 4 traffic between VMs without any internet exposure.

**Why the others are wrong:**
- A public frontend IP exposes the load balancer to the internet, violating the internal-only requirement.
- Application Gateway with a public frontend also exposes the service externally and is unnecessary Layer 7 overhead for a database tier.
- Assigning public IPs to each VM directly exposes every VM to the internet, which is the opposite of the requirement.

</details>

---

**Q5.** You need to force all outbound traffic from a subnet through a network virtual appliance (NVA) instead of the default internet route. Which next hop type should you configure in the user-defined route (UDR)?

A) Virtual appliance
B) Internet
C) Virtual network gateway
D) None

<details>
<summary>Answer</summary>

**Correct: A**

The 'Virtual appliance' next hop type routes traffic to the private IP address of an NVA, allowing inspection or custom routing before traffic leaves the subnet.

**Why the others are wrong:**
- 'Internet' is the default system route and does not redirect traffic to an NVA.
- 'Virtual network gateway' routes traffic to a VPN/ExpressRoute gateway, not an NVA.
- 'None' drops traffic entirely rather than routing it to an appliance.

</details>

---

**Q6.** Which statement correctly differentiates a Service Endpoint from a Private Endpoint?

A) Service endpoints assign a private IP to the PaaS resource; private endpoints keep the resource's public IP
B) Private endpoints assign a NIC with a private IP from the VNet to the PaaS resource; service endpoints keep the resource's public IP but route traffic over the Azure backbone
C) Both assign private IPs to the PaaS resource, but only private endpoints support NSGs
D) Service endpoints and private endpoints are functionally identical, differing only in name

<details>
<summary>Answer</summary>

**Correct: B**

Private Link/Private Endpoint creates a NIC with a private IP in your VNet mapped to the specific PaaS resource, fully removing reliance on the public endpoint. Service Endpoints simply optimize routing over the Azure backbone while the PaaS resource keeps its public IP.

**Why the others are wrong:**
- This reverses the definitions — service endpoints do NOT assign a private IP to the resource.
- Only private endpoints assign private IPs; service endpoints never do.
- They are architecturally different — one uses a NIC with private IP (Private Link), the other is a routing/firewall optimization (Service Endpoint).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A company has two VNets in different subscriptions that need low-latency, high-throughput connectivity without transiting the public internet, and does not require encryption at the network layer. Which solution is MOST appropriate?

A) VPN Gateway VNet-to-VNet connection
B) VNet Peering (including global peering if in different regions)
C) Point-to-Site VPN
D) ExpressRoute circuit

<details>
<summary>Answer</summary>

**Correct: B**

VNet Peering routes traffic through the Microsoft backbone network with low latency and high bandwidth, works across subscriptions and regions (global peering), and doesn't require gateway provisioning or encryption overhead.

**Why the others are wrong:**
- VPN Gateway VNet-to-VNet adds gateway cost/complexity and IPsec encryption overhead not required here; peering is simpler and faster.
- Point-to-Site VPN is for individual client connectivity, not VNet-to-VNet.
- ExpressRoute is for on-premises-to-Azure private connectivity, not VNet-to-VNet within Azure, and is far more costly/complex than needed.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** An Azure Load Balancer health probe is configured with an unhealthy threshold of 2. After the probe fails 2 consecutive times against a backend VM, what happens?

A) The VM is deallocated automatically
B) The load balancer rule is deleted
C) The VM is removed from the load balancer rotation until probes succeed again
D) Traffic continues to be sent but is logged as degraded

<details>
<summary>Answer</summary>

**Correct: C**

Once the unhealthy threshold of consecutive probe failures is reached, the Load Balancer marks the instance unhealthy and stops sending new traffic to it until subsequent probes succeed.

**Why the others are wrong:**
- The Load Balancer never deallocates VMs — that requires a separate action (e.g., autoscale or manual).
- Load balancing rules are configuration objects and are not deleted due to probe failures.
- Unhealthy instances stop receiving new flows; traffic is not merely logged, it is actively rerouted to healthy instances.

</details>

---

