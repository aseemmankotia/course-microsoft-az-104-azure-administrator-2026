## Chapter 5: Blob, Files, and Data Movement Tools — Practice Questions

**Q1.** A media company stores 50TB of blobs. They want blobs automatically moved to the Archive tier if they have not been READ or written for 90 days, and deleted entirely after 3 years. Which lifecycle management condition must they use to trigger the Archive tier move based on access patterns rather than modification date?

A) daysAfterLastAccessTimeGreaterThan
B) daysAfterModificationGreaterThan
C) daysAfterCreationGreaterThan
D) daysAfterLastTierChangeGreaterThan

<details>
<summary>Answer</summary>

**Correct: A**

daysAfterLastAccessTimeGreaterThan triggers actions based on last read access. It requires 'last access time tracking' to be enabled on the storage account; without it, this condition is unavailable.

**Why the others are wrong:**
- daysAfterModificationGreaterThan triggers on writes, not reads — a blob read daily but never rewritten would still age out incorrectly.
- daysAfterCreationGreaterThan only counts from blob creation, ignoring all subsequent access or modification.
- daysAfterLastTierChangeGreaterThan is only valid for the tierToCold action moving blobs FROM Archive, not for a Hot→Archive transition.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A retail company wants to replicate block blobs asynchronously from a storage account in East US to a storage account in West Europe for read-only disaster recovery access. They create the replication policy but it fails validation. What is the most likely missing configuration?

A) Enable soft delete on the destination account only
B) Enable static website hosting on both accounts
C) Enable blob versioning on the source AND destination accounts, and enable change feed on the source account
D) Convert both accounts to premium page blob storage accounts

<details>
<summary>Answer</summary>

**Correct: C**

Object replication requires blob versioning enabled on both source and destination accounts and change feed enabled on the source account. It only supports block blobs in GPv2 or premium block blob accounts.

**Why the others are wrong:**
- Soft delete is not a prerequisite for object replication and does not resolve policy creation failures.
- Static website hosting is unrelated to replication and has no bearing on the feature.
- Object replication does not require premium page blob accounts — page blobs are not even supported; only block blobs are replicated.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A legal team is under active litigation and must guarantee that a set of blobs cannot be deleted or modified until the case concludes, with no predetermined end date. Which storage feature should they apply?

A) A time-based retention immutability policy set for 10 years
B) Enable soft delete with a 365-day retention window
C) An Azure Resource Manager resource lock on the storage account
D) A legal hold immutability policy

<details>
<summary>Answer</summary>

**Correct: D**

Legal hold immutability policies block deletion or modification indefinitely until a user with sufficient permissions explicitly removes the hold — ideal when there is no known end date.

**Why the others are wrong:**
- Time-based retention requires a fixed expiration; litigation end dates are unknown, making this impractical and it would auto-expire.
- Soft delete only protects against accidental deletion for a limited window and can still be permanently purged or the policy disabled.
- An ARM resource lock protects the storage account resource from deletion/modification in the control plane, but does not prevent blob-level data operations within the account.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company runs a fleet of Linux VMs that require POSIX-compliant file permissions and native Linux file locking on a shared file system hosted in Azure. Which Azure Files configuration should they deploy?

A) Standard SMB Azure file share
B) NFS 4.1 Azure file share on a Premium FileStorage account
C) Blob storage with a block blob container mounted via BlobFuse
D) Standard SMB share with Azure AD Domain Services authentication

<details>
<summary>Answer</summary>

**Correct: B**

NFS 4.1 shares provide native POSIX permissions and file locking for Linux clients, but are only available on Premium (FileStorage) storage accounts and require access over a private endpoint or VNet — not public endpoints.

**Why the others are wrong:**
- SMB is optimized for Windows semantics; it lacks native POSIX permission support that Linux workloads expect.
- BlobFuse mounts blob storage as a filesystem but does not provide true POSIX permissions or file locking semantics.
- SMB with Azure AD DS provides Windows-style ACLs, not POSIX permissions required by Linux-native applications.

