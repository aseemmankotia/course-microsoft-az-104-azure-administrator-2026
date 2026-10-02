## Chapter 6: Virtual Machines: Deployment, Availability, and Disks — Practice Questions

**Q1.** A company runs a stateless web tier that must remain available if an entire Azure datacenter fails, and it must achieve a 99.99% VM uptime SLA. What should you deploy?

A) A single VM with Premium SSD managed disks
B) An availability set with two fault domains
C) Three or more VMs spread across Availability Zones in the region, behind a zone-redundant load balancer
D) A VM Scale Set with a single fault domain in one zone

<details>
<summary>Answer</summary>

**Correct: C**

Availability Zones map to physically separate datacenters with independent power/cooling/network. Spreading VMs across 3 zones with a Standard (zone-redundant) Load Balancer achieves the 99.99% SLA and survives full datacenter loss.

**Why the others are wrong:**
- A single VM only reaches 99.9% at best (Premium SSD/Ultra required) and has no redundancy against datacenter failure.
- Availability sets protect against rack/host failure within ONE datacenter, not a full datacenter outage — max SLA is 99.95%.
- A scale set confined to one zone/fault domain provides no protection against datacenter-level failure.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A database workload requires up to 300,000 IOPS and needs the ability to adjust IOPS and throughput independently of the provisioned disk capacity, without redeploying the VM. Which managed disk type meets this requirement?

A) Standard SSD
B) Ultra Disk
C) Premium SSD
D) Standard HDD

<details>
<summary>Answer</summary>

**Correct: B**

Ultra Disk supports up to 400,000 IOPS and lets you tune IOPS/throughput dynamically and independently of disk size, without a VM reboot.

**Why the others are wrong:**
- Standard SSD tops out around 6,000 IOPS — far below the requirement.
- Premium SSD tops out around 20,000 IOPS and performance scales with disk size, not independently adjustable on the fly.
- Standard HDD is the lowest-performance tier (max ~2,000 IOPS), used for infrequent/backup workloads.

</details>

---

**Q3.** A compliance policy requires that OS and data disk volumes be encrypted using BitLocker (Windows) or DM-Crypt (Linux), with encryption keys stored in and controlled through Azure Key Vault. Which feature satisfies this requirement?

A) Storage Service Encryption (SSE) with platform-managed keys
B) Encryption at host
C) Azure Disk Encryption (ADE)
D) SSE with customer-managed keys (CMK)

<details>
<summary>Answer</summary>

**Correct: C**

Azure Disk Encryption performs guest-OS-level encryption using BitLocker on Windows and DM-Crypt on Linux, and integrates directly with Key Vault for key management — exactly matching the requirement.

**Why the others are wrong:**
- SSE with platform-managed keys encrypts data at the storage layer transparently but does not use BitLocker/DM-Crypt and gives no customer key control.
- Encryption at host encrypts temp disks and host caches at the hypervisor level; it doesn't use BitLocker/DM-Crypt inside the guest OS.
- SSE with CMK still encrypts at the storage platform layer, not inside the guest OS with BitLocker/DM-Crypt.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A development team needs low-cost VMs for intermittent workloads that occasionally spike in CPU usage but are mostly idle. Which VM series should they choose?

A) D-series (general purpose)
B) F-series (compute optimized)
C) B-series (burstable)
D) M-series (memory optimized)

<details>
<summary>Answer</summary>

**Correct: C**

B-series VMs accrue CPU credits during idle periods and burst above the baseline when needed, making them the cheapest option for intermittent, spiky workloads.

**Why the others are wrong:**
- D-series provides consistent general-purpose performance but at higher steady-state cost with no credit-based bursting.
- F-series is optimized for sustained high CPU workloads (batch processing, gaming servers), not idle/burst patterns.
- M-series targets large in-memory databases (e.g., SAP HANA) — massively oversized and expensive for this scenario.

</details>

---

**Q5.** An organization built a custom hardened Linux image and needs to distribute versioned copies of it to VM Scale Sets in five Azure regions across two subscriptions, with support for image versioning and rollback. What should they use?

A) Copy the managed disk snapshot manually to each region
B) Azure Compute Gallery (formerly Shared Image Gallery)
C) Store the VHD in a Storage Account and share the SAS URL
D) Azure Marketplace private offer

<details>
<summary>Answer</summary>

**Correct: B**

Azure Compute Gallery is purpose-built for sharing and replicating versioned VM images across regions and subscriptions, with support for image definitions, versions, and controlled replication.

**Why the others are wrong:**
- Manually copying snapshots per region is unmanaged, doesn't support versioning, and doesn't scale.
- Sharing a raw VHD via SAS URL provides no versioning, access control granularity, or regional replication management.
- Marketplace private offers are for publishing commercial images to customers, not for internal multi-subscription image distribution.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** You create a new Availability Set in the Azure portal without changing default settings. What are the default fault domain and update domain counts?

A) 3 fault domains, 5 update domains
B) 2 fault domains, 20 update domains
C) 5 fault domains, 3 update domains
D) 1 fault domain, 10 update domains

<details>
<summary>Answer</summary>

**Correct: A**

The default availability set configuration is 3 fault domains (max in most regions with managed disks) and 5 update domains (configurable up to 20).

**Why the others are wrong:**
- Fault domain max is 3 (or 2 in some regions) — 20 update domains is a valid max but not the default of 5.
- 5 fault domains exceeds the maximum allowed (max is 2 or 3); the FD/UD counts are reversed.
- 1 fault domain provides zero redundancy and is not a valid availability set default.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which encryption feature specifically encrypts the temporary disk and the disk caches (for OS and data disks) at rest, using keys managed by the Azure platform, without requiring an in-guest agent?

A) Azure Disk Encryption (ADE)
B) Client-side encryption
C) SSE with customer-managed keys
D) Encryption at host

<details>
<summary>Answer</summary>

**Correct: D**

Encryption at host encrypts data on the VM host, including temp disks and OS/data disk caches, end-to-end, without needing an in-guest extension — and it's incompatible with ADE on the same VM.

**Why the others are wrong:**
- ADE requires an in-guest agent (BitLocker/DM-Crypt) and does not encrypt temp disk or host caches.
- Client-side encryption applies to data encrypted by the application before sending to storage, not VM disk caches.
- SSE with CMK encrypts managed disk data at rest in the storage layer, not the temp disk or host-level caches.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the fundamental difference between an Availability Set and an Availability Zone in Azure?

A) Availability Sets protect against region-wide failure; Availability Zones protect against rack failure only
B) Availability Sets distribute VMs across fault and update domains within a single datacenter; Availability Zones distribute VMs across physically separate datacenters within a region
C) There is no functional difference — they are interchangeable terms for the same feature
D) Availability Zones are only available for VM Scale Sets, while Availability Sets work for all compute resources

<details>
<summary>Answer</summary>

**Correct: B**

Availability Sets logically group VMs across fault domains (racks/power/network) and update domains within one datacenter. Availability Zones physically separate resources across distinct datacenters within the same region for higher resiliency.

**Why the others are wrong:**
- This reverses the actual scope — Availability Sets are datacenter-local, and neither protects against a full region outage (that requires region pairing/geo-redundancy).
- They are distinct features with different SLAs (99.95% vs 99.99%) and cannot be combined on the same VM deployment.
- Availability Zones are supported by VMs, VM Scale Sets, managed disks, load balancers, and more — not restricted to scale sets.

</details>

---

