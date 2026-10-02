# Chapter 8 Cheat Sheet: Containers & App Service

## Container Hosting Options
| Service | Orchestration | Autoscale | Scale-to-zero | Best For |
|---|---|---|---|---|
| Container Instances (ACI) | None | No | N/A (per-second billing) | Short-lived/batch, simple single-container jobs |
| Container Apps | KEDA-based | Yes (event-driven, HTTP, CPU/mem) | Yes | Microservices, Dapr, event-driven scaling, revisions/traffic split |
| App Service (containers) | None (single/multi via compose) | Yes (Standard+) | No | Web apps needing slots, custom domains/TLS, VNet integration |

## ACI Limits
- Default max per container group (Linux): 4 vCPU / 16 GB memory
- No built-in load balancing or orchestration — one container group = one deployable unit
- Billed per second of execution

## Azure Container Registry (ACR)
| SKU | Storage | Geo-replication | Notes |
|---|---|---|---|
| Basic | Lowest | No | Dev/test |
| Standard | Medium | No | Most production workloads |
| Premium | Highest | **Yes** | Content trust, private link, higher throughput |

- Admin user: disabled by default; avoid in production — use Managed Identity or service principal instead
- ACR Tasks: automate image build/push on git commit or base-image update — `az acr build`

## App Service Plan Tiers
| Tier | Scaling | Max Instances | Deployment Slots | Custom Domain TLS |
|---|---|---|---|---|
| Free (F1) | None | 1 | 0 | No |
| Shared (D1) | None | 1 | 0 | No |
| Basic (B1-B3) | Manual only | 3 | 0 | Yes |
| Standard (S1-S3) | Manual + Autoscale | 10 | 5 | Yes |
| Premium (Pv2/Pv3) | Manual + Autoscale | 30 | 20 | Yes |
| Isolated (I1-I3, ASE) | Manual + Autoscale | 100 | 20 | Yes |

**Exam Rule:** Autoscale requires Standard tier or higher. Deployment slots require Standard tier or higher.

## Deployment Slot Swap
- Swap warms up target slot before routing traffic (near zero-downtime)
- **Slot-sticky (does NOT swap):** custom domains, TLS/SSL bindings, scale settings, IP restrictions, WebJobs schedulers, Always On, VNet integration, managed identities
- App settings/connection strings: swap by default UNLESS explicitly checked as "Deployment slot setting"
- Command: `az webapp deployment slot swap --resource-group <rg> --name <app> --slot staging --target-slot production`

## Manual vs Automatic Scaling
- **Manual**: admin sets fixed instance count (available from Basic tier up, max 3 on Basic)
- **Autoscale**: rule-based (CPU/memory/schedule) auto add/remove instances (Standard tier+)

## Common Exam Traps
1. Choosing ACI for workloads that need autoscaling — ACI has none.
2. Assuming Basic tier supports deployment slots — it does not (Standard minimum).
3. Forgetting to mark connection strings as slot-sticky before a swap, causing production to point at the wrong database.
4. Confusing Container Apps (KEDA event-driven, Dapr, revisions) with App Service containers (slots, custom domains, VNet).
