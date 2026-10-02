## Chapter 7: ARM Templates, Bicep, and Scale Sets with Autoscale — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | ARM deployment mode that deletes resources in the resource group not present in the template? | Complete mode. Incremental (default) leaves unlisted resources untouched. Exam tip: Complete is scoped to the resource group only. |
| 2 | Command to preview an ARM/Bicep deployment's changes without applying them? | az deployment group what-if. Reports Create, Modify, Delete, NoChange, Ignore per resource. |
| 3 | Max VMSS instances with Uniform orchestration + Marketplace image + managed disks? | 1,000 instances. Drops to 600 if using a custom image. |
| 4 | Default cooldown period between autoscale scaling actions? | 5 minutes. Prevents rapid oscillating scale in/out (flapping). |
| 5 | Bicep keyword used to reference another template file for reuse? | module — e.g. module vnet 'vnet.bicep' = { name: 'vnetDeploy', params: {...} } |
| 6 | Bicep vs ARM JSON: how do you access a parameter value? | Bicep: reference it directly by name (e.g. location). ARM JSON: wrap in a function, e.g. parameters('location'). |
| 7 | Scale-in policy options for a VM Scale Set? | Default, NewestVM, OldestVM. Controls which instance is removed first when scaling in. |
| 8 | ARM template top-level sections (in order)? | $schema, contentVersion, parameters, variables, resources, outputs (functions optional). |
| 9 | Incremental vs Complete deployment mode — exam scenario trap? | Complete mode silently deletes any resource in the resource group not defined in the template — including ones created manually via Portal. |
| 10 | Command to convert an existing ARM JSON template to Bicep? | az bicep decompile --file azuredeploy.json |
| 11 | What metric types can trigger VMSS autoscale rules? | Host-level metrics like CPU %, plus guest/custom metrics (e.g. memory %, queue length) via diagnostics extension or Application Insights. |
| 12 | Does enabling autoscale on a VMSS have an extra service charge? | No — Azure Monitor autoscale itself is free; you only pay for the VM instances that get provisioned during scale-out events. |
