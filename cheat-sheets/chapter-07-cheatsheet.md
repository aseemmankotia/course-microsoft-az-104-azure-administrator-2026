## ARM Templates, Bicep & VMSS Autoscale — Cheat Sheet

### ARM Template Structure
| Section | Required? | Purpose |
|---|---|---|
| $schema | Yes | Defines JSON schema version |
| contentVersion | Yes | Template versioning (e.g. 1.0.0.0) |
| parameters | No | Input values at deploy time |
| variables | No | Computed/reused values |
| resources | Yes | Resources to deploy |
| outputs | No | Values returned after deployment |

Bicep drops $schema/contentVersion — the compiler handles them. Reference params/vars directly by name; no parameters()/variables() functions needed.

### Deployment Modes
| Mode | Default? | Effect on unlisted resources in RG |
|---|---|---|
| Incremental | Yes | Left untouched |
| Complete | No | **Deleted** |

Complete is scoped to the target resource group only — resources in other RGs are never affected. Always run what-if before using Complete mode.

### What-If Validation
```bash
az deployment group what-if \
  --resource-group myRG \
  --template-file main.bicep \
  --parameters env=prod
```
Output change types: Create, Modify, Delete, NoChange, Ignore.

### Bicep Essentials
```bicep
param location string = resourceGroup().location
var vmName = 'vm-${uniqueString(resourceGroup().id)}'

module network 'modules/vnet.bicep' = {
  name: 'vnetDeploy'
  params: { location: location }
}

resource vm 'Microsoft.Compute/virtualMachines@2023-09-01' = {
  name: vmName
  location: location
  properties: { }
}

output vmId string = vm.id
```
Commands:
- Build: `az bicep build --file main.bicep`
- Decompile: `az bicep decompile --file azuredeploy.json`
- Deploy: `az deployment group create --template-file main.bicep`

### VM Scale Sets — Instance Limits
| Orchestration | Image type | Max instances |
|---|---|---|
| Uniform | Marketplace + managed disk | 1,000 |
| Uniform | Custom image | 600 |
| Flexible | Marketplace/custom | 1,000 |

### Autoscale Rules
| Setting | Notes |
|---|---|
| Metric source | CPU %, memory %, disk queue length, custom metrics |
| Statistic | Average, Min, Max, Sum over time window |
| Cooldown | Default 5 min between scale actions (per direction) |
| Scale-in policy | Default / NewestVM / OldestVM — decides which VM is removed first |

### Exam Gotchas
1. **Complete mode** deletes resources not in the template — a top exam trap; always confirm scope is the resource group.
2. **Custom image caps VMSS at 600 instances**, not 1,000 — commonly missed number.
3. **Bicep modules** replace ARM's `linkedTemplates`/`nestedTemplates` pattern for reuse.
4. Autoscale **cooldown** prevents flapping; exam may ask why scale-in didn't happen immediately after a scale-out.
5. `what-if` never applies changes — use it before every production deployment to catch unintended deletions in Complete mode.
