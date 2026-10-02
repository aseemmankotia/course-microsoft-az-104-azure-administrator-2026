# Chapter 1 Cheat Sheet: Entra ID Users, Groups, Administrative Units

## Tenant vs Subscription
| Concept | Fact |
|---|---|
| Tenant | Container for identities (users, groups, apps) |
| Subscription | Billing/resource container; trusts **exactly 1 tenant** at a time |
| Change trust | Subscription can be moved to trust a different tenant, but never 2 at once |

## Member vs Guest (B2B) Users
| Attribute | Member | Guest |
|---|---|---|
| UserType | Member | Guest |
| Credentials | Managed by your tenant | Own home tenant/social ID |
| Use case | Employees | External partners/vendors |

## Security Group vs Microsoft 365 Group
| Feature | Security Group | Microsoft 365 Group |
|---|---|---|
| Devices as members | ✅ | ❌ |
| Azure RBAC assignment | ✅ | ✅ (users only) |
| Shared mailbox/calendar/files | ❌ | ✅ |
| Dynamic membership support | ✅ | ✅ |

## Membership Types
| Type | Behavior | License |
|---|---|---|
| Assigned | Manual add/remove | Free tier OK |
| Dynamic User/Device | Rule-based auto membership | **Requires Entra ID P1/P2** |

### Dynamic Rule Syntax
```
(user.department -eq "Sales") -and (user.usageLocation -eq "US")
```
Operators: `-eq -ne -and -or -contains -notContains -match`

## Administrative Units (AU)
- Scope: **Users, Groups, Devices only** (never resource groups/subscriptions)
- Purpose: Delegate directory roles (User Admin, Helpdesk Admin) to a limited scope
- Assign role **scoped to AU** — not tenant-wide
- Users/groups can belong to multiple AUs

## Device Join/Registration States
| State | On-prem AD | Entra ID | Typical Use |
|---|---|---|---|
| Microsoft Entra joined | ❌ | ✅ | Cloud-only corporate device |
| Microsoft Entra hybrid joined | ✅ | ✅ | Corporate device, GPO + SSO |
| Microsoft Entra registered | ❌ (personal) | ✅ (partial) | BYOD/personal device |

## Self-Service Password Reset (SSPR)
| Setting | Default |
|---|---|
| Methods required to REGISTER | 1 |
| Methods required to RESET | 2 |
| Scope options | None / Selected group / All |

## Quick Exam Triggers
- "Automatically add/remove members based on attribute" → **Dynamic group + P1 license**
- "Delegate admin rights to a subset of users only" → **Administrative Unit**
- "Domain-joined + SSO to cloud" → **Hybrid joined**
- "BYOD, personal phone" → **Registered**
- "External vendor, own credentials" → **B2B Guest**
- "Devices need to be group members" → **Security group** (never M365 group)