</details>

---

**Q5.** An organization wants storage account access restricted so only resources inside a specific subnet of their VNet can reach the storage account, with all other traffic denied by default, without requiring a private IP address on the storage account.

A) Deploy a private endpoint and remove all firewall rules
B) Generate a SAS token restricted to the subnet's IP range
C) Enable Azure AD Conditional Access on the storage account
D) Configure a service endpoint for Microsoft.Storage on the subnet and add a virtual network rule with default action set to Deny

<details>
<summary>Answer</summary>

**Correct: D**

A service endpoint for Microsoft.Storage combined with a storage account virtual network rule and default action of Deny restricts traffic to the specified subnet without giving the storage account a private IP.

**Why the others are wrong:**
- A private endpoint assigns a private IP to the storage account and is a valid alternative, but it is a heavier solution than required and the scenario specifically avoids a private IP requirement.
- SAS tokens control data-plane authorization, not network-level restriction — they cannot enforce subnet-only access.
- Storage accounts do not support Azure AD Conditional Access policies directly for network restriction; Conditional Access applies to Azure AD sign-ins, not storage REST/SMB endpoints.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator needs to mirror a local directory to a blob container so that files deleted locally are also removed from the destination, keeping both perfectly in sync. Which AzCopy command accomplishes this?

A) azcopy sync "C:\data" "https://acct.blob.core.windows.net/container" --delete-destination=true
B) azcopy copy "C:\data" "https://acct.blob.core.windows.net/container" --recursive=true
C) azcopy copy "C:\data" "https://acct.blob.core.windows.net/container" --overwrite=true
D) azcopy remove "https://acct.blob.core.windows.net/container" --recursive=true

<details>
<summary>Answer</summary>

**Correct: A**

azcopy sync with --delete-destination=true compares source and destination and removes destination files that no longer exist in the source, achieving true mirroring.

**Why the others are wrong:**
- azcopy copy --recursive uploads all files recursively but never deletes extra files at the destination — it is one-directional and additive only.
- azcopy copy --overwrite=true only controls whether existing destination files are replaced; it never removes files absent from the source.
- azcopy remove deletes blobs outright and does not perform any comparison or copy — it would wipe the destination, not sync it.

</details>

---

**Q7.** A compliance team locks a time-based retention immutability policy on a container to satisfy a 3-year regulatory requirement. Six months later, regulations change and they need to extend the retention period to 5 years. What is true about modifying a locked time-based retention policy?

A) Locked policies cannot be modified under any circumstances
B) The retention period can be freely increased or decreased at any time
C) The policy must be deleted and recreated to change the duration
D) The retention period can only be increased, never decreased, and this can be done up to 5 times

<details>
<summary>Answer</summary>

**Correct: D**

A locked time-based retention policy allows the retention interval to be extended (never shortened), and Azure limits this extension to a maximum of 5 times per policy.

**Why the others are wrong:**
- Locked policies can still be extended — 'locked' prevents deletion and shortening, not all modification.
- Decreasing the retention period on a locked policy is explicitly disallowed to preserve compliance guarantees.
- Locked policies cannot be deleted while active immutable data exists in the container; recreation is not the supported path for extension.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which blob container access level allows anonymous users to read individual blobs directly by URL, but does NOT allow them to list or enumerate the blobs contained in the container?

A) Blob (anonymous read access for blobs only)
B) Private (no anonymous access)
C) Container (anonymous read access for containers and blobs)
D) Public (full anonymous read and write)

<details>
<summary>Answer</summary>

**Correct: A**

The 'Blob' access level permits anonymous read of individual blobs when the exact URL is known, but does not expose container-level listing operations.

**Why the others are wrong:**
- Private disallows all anonymous access — even direct blob URLs require authentication or a SAS token.
- Container access level allows both anonymous blob reads AND full container/blob enumeration, which exceeds the requirement stated.
- There is no 'Public' access level with anonymous write in Azure Blob Storage — anonymous access is always read-only, and this option does not exist as a real setting.

</details>

---

