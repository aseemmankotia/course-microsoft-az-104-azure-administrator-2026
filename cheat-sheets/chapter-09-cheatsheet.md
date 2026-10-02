# Chapter 9: VNets, DNS, and Network Security — Cheat Sheet

## NSG Rule Evaluation
| Aspect | Detail |
|---|---|
| Priority range | 100–4096 |
| Evaluation order | Lowest number first; first match wins, stops evaluation |
| Association levels | Subnet AND/OR NIC — both must allow traffic |
| Rule scope | Stateful; return traffic auto-allowed |

## Default NSG Rules
| Direction | Priority | Name | Effect |
|---|---|---|---|
| Inbound | 65000 | AllowVNetInBound | Allow from VirtualNetwork tag (includes peered VNets) |
| Inbound | 65001 | AllowAzureLoadBalancerInBound | Allow LB health probes |
| Inbound | 65500 | DenyAllInBound | Deny everything else |
| Outbound | 65000 | AllowVNetOutBound | Allow to VirtualNetwork tag |
| Outbound | 65001 | AllowInternetOutBound | Allow to Internet |
| Outbound | 65500 | DenyAllOutBound | Deny everything else |

**Exam trap:** Custom rules always override defaults if priority number is lower. Defaults can't be deleted, only overridden.

## VNet Peering
- **Non-transitive**: A↔B, B↔C does NOT give A↔C.
- **Gateway Transit**: spoke uses hub's VPN/ExpressRoute gateway. Configure 'Allow gateway transit' (hub) + 'Use remote gateways' (spoke).
- Peering must be created in **both directions** (two peering objects, one per VNet).
- No transitive resolution for on-premises via peered VNet unless gateway transit configured.

## NSG vs Azure Firewall vs ASG
| Feature | NSG | Azure Firewall | ASG |
|---|---|---|---|
| Layer | L3/L4 | L3–L7 (FQDN, app rules) | N/A (grouping only) |
| Threat intelligence | No | Yes | No |
| FQDN filtering | No | Yes | No |
| Scope | Subnet/NIC | VNet/Hub, cross-subscription via policy | Used inside NSG rules |
| Stateful | Yes | Yes | N/A |

## Azure DNS
| Zone Type | Use Case | Key Requirement |
|---|---|---|
| Public DNS zone | Internet name resolution | Domain delegation to Azure name servers |
| Private DNS zone | Internal VNet resolution | Must link to VNet(s); optional auto-registration |

**Exam trap:** A Private DNS zone with no VNet link resolves nothing for VMs — linking is mandatory, it's not automatic.

## Subnet Design
- Azure reserves **5 IPs** per subnet (network, gateway, 2x DNS, broadcast).
- Minimum subnet size: **/29** (8 addresses, 3 usable).
- Special subnets: `GatewaySubnet` (VPN/ExpressRoute gateway), `AzureBastionSubnet` (min **/26**), `AzureFirewallSubnet` (min /26).

## Azure Bastion
- PaaS, deployed in `AzureBastionSubnet` (exact name required).
- No public IP needed on target VMs.
- Connects via Azure Portal over TLS 443.
- Eliminates jump-box patching overhead.

## Application Security Groups (ASG)
- Group NICs logically (e.g., "WebTier").
- Reference ASG as source/destination in NSG rules instead of IP ranges.
- ASG and referencing NSG rule's NICs must be in the **same VNet**.

## Common Exam Traps Summary
1. Assuming VNet peering is transitive — it is NOT.
2. Forgetting NSGs apply at BOTH subnet and NIC level — both must permit traffic.
3. Confusing gateway transit (shares a gateway) with transitive routing (does not exist).
4. Forgetting Private DNS zones require an explicit VNet link.
5. Choosing NSG when the requirement needs FQDN filtering or threat intelligence — that's Azure Firewall's job.
