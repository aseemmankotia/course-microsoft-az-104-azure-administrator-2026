## Chapter 3: Governance: Management Groups, Azure Policy, Locks, and Cost Controls — Practice Questions

**Q1.** A company has a production resource group that must never be accidentally deleted, but engineers still need to modify VM sizes and add resources inside it daily. Which lock configuration meets this requirement?

A) Apply a CanNotDelete lock on the resource group
B) Apply a ReadOnly lock on the resource group
C) Apply a ReadOnly lock on each individual resource
D) Apply an Azure Policy with Deny effect on delete operations

<details>
<summary>Answer</summary>

**Correct: A**

CanNotDelete allows authorized users to read and modify a resource but blocks deletion, which is exactly the requirement.

**Why the others are wrong:**
- ReadOnly would also block the daily VM size modifications, breaking normal operations.
- Locking each resource individually doesn't cover future resources added to the group and is operationally heavier than a single group-level lock.
- Azure Policy Deny effect blocks non-compliant resource creation/updates, it isn't designed to block delete operations on existing resources.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An administrator places a ReadOnly lock on a resource group containing a storage account. Afterward, an application using that storage account starts failing with authorization errors when rotating access keys programmatically. What is the cause?

A) ReadOnly locks only affect ARM template deployments, not runtime operations
B) The storage account needs its own separate ReadOnly lock to be affected
C) ReadOnly locks block any POST action, including operations like key rotation that require a write on the resource
D) ReadOnly locks expire after 24 hours and must be reapplied

<details>
<summary>Answer</summary>

**Correct: C**

ReadOnly locks block all write and delete operations, including POST actions like regenerating storage keys, even though the account's data plane isn't technically 'modified' as a resource property change.

**Why the others are wrong:**
- ReadOnly locks affect the management plane broadly, not just ARM template deployments — they block API write/action calls at runtime too.
- Locks are inherited from the resource group down to all child resources automatically; a separate lock isn't needed.
- Azure resource locks do not expire automatically; they persist until manually removed.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company wants every new resource deployed in the subscription to automatically receive a 'CostCenter' tag copied from its parent resource group if the tag is missing, without blocking the deployment. Which Azure Policy effect should be used?

A) Modify
B) Deny
C) Audit
D) Append

<details>
<summary>Answer</summary>

**Correct: A**

Modify can add, update, or remove tags on resources during creation, update, and via remediation tasks on already-existing resources — it's the only effect that supports full lifecycle tag management including remediation.

**Why the others are wrong:**
- Deny would block deployment entirely if the tag is missing, which fails the 'without blocking' requirement.
- Audit only flags non-compliance in reports; it does not add the tag.
- Append can add the tag field only at creation/update time but cannot remediate existing non-compliant resources; Modify is required for that broader scope.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company has 40 subscriptions across 5 departments and needs to apply a single set of governance policies and RBAC assignments consistently to all subscriptions in each department, without assigning policies to each subscription individually. Which Azure feature should be used?

A) Azure Blueprints only
B) Management groups
C) Resource tags with policy-based filtering
D) Azure Policy initiatives assigned per subscription

<details>
<summary>Answer</summary>

**Correct: B**

Management groups let you group subscriptions hierarchically and apply policy/RBAC assignments once at the management group level, inheriting down to all child subscriptions.

**Why the others are wrong:**
- Azure Blueprints (retiring) packages artifacts but doesn't solve the hierarchical scoping problem by itself.
- Tags don't enforce or scope RBAC/policy assignment; they're metadata used inside policy conditions, not a governance boundary.
- Assigning per subscription individually is exactly the repetitive manual work the company wants to avoid.

</details>

---

**Q5.** Which Azure resource is the correct choice to group multiple related Azure Policy definitions (e.g., all CIS benchmark controls) so they can be assigned as a single unit to a scope?

A) Policy exemption
B) Management group
C) Resource lock
D) Policy initiative (policy set definition)

<details>
<summary>Answer</summary>

**Correct: D**

An initiative (policySetDefinition) bundles multiple policy definitions so they can be assigned together at a scope, commonly used for compliance standards like CIS or NIST.

**Why the others are wrong:**
- A policy exemption excludes a resource from evaluation, it doesn't group policies.
- Management groups are organizational scopes for subscriptions, not containers for policy definitions.
- Resource locks prevent delete/modify actions and are unrelated to grouping policies.

</details>

---

**Q6.** How many levels of management groups does Azure support in the hierarchy, not counting the root management group and the subscription level?

A) 6 levels
B) 3 levels
C) 10 levels
D) Unlimited levels

<details>
<summary>Answer</summary>

**Correct: A**

Azure supports a maximum depth of 6 levels of management groups beneath the root, excluding the root level itself and the subscription level.

**Why the others are wrong:**
- 3 levels understates the documented supported depth.
- 10 levels exceeds Azure's documented limit.
- The hierarchy is not unlimited; Azure enforces a fixed maximum depth.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A resource is legitimately non-compliant with a subscription-wide Azure Policy assignment due to a temporary business exception, but the team does not want to modify the policy assignment itself or wait for it to be fixed. Which feature should be used, and under which category?

A) Delete the policy assignment for that resource group
B) Apply a ReadOnly lock to hide the resource from evaluation
C) Set the policy effect to Disabled for the whole subscription
D) Create a policy exemption with category 'Waiver'

<details>
<summary>Answer</summary>

**Correct: D**

Policy exemptions let you exclude a specific resource or scope from a policy assignment's evaluation. The 'Waiver' category is used when the resource is intentionally exempt for business reasons (as opposed to 'Mitigated' where the risk is addressed another way).

**Why the others are wrong:**
- Deleting the assignment removes governance for the entire resource group, not just the one resource, which is overly broad.
- Resource locks control delete/modify actions, not policy evaluation.
- Disabling the effect subscription-wide removes enforcement everywhere, not just for the exempted resource.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A subscription owner is confused about the difference between Azure Policy and Azure RBAC. Which statement correctly distinguishes the two?

A) Azure Policy controls user permissions to Azure resources; RBAC evaluates resource configuration compliance
B) RBAC controls what actions a user/service principal can perform; Azure Policy evaluates and enforces the properties/configuration of resources regardless of who created them
C) RBAC and Azure Policy are interchangeable and either can enforce tagging standards
D) Azure Policy only works on resource groups, while RBAC works only on individual resources

<details>
<summary>Answer</summary>

**Correct: B**

RBAC governs identity access (who can do what), while Azure Policy governs resource state and compliance (what configurations are allowed), independent of who deployed the resource.

**Why the others are wrong:**
- This reverses the actual roles of RBAC and Azure Policy.
- They serve different purposes and are not interchangeable — RBAC cannot enforce tag values on resource properties like Policy can.
- Both RBAC and Azure Policy can be scoped at management group, subscription, resource group, or resource level — neither is restricted the way this option describes.

</details>

---

