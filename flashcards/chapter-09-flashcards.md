## Chapter 9: Virtual Networks, DNS, and Network Security — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | NSG rule priority range and evaluation order? | 100–4096, lower number = higher priority, evaluated first. First match wins, processing stops. Exam tip: a lower-priority-number Deny placed before a higher-priority-number Allow will block traffic even if the Allow rule would otherwise match. |
| 2 | Default NSG inbound rules (priority and name)? | 65000 AllowVNetInBound, 65001 AllowAzureLoadBalancerInBound, 65500 DenyAllInBound. Exam tip: these can't be deleted but CAN be overridden by custom rules with lower priority numbers. |
| 3 | Default NSG outbound rules (priority and name)? | 65000 AllowVNetOutBound, 65001 AllowInternetOutBound, 65500 DenyAllOutBound. |
| 4 | Is VNet peering transitive? | No. If A↔B and B↔C are peered, A cannot reach C automatically. Requires direct peering A↔C or routing via NVA/gateway in B. Heavily tested exam fact. |
| 5 | What does 'Gateway Transit' on a VNet peering do? | Allows a peered VNet to use the VPN/ExpressRoute gateway of the other VNet instead of deploying its own gateway. Set 'Use remote gateways' on the spoke side and 'Allow gateway transit' on the hub side. |
| 6 | NSG vs Azure Firewall — key capability difference? | NSG: stateful L3/L4 filtering by IP/port/protocol, no FQDN filtering, no threat intelligence, applied per subnet/NIC. Azure Firewall: managed stateful firewall with FQDN filtering, threat intelligence, centralized policy across VNets/subscriptions, DNAT/SNAT support. |
| 7 | Where can an NSG be associated? | A subnet and/or a network interface (NIC). If both have an NSG, traffic must be allowed by BOTH to pass. Exam trap: assuming only one NSG level applies. |
| 8 | How many IP addresses does Azure reserve in every subnet? | 5: network address, default gateway, two reserved for Azure DNS mapping, and the broadcast address. Minimum usable subnet size is /29 (8 addresses, 3 usable). |
| 9 | Azure Bastion subnet name and minimum size requirement? | Must be named exactly 'AzureBastionSubnet'. Minimum recommended size: /26. No NSG rules blocking required Bastion control-plane ports should be applied. |
| 10 | What is required to resolve names in a Private DNS zone from a VM in a VNet? | The VNet must have a virtual network link to the Private DNS zone. Optionally enable 'auto registration' so VM DNS records are created/updated/removed automatically. |
| 11 | Application Security Group (ASG) — what can it be used for? | Logical grouping of VM NICs by role (e.g., WebServers), referenced as source/destination in NSG rules instead of individual IPs. Constraint: NICs in an ASG referenced by an NSG rule must belong to the same VNet as the ASG. |
| 12 | Azure Bastion vs jump box VM — key exam differentiator? | Bastion is PaaS, needs no public IP on target VMs, no patching/management overhead, connects via Azure Portal/TLS 443. Jump box is an IaaS VM you must patch, secure, and often needs a public IP. |
