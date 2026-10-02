## Chapter 6: Virtual Machines: Deployment, Availability, and Disks — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Availability Set SLA vs Availability Zone SLA for VMs? | Availability Set: 99.95% (2+ VMs). Availability Zones: 99.99% (VMs across 2+ zones). Exam tip: single VM with Premium SSD/Ultra Disk only = 99.9%. |
| 2 | Default fault domains / update domains in a new Availability Set? | 3 fault domains (max in most regions), 5 update domains (max configurable = 20). Exam tests these exact defaults. |
| 3 | Max IOPS: Standard HDD vs Standard SSD vs Premium SSD vs Ultra Disk? | Standard HDD: ~2,000 IOPS. Standard SSD: ~6,000 IOPS. Premium SSD: ~20,000 IOPS. Ultra Disk: up to 400,000 IOPS, independently configurable. |
| 4 | Max managed disk size for Standard HDD/SSD and Premium SSD vs Ultra Disk? | Standard HDD/SSD and Premium SSD: up to 32,767 GiB. Ultra Disk: up to 65,536 GiB. Exam tip: Ultra Disk doubles max capacity. |
| 5 | SSE vs Azure Disk Encryption (ADE) — what's the key difference? | SSE encrypts at the storage platform layer automatically (always-on, AES-256, PMK or CMK). ADE encrypts inside the guest OS using BitLocker (Windows)/DM-Crypt (Linux), integrated with Key Vault. |
| 6 | When can you NOT use Azure Disk Encryption (ADE)? | ADE cannot be combined with 'Encryption at host' on the same VM, and has OS/distro compatibility restrictions. Exam tip: pick one encryption approach per VM. |
| 7 | Encryption at host — what does it encrypt that SSE doesn't? | Encrypts data on the VM host, including temp disks and OS/data disk caches — the gap left by standard SSE, which only covers managed disk data at rest. |
| 8 | Availability Set vs Availability Zone vs Scale Set — quick pick rule | Availability Set = protect within 1 datacenter (rack/host failure). Availability Zone = protect across datacenters in a region. Scale Set = auto-scaling identical VM instances, can span zones. |
| 9 | B-series VM use case (memory trick) | B = 'Burstable/Bank credits'. Accrues CPU credits when idle, spends them to burst. Best for dev/test, low-traffic web apps. Cheapest for spiky-idle workloads. |
| 10 | VM family cheat: D, E, F, M, L, N series | D=general purpose, E=memory optimized, F=compute optimized, M=large memory (SAP HANA), L=storage optimized (high disk I/O), N=GPU (AI/rendering). |
| 11 | Custom Script Extension vs DSC Extension | Custom Script Extension: runs an arbitrary script (bash/PowerShell) once at deployment/on-demand for config/setup. DSC Extension: applies and continuously enforces a PowerShell Desired State Configuration for ongoing compliance. |
| 12 | Azure Compute Gallery (Shared Image Gallery) — purpose? | Stores versioned custom VM images (image definitions + versions) and replicates them across regions/subscriptions for consistent, scalable image distribution to VMs and Scale Sets. |
