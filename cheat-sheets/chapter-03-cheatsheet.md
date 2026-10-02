## Chapter 3 Cheat Sheet — Governance

### Management Groups
| Fact | Value |
|---|---|
| Max hierarchy depth (excl. root & subscription) | 6 levels |
| Max management groups per directory | 10,000 |
| Parents per management group/subscription | 1 (single parent only) |
| Root management group | Cannot be deleted or moved |

### Azure Policy Effects
| Effect | Behavior |
|---|---|
| Deny | Blocks non-compliant request at deployment |
| Audit | Allows deployment, flags non-compliance in reports |
| Append | Adds fields to request at create/update only, no remediation |
| Modify | Adds/updates/removes properties or tags, supports remediation tasks |
| DeployIfNotExists | Deploys a related resource if missing (e.g., auto-install Log Analytics agent) |
| AuditIfNotExists | Audits if a related resource is missing |
| Disabled | Turns off evaluation without removing assignment |

**Evaluation order:** Disabled → Append/Modify → Deny → Audit → AuditIfNotExists/DeployIfNotExists

### Policy Limits
| Item | Limit (per mgmt group/subscription) |
|---|---|
| Custom policy definitions | 500 |
| Initiative definitions | 200 |
| Policy/initiative assignments | 200 |

### Resource Locks
| Lock Type | Delete | Modify |
|---|---|---|
| CanNotDelete | ❌ Blocked | ✅ Allowed |
| ReadOnly | ❌ Blocked | ❌ Blocked (incl. POST actions like key rotation) |

- Locks inherit downward: subscription → resource group → resource.
- ReadOnly on a resource group can break apps needing runtime writes (e.g., storage key rotation, VM disk operations).
- Only Owner or User Access Administrator (or Contributor with Microsoft.Authorization/locks/* permission) can manage locks.

### Policy Exemptions
| Category | Use Case |
|---|---|
| Waiver | Business decision to accept non-compliance |
| Mitigated | Risk addressed through compensating control |

### Remediation Tasks
- Required for **Modify** and **DeployIfNotExists** effects to fix *existing* non-compliant resources.
- New/updated resources are auto-evaluated at deployment; existing resources need a manually or automatically triggered remediation task.
- CLI: `az policy remediation create --name <name> --policy-assignment <assignmentId>`

### Tags via Policy
- Use **Append** to add a tag only at creation.
- Use **Modify** to enforce/correct tags on existing resources (requires remediation).
- Max 50 tags/resource; tag name ≤512 chars (256 for VM/VMSS); tag value ≤256 chars.

### Cost Management — Budgets
- Budgets can be scoped to subscription, resource group, or management group.
- Alerts can trigger on **Actual** or **Forecasted** cost thresholds (e.g., 80%, 100%, 120%).
- Action groups can be attached to budget alerts to automate notifications/responses.

### Key CLI Commands
```bash
az policy definition create --name <n> --rules <rules.json> --params <params.json>
az policy assignment create --name <n> --policy <policyId> --scope <scopeId>
az policy exemption create --name <n> --policy-assignment <assignmentId> --exemption-category Waiver
az lock create --name <n> --resource-group <rg> --lock-type CanNotDelete
az policy remediation create --name <n> --policy-assignment <assignmentId>
```
