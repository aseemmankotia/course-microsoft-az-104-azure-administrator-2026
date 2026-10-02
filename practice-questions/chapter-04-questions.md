## Chapter 4: Storage Accounts: Redundancy, Tiers, and Secure Access — Practice Questions

**Q1.** A company's primary region storage account must remain readable by a reporting application even during a full regional outage, but the company wants the lowest-cost redundancy option that still provides this capability. Which redundancy option should they choose?

A) Zone-redundant storage (ZRS)
B) Read-access geo-redundant storage (RA-GRS)
C) Read-access geo-zone-redundant storage (RA-GZRS)
D) Locally-redundant storage (LRS)

<details>
<summary>Answer</summary>

**Correct: B**

RA-GRS replicates data asynchronously to a secondary region and exposes a read-only secondary endpoint, satisfying the read-during-outage requirement at a lower cost than RA-GZRS.

**Why the others are wrong:**
- ZRS only protects against zone failure within one region and offers no secondary region to read from during a regional outage.
- RA-GZRS provides the same read capability but adds zone redundancy in the primary region, which increases cost beyond what's required here.
- LRS keeps three copies in a single datacenter only — there's no secondary region and no read access during an outage.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A dataset is accessed roughly once every 3 to 4 months but must return data with millisecond latency whenever it's queried, and the retention commitment is at least 90 days. Which access tier BEST fits this pattern?

A) Cold
B) Hot
C) Cool
D) Archive

<details>
<summary>Answer</summary>

**Correct: A**

Cold tier is designed for infrequently accessed data (less often than Cool) that still requires online, millisecond access, with a minimum retention of 90 days matching the scenario.

**Why the others are wrong:**
- Hot tier is optimized for frequent access and has the highest storage cost, unnecessary for data accessed only quarterly.
- Cool tier has a 30-day minimum retention and is meant for slightly more frequent access than Cold, but its storage cost is higher than Cold for this access pattern.
- Archive tier is offline — it cannot deliver millisecond access; retrieval requires rehydration taking hours.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An administrator needs to urgently read a 5 GB blob currently stored in the Archive tier and must have it available within one hour. What should they do?

A) Change the blob's tier to Hot; it becomes readable immediately
B) Rehydrate the blob using Standard priority
C) Rehydrate the blob using High priority
D) Copy the blob to a new storage account with GRS redundancy

<details>
<summary>Answer</summary>

**Correct: C**

High-priority rehydration can retrieve blobs under roughly 10 GB in under one hour, meeting the urgent access requirement.

**Why the others are wrong:**
- Setting the tier does not make an archived blob instantly readable — it must be rehydrated first, which takes time regardless of the target tier.
- Standard priority rehydration can take up to approximately 15 hours, which does not meet the one-hour requirement.
- Copying does not bypass rehydration — the blob must be rehydrated before it can be copied or read, and redundancy is unrelated to retrieval speed.

</details>

---

**Q4.** A developer must generate a time-limited token that grants read access to a single blob container and is secured using the requesting user's Microsoft Entra ID credentials instead of the storage account key. Which SAS type should they use?

A) Account SAS
B) User delegation SAS
C) Service SAS signed with an account key
D) Stored access policy

<details>
<summary>Answer</summary>

**Correct: B**

A user delegation SAS is a service SAS secured with Microsoft Entra ID credentials via a user delegation key, and it applies to Blob storage (including Data Lake Storage Gen2).

**Why the others are wrong:**
- Account SAS is signed with the storage account key and can span multiple services, but it is not tied to Entra ID credentials.
- A service SAS signed with an account key uses the storage account key for signing, not Entra ID identity.
- A stored access policy is a server-side rule that can be associated with a SAS to control revocation, but it is not itself a SAS type or an Entra-based credential.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** An application needs a single access token that grants permissions across both the Blob and File services of a storage account, including the ability to create containers and shares. Which SAS type meets this requirement?

A) Service SAS
B) User delegation SAS
C) Account SAS
D) Stored access policy

<details>
<summary>Answer</summary>

**Correct: C**

Account SAS operates at the storage account level and can grant access to multiple services (Blob, File, Queue, Table) as well as account-level operations like creating containers.

**Why the others are wrong:**
- Service SAS is scoped to a single service and a specific resource within it, not multiple services at once.
- User delegation SAS only applies to the Blob service, not File or Queue.
- A stored access policy defines constraints for a service SAS on one resource type; it does not span multiple services or grant account-level operations.

</details>

---

**Q6.** A storage account currently authenticates all client applications using Access Key 1. The administrator wants to regenerate this key without causing any application downtime. What is the correct approach?

A) Update all applications to use Key 2, then regenerate Key 1
B) Regenerate Key 1 immediately; applications will reconnect automatically
C) Delete the storage account and recreate it with a new key
D) Disable access keys entirely and switch to Entra ID before regenerating

<details>
<summary>Answer</summary>

**Correct: A**

Storage accounts maintain two keys precisely for zero-downtime rotation: switch applications to the unused key (Key 2), then safely regenerate Key 1 without breaking active connections.

**Why the others are wrong:**
- Regenerating Key 1 while applications are actively using it immediately invalidates their connections, causing downtime.
- Deleting and recreating the account destroys existing data references and is unnecessary and destructive.
- Switching to Entra ID is a valid long-term security improvement but is a much larger change than what's needed to simply rotate a key without downtime.

</details>

---

**Q7.** A company sets a lifecycle policy to move blobs to the Archive tier after 60 days. A business need arises to delete one of these blobs only 45 days after it entered the Archive tier. What happens?

A) The blob deletes with no additional charge
B) The deletion is blocked entirely until 180 days have passed
C) The blob must first be rehydrated to Hot tier before it can be deleted
D) An early deletion fee applies because the blob was deleted before the 180-day minimum retention period

<details>
<summary>Answer</summary>

**Correct: D**

Archive tier has a minimum retention period of 180 days; deleting or moving the blob out of Archive before that incurs a prorated early deletion charge.

**Why the others are wrong:**
- Deletion is not free before the minimum retention period — an early deletion fee is charged.
- Azure does not block the deletion outright; it allows it but charges the early deletion fee.
- Rehydration is required to read blob content, not to delete it — a blob can be deleted directly from Archive tier.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the primary advantage of using a stored access policy in combination with a service SAS, compared to a standalone service SAS?

A) It allows access across multiple storage accounts
B) It removes the need to specify an expiry time
C) It grants Entra ID-based authentication automatically
D) It enables revocation or modification of the SAS permissions without regenerating the storage account key

<details>
<summary>Answer</summary>

**Correct: D**

A stored access policy centralizes constraints (permissions, start/expiry time) on the server side; changing or revoking the policy immediately affects all SAS tokens tied to it, without needing to regenerate account keys.

**Why the others are wrong:**
- Stored access policies are scoped to a single resource (e.g., one container, queue, table, or share) within one storage account, not across accounts.
- An expiry time can still be set on the stored access policy or the SAS itself; it is not eliminated.
- Stored access policies do not involve Entra ID authentication — that capability is specific to user delegation SAS.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

