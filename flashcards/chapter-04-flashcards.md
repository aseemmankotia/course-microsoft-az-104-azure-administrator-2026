## Chapter 4: Storage Accounts: Redundancy, Tiers, and Secure Access — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Durability of LRS storage? | 11 nines (99.999999999%) annual durability. Exam tip: LRS = 3 copies in a single datacenter, cheapest option, no protection from datacenter-level disaster. |
| 2 | Durability of ZRS storage? | 12 nines (99.9999999999%). Data is replicated synchronously across 3 availability zones in the same region. Exam tip: protects against datacenter loss, not regional disaster. |
| 3 | Durability of GRS/GZRS storage? | 16 nines (99.99999999999999%) over a given year. Data is asynchronously copied to a secondary region. Exam tip: GZRS = ZRS in primary + LRS in secondary. |
| 4 | RA-GRS vs GRS? | GRS replicates to secondary region but secondary is not readable unless a failover occurs. RA-GRS (Read-Access GRS) exposes the secondary as a readable endpoint at all times. |
| 5 | Minimum retention period: Cool tier | 30 days. Deleting or moving blob out before 30 days incurs an early deletion fee. |
| 6 | Minimum retention period: Cold tier | 90 days. Sits between Cool and Archive in both cost and access latency. |
| 7 | Minimum retention period: Archive tier | 180 days. Blob is offline; must be rehydrated (Standard ≤15 hrs, High priority <1 hr for blobs under ~10GB) before it can be read. |
| 8 | Account SAS vs Service SAS vs User Delegation SAS | Account SAS: multi-service, account-key signed. Service SAS: single resource in one service, account-key or user delegation key signed. User Delegation SAS: Blob-only, signed with Entra ID-derived key instead of account key. |
| 9 | Maximum expiry for a user delegation SAS? | 7 days from time of creation — enforced regardless of the expiry time specified in the SAS, because the user delegation key itself has this max lifetime. |
| 10 | How many access keys does a storage account have, and how are they rotated safely? | Two keys (Key1, Key2), each 512-bit. Rotate by switching apps to the unused key first, then regenerating the other — avoids downtime. |
| 11 | Which resource types support a stored access policy? | Blob containers, file shares, queues, and tables. NOT supported for Account SAS — stored access policies only apply to service SAS on these four resource types. |
| 12 | Standard vs Premium performance tier | Standard = HDD-backed, general purpose, lower cost. Premium = SSD-backed, low-latency, used for Premium Block Blob, Premium Page Blob (disks), and Premium File Storage. Exam tip: Premium requires choosing the account type at creation and cannot mix tiers in one Standard account. |
