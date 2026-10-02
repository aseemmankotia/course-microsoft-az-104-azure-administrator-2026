## Chapter 10 Cheat Sheet — Load Balancing, Routing, Hybrid Connectivity

### Load Balancer vs Application Gateway
| Feature | Load Balancer | Application Gateway |
|---|---|---|
| OSI Layer | 4 (TCP/UDP) | 7 (HTTP/HTTPS) |
| Routing | IP + port | URL path, host header |
| WAF | No | Yes (WAF_v2 SKU) |
| SKUs | Basic (retired 9/30/25), Standard | v1 (retiring 4/28/26), v2 |
| Session affinity | 5-tuple hash | Cookie-based |

### Public IP SKUs
| SKU | Allocation | Status |
|---|---|---|
| Basic | Static/Dynamic | Retired 9/30/2025 |
| Standard | Static only | Default, secure-by-default (needs NSG allow) |

### Load Balancer Standard Limits
- Backend pool: up to 1000 instances
- SLA: 99.99%
- Health probe: TCP/HTTP/HTTPS; unhealthy threshold = consecutive failures before VM removed from rotation
- Must pair with Standard Public IP

### VPN Gateway SKUs (approx. throughput / max S2S tunnels)
| SKU | Throughput | Tunnels | Generation |
|---|---|---|---|
| Basic | 100 Mbps | 10 | Gen1 (legacy, no BGP) |
| VpnGw1 | 650 Mbps | 30 | Gen1 |
| VpnGw2 | 1 Gbps | 30 | Gen1 |
| VpnGw3 | 1.25 Gbps | 30 | Gen1 |
| VpnGw4 | 5 Gbps | 100 | Gen2 |
| VpnGw5 | 10 Gbps | 100 | Gen2 |

⚠️ Resize only within same generation. Cross-generation change = delete & recreate.

### Service Endpoint vs Private Endpoint
| Feature | Service Endpoint | Private Endpoint |
|---|---|---|
| IP assigned | None (resource keeps public IP) | Private IP (NIC) in your VNet |
| Traffic path | Azure backbone, scoped by subnet | Fully private via Private Link |
| DNS change | No | Yes — requires Private DNS Zone |
| Removes public endpoint | No | Effectively yes |

### UDR Next Hop Types
- **Virtual network gateway** — send to VPN/ExpressRoute GW
- **Virtual appliance** — send to NVA private IP
- **Virtual network (VNet)** — local VNet routing
- **Internet** — default system route
- **None** — black-hole/drop traffic

### Common Exam Gotchas
- Load Balancer cannot inspect HTTP payload — pick App Gateway for URL/WAF scenarios.
- Standard LB + Standard Public IP only — Basic and Standard SKUs cannot mix.
- Service endpoint ≠ private IP; don't confuse with Private Endpoint.
- VNet Peering is NOT transitive — VNet A ↔ B ↔ C does not let A reach C automatically.
- VPN Gateway resize across generations requires redeployment, not just a resize command.
