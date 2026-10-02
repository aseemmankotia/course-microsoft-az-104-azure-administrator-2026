## Chapter 3: Governance: Management Groups, Azure Policy, Locks, and Cost Controls — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Maximum management group hierarchy depth (excluding root management group and subscription level)? | 6 levels. Exam tip: root management group itself and the subscription level below the hierarchy don't count toward this limit. |
| 2 | Maximum number of management groups supported per Azure AD directory? | 10,000. Each management group and subscription supports only ONE parent — no multi-parent hierarchies. |
| 3 | Limit on custom Azure Policy definitions per management group or subscription? | 500 custom policy definitions. Exam tip: built-in policy definitions do not count against this limit. |
| 4 | Limit on Azure Policy initiative (policy set) definitions per management group or subscription? | 200 initiative definitions. Policy assignments are also capped at 200 per scope. |
| 5 | Tag limits: max tags per resource, max tag name length, max tag value length? | 50 tags per resource/resource group/subscription. Tag name max 512 characters (256 for VMs/VMSS). Tag value max 256 characters. |
| 6 | CanNotDelete lock vs ReadOnly lock — what's the difference? | CanNotDelete: authorized users can still read and modify, but cannot delete. ReadOnly: users can read but cannot modify OR delete — this can break apps that need to write (e.g., key rotation, VM extensions). |
| 7 | Azure Policy: Deny effect vs Audit effect? | Deny: blocks the non-compliant resource request at deployment time. Audit: allows the deployment but flags it as non-compliant in compliance reports — no blocking. |
| 8 | Azure Policy: Append effect vs Modify effect? | Append: adds fields/values to a resource request only during creation/update, cannot remediate existing resources. Modify: can add/update/remove properties or tags on existing resources too, and supports remediation tasks. |
| 9 | CLI command to assign an Azure Policy definition to a scope? | az policy assignment create --name <name> --policy <policyDefinitionId> --scope <scopeId> |
| 10 | CLI command to apply a CanNotDelete lock on a resource group? | az lock create --name myLock --resource-group myRG --lock-type CanNotDelete |
| 11 | What are the two categories used when creating an Azure Policy exemption? | Waiver (resource is intentionally exempt for business reasons) and Mitigated (non-compliance risk has been addressed through another control). |
| 12 | What is the order in which Azure Policy effects are evaluated when multiple could apply? | Disabled → Append/Modify → Deny → Audit → AuditIfNotExists/DeployIfNotExists. Exam tip: Append/Modify run BEFORE Deny is evaluated, so a policy can fix a property before Deny checks it. |
