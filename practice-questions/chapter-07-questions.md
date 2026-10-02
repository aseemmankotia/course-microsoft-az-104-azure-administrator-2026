## Chapter 7: ARM Templates, Bicep, and Scale Sets with Autoscale — Practice Questions

**Q1.** You deploy an ARM template using Complete mode to a resource group that already contains a storage account not defined in the template, plus a VM that IS defined in the template. What happens after deployment?

A) Both the storage account and VM remain unchanged
B) The deployment fails because the storage account is not in the template
C) The storage account is moved to a new resource group automatically
D) The storage account is deleted; the VM is updated per the template

<details>
<summary>Answer</summary>

**Correct: D**

Complete mode deletes any resource in the target resource group that is not defined in the template, regardless of how it was originally created.

**Why the others are wrong:**
- Incorrect — Complete mode explicitly removes resources not present in the template; this only happens in Incremental mode.
- Incorrect — the deployment does not fail; unlisted resources are deleted, not flagged as errors.
- Incorrect — ARM deployment modes never move resources between resource groups.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company wants to preview exactly what an ARM/Bicep deployment will change before running it, without applying any changes. Which command should they run?

A) az deployment group create --confirm-with-what-if
B) az deployment group validate
C) az deployment group what-if
D) az group deployment export

<details>
<summary>Answer</summary>

**Correct: C**

az deployment group what-if produces a report of Create/Modify/Delete/NoChange/Ignore changes without deploying anything.

**Why the others are wrong:**
- This flag does not exist as written for previewing changes without deploying.
- validate only checks template syntax/schema correctness, not the actual resource-level change set.
- This command exports an existing deployment's template; it does not preview changes.

</details>

---

**Q3.** A VM Scale Set running a Bicep-deployed workload needs to scale out when average CPU exceeds 75% and scale in when it drops below 25%, with no more than one scaling action every 5 minutes. Which Azure feature should be configured?

A) Azure Advisor recommendations
B) Azure Policy with a deny effect
C) Azure Monitor autoscale settings with CPU-based rules and default cooldown
D) Manual scaling via Azure CLI cron job

<details>
<summary>Answer</summary>

**Correct: C**

Azure Monitor autoscale settings support metric-based scale-out/scale-in rules with a configurable cooldown period (default 5 minutes) between scaling actions.

**Why the others are wrong:**
- Advisor gives recommendations only; it does not perform automated scaling.
- Azure Policy enforces compliance rules; it has no scaling capability.
- A manual CLI cron job is not a supported or exam-relevant native scaling mechanism.

</details>

---

**Q4.** Which orchestration mode and image combination allows a single Virtual Machine Scale Set to reach the maximum of 1,000 VM instances?

A) Uniform orchestration with a custom image
B) Uniform orchestration with a Marketplace image and managed disks
C) Availability Set with unmanaged disks
D) Uniform orchestration with unmanaged disks

<details>
<summary>Answer</summary>

**Correct: B**

Uniform orchestration scale sets can reach 1,000 instances only when using a Marketplace (platform) image with managed disks; custom images cap out at 600 instances.

**Why the others are wrong:**
- Custom images limit Uniform scale sets to 600 instances, not 1,000.
- Availability Sets are a separate feature entirely and are not VM Scale Sets.
- Unmanaged disks are not supported for scale sets at the 1,000-instance limit and are generally discouraged.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A Bicep file needs to reference a separately maintained template that provisions a virtual network, and pass the VNet name as a parameter. Which construct should be used?

A) A nested 'variables' block referencing the VNet template
B) An ARM 'linkedTemplates' array inside 'resources'
C) A 'reference()' function call to the VNet template
D) The 'module' keyword pointing to the VNet .bicep file

<details>
<summary>Answer</summary>

**Correct: D**

Bicep's 'module' keyword is used to compose reusable templates, passing parameters and reading outputs from the referenced .bicep file.

**Why the others are wrong:**
- Variables blocks hold values, not template references.
- linkedTemplates is ARM JSON syntax for nested/linked deployments, not native Bicep syntax.
- reference() retrieves runtime properties of a deployed resource; it does not link separate template files.

</details>

---

**Q6.** An administrator sets an autoscale scale-in policy of 'OldestVM' on a scale set. What does this configuration control?

A) Which VM instance is patched first during OS updates
B) Which VM instance receives the highest storage tier
C) Which VM instance is removed first when the scale set scales in
D) Which VM instance is placed in the update domain first

<details>
<summary>Answer</summary>

**Correct: C**

The scale-in policy (Default, NewestVM, OldestVM) determines the order in which instances are terminated when the scale set removes VMs during a scale-in event.

**Why the others are wrong:**
- Patch ordering is controlled by maintenance/update configurations, not the scale-in policy.
- Storage tier assignment is unrelated to scale-in policy.
- Update domain placement is handled by the platform's fault domain algorithm, not the scale-in policy.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** You deploy the same ARM template twice to the same resource group using Incremental mode, changing only one property value between deployments. What happens to resources present in the resource group but absent from the template?

A) They are deleted on the second deployment
B) They are converted to read-only
C) They trigger a validation error
D) They are left untouched

<details>
<summary>Answer</summary>

**Correct: D**

Incremental mode (the default) only adds or updates resources defined in the template and leaves all other existing resources in the resource group unaffected.

**Why the others are wrong:**
- Deletion of unlisted resources only happens in Complete mode.
- ARM deployments never mark resources as read-only.
- There is no validation error for unrelated resources existing in the resource group.

</details>

---

**Q8.** What is the primary structural difference between a Bicep file and an equivalent ARM JSON template?

A) Bicep uses a declarative simplified syntax that transpiles to ARM JSON, removing the need for functions like parameters() and variables()
B) Bicep requires an explicit contentVersion and $schema property while ARM JSON does not
C) Bicep only supports deploying storage accounts and VMs
D) Bicep templates cannot include outputs

<details>
<summary>Answer</summary>

**Correct: A**

Bicep is a domain-specific language that compiles down to standard ARM JSON, but its syntax lets you reference parameters and variables directly by name instead of wrapping them in functions.

**Why the others are wrong:**
- It's the reverse — ARM JSON requires $schema and contentVersion; Bicep abstracts these away.
- Bicep supports the same full range of Azure resource types as ARM JSON, not a limited subset.
- Bicep fully supports an 'output' block just like ARM JSON.

</details>

---

