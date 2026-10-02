# Chapter 4 Cheat Sheet: Storage Redundancy, Tiers & Secure Access

## Redundancy Options
| Option | Copies | Scope | Durability | Read Secondary? |
|---|---|---|---|---|
| LRS | 3 | Single datacenter | 11 nines | No |
| ZRS | 3 | 3 AZs, same region | 12 nines | No |
| GRS | 3+3 | Primary + secondary region (async) | 16 nines | No (unless failover) |
| RA-GRS | 3+3 | Same as GRS | 16 nines | Yes |
| GZRS | 3+3 | ZRS primary + LRS secondary | 16 nines | No (unless failover) |
| RA-GZRS | 3+3 | Same as GZRS | 16 nines | Yes |

**Exam note:** Geo-redundant options require the storage account region pair; failover changes secondary → primary and is either customer-initiated (unplanned) or Microsoft-initiated.

## Access Tiers
| Tier | Storage Cost | Access Cost | Min Retention | Access Latency |
|---|---|---|---|---|
| Hot | Highest | Lowest | None | Immediate |
| Cool | Lower | Higher | 30 days | Immediate |
| Cold | Lower still | Higher | 90 days | Immediate |
| Archive | Lowest | Highest | 180 days | Hours (rehydration) |

**Rehydration priority:** Standard (≤15 hrs), High (<1 hr, blobs <~10GB).

**Rule of thumb:** Accessed daily → Hot. Monthly-ish → Cool. Quarterly-ish → Cold. Rarely (<once/year) → Archive.

## SAS Types
| Type | Scope | Signed With | Max Expiry |
|---|---|---|---|
| Account SAS | Multiple services, account ops | Account key | Up to key validity |
| Service SAS | One resource, one service | Account key | Up to key validity |
| User Delegation SAS | Blob (& ADLS Gen2) only | Entra ID user delegation key | 7 days |

**Stored access policy:** server-side, revocable rule set applied to a service SAS on containers/shares/queues/tables — NOT usable with Account SAS.

## Access Keys
- 2 keys per account (Key1, Key2), 512-bit.
- Rotate: move apps to unused key → regenerate the other. Zero downtime.

## Microsoft Entra Authorization (Blob/Queue)
- Roles: Storage Blob Data Owner / Contributor / Reader / Delegator.
- Storage Queue Data Contributor / Reader / Message Processor / Message Sender.
- Preferred over access keys for least-privilege, auditable access — required for user delegation SAS generation.

## Performance Tiers
- **Standard:** HDD-backed, general purpose v2 accounts, supports all tiers.
- **Premium:** SSD-backed; separate account kinds — Premium Block Blob, Premium Page Blob (managed disks), Premium File Storage. Chosen at account creation, cannot change after.

## Common Exam Traps
- Confusing GRS (not readable) with RA-GRS (readable secondary).
- Forgetting early deletion fees when moving blobs out of Cool/Cold/Archive before minimum retention.
- Assuming Archive blobs are instantly accessible after tier change — rehydration is mandatory.
- Using Account SAS when a scenario specifically calls for Entra ID identity control (should be User Delegation SAS).
- Forgetting stored access policies cannot apply to Account SAS.
