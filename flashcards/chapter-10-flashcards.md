## Chapter 10: Load Balancing, Routing, and Hybrid Connectivity — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Basic Load Balancer and Basic Public IP SKU retirement date? | September 30, 2025 — both retired for new deployments. Exam tip: assume Standard SKU is now the default/only choice for LB and Public IP going forward. |
| 2 | Application Gateway Standard/WAF v1 retirement date? | April 28, 2026 — migrate to Application Gateway v2/WAF_v2. Exam tip: v2 adds autoscaling and zone redundancy; v1 does not. |
| 3 | Standard Load Balancer max backend pool instances? | Up to 1000 instances. Exam tip: Standard SKU also gives 99.99% SLA and is secure-by-default (traffic denied unless allowed by NSG). |
| 4 | VpnGw1 vs VpnGw3 aggregate throughput? | VpnGw1 ≈ 650 Mbps; VpnGw3 ≈ 1.25 Gbps. Exam tip: throughput scales with SKU number; higher SKUs also support more S2S tunnels (30 for 1-3, 100 for 4-5). |
| 5 | Can you resize a VPN Gateway from Generation1 to Generation2? | No. Gateway Generation (Gen1: Basic-VpnGw3, Gen2: VpnGw2-VpnGw5) cannot be changed by resize — you must delete and recreate the gateway. |
| 6 | Azure Load Balancer vs Application Gateway — OSI layer? | Load Balancer = Layer 4 (TCP/UDP, IP+port routing). Application Gateway = Layer 7 (HTTP/HTTPS, URL-based routing, WAF, cookie-based session affinity). |
| 7 | Service Endpoint vs Private Endpoint — key architectural difference? | Service Endpoint: PaaS resource keeps its public IP, traffic routed via Azure backbone, scoped by subnet. Private Endpoint: NIC with private IP from your VNet mapped to the PaaS resource via Private Link, no public exposure needed. |
| 8 | UDR next hop types (list them) | Virtual network gateway, Virtual appliance, VNet (Virtual network), Internet, None. Exam tip: 'Virtual appliance' = force traffic to an NVA's private IP; 'None' = drop traffic (black hole route). |
| 9 | Application Gateway v2 autoscale instance range? | 0–125 instances (min capacity typically set ≥2 for production availability). Exam tip: v2 SKU autoscaling is a key differentiator from v1, which has fixed instance counts. |
| 10 | Standard Public IP allocation method? | Static only (no dynamic option). Exam tip: Basic SKU (retired) allowed dynamic or static; Standard SKU is always static and secure-by-default. |
| 11 | Private Endpoint DNS requirement? | Requires integration with a Private DNS Zone (e.g., privatelink.blob.core.windows.net) so the resource's FQDN resolves to the private IP instead of the public IP. |
| 12 | VNet Peering vs VPN Gateway VNet-to-VNet — when to use peering? | Use VNet Peering when you need low-latency, high-throughput Azure-backbone connectivity between VNets (same or different regions/subscriptions) without encryption overhead or gateway cost. Use VPN Gateway VNet-to-VNet when encryption or overlapping-scenario transit via gateway is required. |
