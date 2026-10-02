## Chapter 2: Azure RBAC: Roles, Scopes, and Assignments — Practice Questions

**Q1.** Your organization structure is: Management Group 'Corp' → Subscription 'Prod' → Resource Group 'WebApps' → VM 'WebVM1'. An admin assigns the Reader role to UserA at the 'Corp' management group. A different admin assigns the Contributor role to UserA at the 'WebApps' resource group. What is UserA's effective permission on 'WebVM1'?

A) Reader only, because the higher scope assignment always overrides lower scopes
B) Access is denied because the two assignments conflict
C) UserA must select which role to use each time they sign in
D) Contributor, because RBAC role assignments are additive across scopes and Contributor is a superset of Reader

<details>
<summary>Answer</summary>

**Correct: D**

Azure RBAC is purely additive down the scope hierarchy. A user's effective permissions at any resource are the union of all role assignments at that resource and every ancestor scope. Since Contributor includes every action Reader includes, the effective permission on WebVM1 is Contributor.

**Why the others are wrong:**
- RBAC never lets a lower scope 'lose' a higher scope's grant, but it also never restricts a broader role granted lower down — there's no override, only union.
- RBAC assignments never conflict with each other; there is no concept of denial from overlapping role assignments (only explicit deny assignments can block).
- There is no role-selection step for users — effective permissions are computed automatically and silently.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team lead must be able to grant and revoke Azure resource access for team members within a resource group, but must NOT be able to create, modify, or delete any actual resources (VMs, storage, etc.) in that resource group. Which built-in role should be assigned?

A) Owner
B) Contributor
C) Reader
D) User Access Administrator

<details>
<summary>Answer</summary>

**Correct: D**

User Access Administrator grants Microsoft.Authorization/roleAssignments/* actions (manage access) but has no permissions over the resources themselves — exactly matching 'grant access but not touch resources.'

**Why the others are wrong:**
- Owner has full Contributor-level resource permissions PLUS access management — too much access, violates the 'not modify resources' requirement.
- Contributor can fully manage resources but explicitly cannot assign roles or manage access — the opposite of what's needed.
- Reader can only view resources; it has no permission to manage role assignments.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An administrator wants to guarantee that a critical storage account can never be deleted by ANY user — including users who hold the Owner role — without changing any existing role assignments. What should the administrator do?

A) Manually create a deny assignment on the storage account
B) Remove the Owner role from every user in the subscription
C) Apply a CanNotDelete resource lock on the storage account
D) Create a custom role that excludes the delete action and reassign it in place of Owner

<details>
<summary>Answer</summary>

**Correct: C**

Resource locks (CanNotDelete or ReadOnly) apply independently of RBAC role assignments and block the operation for everyone, including Owners, without touching any identity's role assignments.

**Why the others are wrong:**
- Deny assignments cannot be manually created through the portal/CLI by regular administrators — they are system-generated (e.g., via Azure Blueprints or managed apps).
- Removing Owner from everyone breaks other required administrative functions and doesn't scale — it's not the intended control.
- Reassigning roles changes existing role assignments, which the requirement explicitly says to avoid, and still wouldn't block a future Owner reassignment.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** You need to ensure every new storage account created in a subscription automatically has 'Secure transfer required' enabled, regardless of which role the creator holds. Which Azure feature should you use?

A) A custom Azure RBAC role restricted to storage account creation
B) Microsoft Entra Conditional Access
C) Azure Policy with a deny or deploy-if-not-exists effect
D) A resource lock on the subscription

<details>
<summary>Answer</summary>

**Correct: C**

Azure Policy enforces configuration/compliance standards on resources regardless of who creates them. RBAC controls WHO can act; Policy controls WHAT the resource must look like.

**Why the others are wrong:**
- RBAC only controls whether an action is permitted, not the configuration values used when performing that action.
- Conditional Access controls sign-in conditions for identities, not resource configuration.
- Resource locks only prevent delete/modify operations; they don't enforce configuration settings.

</details>

---

**Q5.** A consultant needs read-only access to view the list of users in Microsoft Entra ID but must have zero access to any Azure resources such as VMs or storage accounts. Which role should be assigned, and in which system?

A) Assign the Reader Azure RBAC role at the tenant root management group
B) Assign the Directory Readers Microsoft Entra role
C) Assign Contributor scoped to the Azure Active Directory resource provider
D) Create a custom Azure RBAC role with Microsoft.AAD/*/read actions

<details>
<summary>Answer</summary>

**Correct: B**

Directory objects (users, groups, apps) are governed by Microsoft Entra ID roles, not Azure RBAC. Directory Readers grants read-only visibility into directory data with no Azure resource access.

**Why the others are wrong:**
- Azure RBAC Reader — even at the tenant root management group — only controls Azure resource access; it has no visibility into Entra ID directory objects.
- Azure AD/Entra ID is not an ARM resource provider that Contributor can be scoped against for directory object management.
- Custom Azure RBAC roles cannot grant permissions over Microsoft Entra directory objects — that control plane is entirely separate from ARM/RBAC.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** You are writing a custom role JSON that grants 'Microsoft.Compute/*' in Actions, but you must explicitly prevent the role from deleting any virtual machine. Which JSON property should you use?

A) NotDataActions
B) AssignableScopes
C) DataActions
D) NotActions

<details>
<summary>Answer</summary>

**Correct: D**

NotActions subtracts specific management-plane actions (like Microsoft.Compute/virtualMachines/delete) from the Actions granted by that same role definition.

**Why the others are wrong:**
- NotDataActions subtracts from DataActions (data-plane operations like blob read/write), not management-plane operations like VM delete.
- AssignableScopes controls WHERE the custom role can be assigned, not which permissions it grants or removes.
- DataActions grants data-plane permissions; it's unrelated to restricting VM delete, which is a control-plane action.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the maximum number of custom roles you can create in a single Microsoft Entra tenant (across Azure RBAC)?

A) 500
B) 2000
C) Unlimited
D) 5000

<details>
<summary>Answer</summary>

**Correct: D**

Azure enforces a hard limit of 5000 custom roles per Microsoft Entra tenant, shared across all subscriptions in that tenant.

**Why the others are wrong:**
- 500 is not the documented Azure limit for custom roles.
- 2000 is a plausible-sounding number but is not correct — that figure is often confused with older role assignment limits.
- There is no unlimited tier for custom roles; the tenant-wide cap is fixed.

</details>

---

**Q8.** Which statement BEST describes the difference between a role definition and a role assignment in Azure RBAC?

A) A role definition specifies WHO gets access; a role assignment specifies WHAT actions are allowed
B) A role definition specifies WHAT actions are allowed (a permission set); a role assignment binds a security principal, a role definition, and a scope together
C) Role definitions apply only to custom roles, while role assignments apply only to built-in roles
D) Role definitions apply at subscription scope only, while role assignments apply at resource scope only

<details>
<summary>Answer</summary>

**Correct: B**

A role definition is a reusable collection of permissions (Actions/NotActions/DataActions). A role assignment is the actual grant that ties a specific identity, a specific role definition, and a specific scope together.

**Why the others are wrong:**
- This reverses the concepts — the role definition describes permissions, not identities.
- Both built-in and custom roles are role definitions, and both can be used in role assignments.
- Role definitions and role assignments can both exist at any of the four scope levels (management group, subscription, resource group, resource).

</details>

---

