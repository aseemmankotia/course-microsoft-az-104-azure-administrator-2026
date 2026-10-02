## Chapter 2 Cheat Sheet — Azure RBAC

### Scope Hierarchy (inheritance flows DOWN only)
| Level | Example | Notes |
|---|---|---|
| Management Group | `Corp` | Top of hierarchy, groups subscriptions |
| Subscription | `Prod` | Billing + policy boundary |
| Resource Group | `WebApps` | Logical container |
| Resource | `WebVM1` | Most granular scope |

Rule: assignments are **additive** across scopes — effective permission = union of all assignments up the chain. There is no override, only accumulation.

### Built-in Role Comparison
| Role | Manage Resources | Assign Roles | View Only |
|---|---|---|---|
| Owner | ✅ Full | ✅ Yes | — |
| Contributor | ✅ Full | ❌ No | — |
| Reader | ❌ No | ❌ No | ✅ Yes |
| User Access Administrator | ❌ No | ✅ Yes | — |

Exam trap: Contributor CANNOT grant access to others — students often assume it can because it's 'almost Owner'.

### Custom Role JSON Skeleton
```json
{
  "Name": "VM Operator",
  "IsCustom": true,
  "Description": "Start/restart VMs, no delete",
  "Actions": ["Microsoft.Compute/virtualMachines/start/action",
              "Microsoft.Compute/virtualMachines/restart/action"],
  "NotActions": [],
  "DataActions": [],
  "NotDataActions": [],
  "AssignableScopes": ["/subscriptions/<sub-id>"]
}
```
- `Actions` — management-plane permissions granted
- `NotActions` — subtracts from THIS role's own Actions only (not a global deny)
- `DataActions` / `NotDataActions` — data-plane (e.g., blob read/write)
- `AssignableScopes` — required; where the role can be assigned (cannot be root `/`)

### Key Commands
| Task | Command |
|---|---|
| Create custom role | `az role definition create --role-definition role.json` |
| Update custom role | `az role definition update --role-definition role.json` |
| Assign role | `az role assignment create --assignee <id> --role "Contributor" --scope <scope>` |
| List assignments | `az role assignment list --scope <scope>` |

### Numbers & Limits
| Item | Limit |
|---|---|
| Custom roles per tenant | 5000 |
| Role assignments per subscription | 4000 |

### RBAC vs Policy vs Entra ID Roles
| Control | Governs | Example |
|---|---|---|
| Azure RBAC | WHO can act on Azure resources | Reader, Contributor, Owner |
| Azure Policy | WHAT resource configs are compliant | Require HTTPS, enforce tags |
| Microsoft Entra roles | WHO can manage directory objects | Global Administrator, Directory Readers |

### Deny Assignments
- Explicitly BLOCK actions; always override role assignment grants.
- Cannot be manually created by regular admins — generated via Blueprints/managed apps.
- Use **resource locks** (CanNotDelete/ReadOnly) as the practical exam answer to 'block even Owners'.
