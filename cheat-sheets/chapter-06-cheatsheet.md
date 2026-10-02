# Chapter 6 Cheat Sheet: VMs — Availability, Disks, Encryption

## Availability Options
| Option | Scope | Protects Against | SLA |
|---|---|---|---|
| Single VM (Premium SSD/Ultra) | 1 datacenter | Nothing beyond disk redundancy | 99.9% |
| Availability Set | 1 datacenter, spread across FD/UD | Rack/host/power/network failure | 99.95% |
| Availability Zones | Region, 3+ physical datacenters | Datacenter-level failure | 99.99% |
| VM Scale Set | Can span zones/FDs | Auto-scale + failure isolation | Matches underlying zone/set config |

**Availability Set defaults:** 3 fault domains (max, region-dependent), 5 update domains (max 20 configurable).

## Managed Disk Types
| Type | Max Size | Max IOPS | Max Throughput | Use Case |
|---|---|---|---|---|
| Standard HDD | 32,767 GiB | ~2,000 | ~500 MB/s | Backup, infrequent access, dev/test |
| Standard SSD | 32,767 GiB | ~6,000 | ~750 MB/s | Web servers, light enterprise apps |
| Premium SSD | 32,767 GiB | ~20,000 | ~900 MB/s | Production DBs, IO-intensive apps (needs premium-capable VM, Dsv3/Esv3+) |
| Ultra Disk | 65,536 GiB | Up to 400,000 | Up to 10,000 MB/s | Mission-critical DBs (SQL, SAP HANA), independently tunable IOPS/throughput without reboot |

**Exam rule of thumb:** Cost/performance order = Standard HDD < Standard SSD < Premium SSD < Ultra Disk.

## Encryption Comparison
| Feature | Layer | Key Management | Encrypts Temp Disk/Cache? | Notes |
|---|---|---|---|---|
| SSE (Storage Service Encryption) | Storage platform | Platform-managed (default) or CMK via Key Vault | No | Always on by default, AES-256, transparent |
| Azure Disk Encryption (ADE) | Guest OS | Customer keys in Key Vault (required) | No | BitLocker (Windows) / DM-Crypt (Linux); incompatible with Encryption at host |
| Encryption at Host | VM host | Platform-managed or CMK | Yes | No in-guest agent needed; covers gap SSE leaves (temp disk, caches) |

## VM Sizing Families (quick map)
- **B** = Burstable (dev/test, variable load)
- **D** = General purpose (balanced CPU/memory)
- **E** = Memory optimized (in-memory apps, caching)
- **F** = Compute optimized (batch, gaming, analytics)
- **M** = Large memory (SAP HANA, large DBs)
- **L** = Storage optimized (high disk throughput, NoSQL)
- **N** = GPU (AI/ML, rendering, CUDA)

## Azure Compute Gallery
- Replaces older 'Shared Image Gallery' naming.
- Structure: Gallery → Image Definition → Image Version.
- Supports multi-region replication and cross-subscription sharing with RBAC.
- Use for: standardized golden images, versioning/rollback, scale set image source.

## VM Extensions
- **Custom Script Extension**: one-time or on-demand script execution (bash/PowerShell) for post-deploy config.
- **DSC Extension**: applies and enforces ongoing PowerShell Desired State Configuration for continuous compliance drift correction.

## Common Exam Traps
1. Confusing Availability Set (single datacenter) with Availability Zone (multi-datacenter) scope.
2. Assuming SSE covers temp disk/cache encryption — it does not; that requires Encryption at host.
3. Trying to enable ADE and Encryption at host on the same VM (mutually exclusive).
