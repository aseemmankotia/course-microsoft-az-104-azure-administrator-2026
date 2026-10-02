## Chapter 5 Cheat Sheet — Blob, Files & Data Movement

### Container Access Levels
| Level | Anonymous blob read | Anonymous listing |
|---|---|---|
| Private | No | No |
| Blob | Yes (direct URL) | No |
| Container | Yes | Yes |

### Lifecycle Management: Conditions → Actions
| Condition | Based on |
|---|---|
| daysAfterModificationGreaterThan | Last write |
| daysAfterLastAccessTimeGreaterThan | Last read (requires access tracking enabled) |
| daysAfterCreationGreaterThan | Blob creation date |
| daysAfterLastTierChangeGreaterThan | Only valid for tierToCold FROM Archive |

Actions: `tierToCool`, `tierToCold`, `tierToArchive`, `delete` (also apply to blob versions/snapshots).

### Access Tier Minimum Durations & Rehydration
| Tier | Min. duration | Notes |
|---|---|---|
| Hot | none | Frequent access |
| Cool | 30 days | Infrequent access |
| Cold | 90 days | Rarely accessed |
| Archive | 180 days | Offline; rehydrate Standard (≤15h) or High priority (<1h, <10GB) |

### Object Replication — 4 Prerequisites
1. Blob **versioning** on source AND destination
2. **Change feed** enabled on source
3. **Block blobs only** (no page/append)
4. GPv2 or premium block blob accounts; source ≠ destination

### Immutability Policies
| Type | End condition | Modification after lock |
|---|---|---|
| Time-based retention | Fixed date | Extend only, max 5 times, never decrease |
| Legal hold | Manual removal | No fixed end date |

### Azure Files: SMB vs NFS 4.1
| Feature | SMB | NFS 4.1 |
|---|---|---|
| Account tier | Standard or Premium | Premium (FileStorage) only |
| Network | Public or private | Private endpoint/VNet only |
| Permissions | Windows ACL | POSIX |
| AD auth | Yes | No |

### Azure File Sync Topology
Storage Sync Service → Sync Group → **1 Cloud Endpoint** (Azure file share) + **N Server Endpoints** (paths on registered servers). Cloud tiering: hot files cached locally, cold files become pointers.

### Storage Account Network Security
- **Firewall + Service Endpoint**: subnet-restricted, storage keeps public IP
- **Private Endpoint**: storage account gets private IP in your VNet
- Adding any network rule sets default action to **Deny**
- Trusted Microsoft services can bypass firewall (must enable explicitly)

### AzCopy Essentials
```bash
# One-way upload
azcopy copy "<source>" "<dest>" --recursive=true

# True mirror (deletes extras at destination)
azcopy sync "<source>" "<dest>" --delete-destination=true
```
Use **AzCopy** for bulk/high-throughput transfers; use **Storage Explorer** for manual/GUI browsing.

### Key Numbers
- Max block blob size: ~190.7 TiB | Max blocks: 50,000 | Max block size: 4000 MiB
- Standard file share: 5 TiB (100 TiB with large file shares) | Premium file share: 100 TiB
