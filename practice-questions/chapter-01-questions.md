## Chapter 1: Microsoft Entra ID: Users, Groups, and Administrative Units — Practice Questions

**Q1.** A company's HR system tags every employee account with a department attribute. The IT team wants a group that automatically adds and removes members whenever an employee's department attribute changes, with no manual intervention. Which solution meets this requirement?

A) Create an assigned security group and update membership manually each time HR changes a department
B) Create a Microsoft 365 group and nest it inside a security group
C) Create an administrative unit scoped to the Marketing department
D) Create a dynamic membership security group with the rule (user.department -eq "Marketing")

<details>
<summary>Answer</summary>

**Correct: D**

Dynamic membership groups evaluate attribute-based rules automatically and add/remove members without admin action. Requires Microsoft Entra ID P1 (or P2) licensing.

**Why the others are wrong:**
- Assigned groups require manual add/remove — fails the 'no manual intervention' requirement
- Microsoft 365 groups can be dynamic too, but nesting inside a security group doesn't create automatic membership evaluation on its own — the rule is what matters, and this option never defines one
- Administrative units scope delegated administration permissions, they do not provide group-style automatic membership for access assignment

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A global company wants its Australia-based support team to reset passwords and manage licenses only for users located in the Australia office, without granting any rights over users in other regions or over the tenant itself. What should the administrator configure?

A) Create an Administrative Unit containing the Australia users and assign the User Administrator role scoped to that Administrative Unit
B) Assign the User Administrator role at the tenant (organization) level
C) Create a dynamic security group for Australia users and assign the support team as group Owners
D) Use Azure RBAC to assign the Contributor role on the Australia resource group

<details>
<summary>Answer</summary>

**Correct: A**

Administrative units let you scope directory role assignments (like User Administrator) to a defined subset of users, groups, or devices — exactly the delegated, limited-scope administration described.

**Why the others are wrong:**
- Tenant-level role assignment grants rights over ALL users in the organization, violating the scoping requirement
- Group Owner status lets someone manage group membership, not reset passwords or manage user objects tenant-wide
- Azure RBAC governs access to Azure resources (VMs, storage, etc.), not Microsoft Entra ID user/password administration

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company issues corporate laptops that must remain joined to the on-premises Active Directory domain (for Group Policy) while also getting single sign-on to Microsoft 365 and conditional access enforcement. Which device state should these laptops use?

A) Microsoft Entra joined
B) Microsoft Entra registered
C) Microsoft Entra hybrid joined
D) Workgroup joined

<details>
<summary>Answer</summary>

**Correct: C**

Hybrid Entra joined devices are joined to on-premises AD DS and registered with Microsoft Entra ID simultaneously, preserving GPO management while enabling SSO and Conditional Access.

**Why the others are wrong:**
- Microsoft Entra joined devices have no relationship with on-premises AD DS — GPO management would be lost
- Microsoft Entra registered is used for BYOD/personal devices, not corporately managed domain-joined laptops
- 'Workgroup joined' is not a Microsoft Entra device state — it's a distractor term

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** You need a group that can include devices as members, be granted RBAC roles on Azure resources, and be used to assign NTFS permissions on a file server. Which group type should you create?

A) Microsoft 365 group
B) Distribution list
C) Security group
D) Mail-enabled security group

<details>
<summary>Answer</summary>

**Correct: C**

Security groups support user, device, service principal, and group members, and are the only group type usable for both Azure RBAC role assignment and on-prem file/folder permissions.

**Why the others are wrong:**
- Microsoft 365 groups support only user members (no devices) and are aimed at collaboration, not resource permissions
- Distribution lists are email-only and cannot be used for access control or RBAC
- Mail-enabled security groups cannot contain devices and are primarily for email distribution with limited access-control support

</details>

---

**Q5.** An external vendor needs temporary access to a specific Teams channel and SharePoint site using their own company credentials, without your organization managing their password.

A) Create a new member user account in your tenant
B) Create a local Windows account on the SharePoint server
C) Invite the vendor as a Microsoft Entra B2B guest user
D) Create a service principal for the vendor

<details>
<summary>Answer</summary>

**Correct: C**

B2B guest invitations let external users authenticate with their own home-tenant or social identity credentials while accessing specific resources you grant, with UserType set to Guest.

**Why the others are wrong:**
- Member users require your organization to manage a full identity lifecycle and credentials, unnecessary for temporary external access
- Local Windows accounts don't integrate with Entra ID-based resources like Teams/SharePoint Online
- Service principals represent applications/automation, not human interactive access

</details>

---

**Q6.** Which dynamic membership rule correctly adds users to a group only when their department is 'Sales' AND their usage location is 'US'?

A) (user.department -eq "Sales") -and (user.usageLocation -eq "US")
B) user.department = "Sales" AND user.usageLocation = "US"
C) user.department == "Sales" && user.usageLocation == "US"
D) (user.department -eq "Sales")

<details>
<summary>Answer</summary>

**Correct: A**

Microsoft Entra dynamic membership rules use PowerShell-style operators (-eq, -and, -or) with attribute expressions wrapped in parentheses when combined.

**Why the others are wrong:**
- Uses invalid operator syntax (=, AND) not recognized by the Entra rule engine
- Uses C-style operators (==, &&) which are not valid in Entra dynamic rule syntax
- Only expresses one condition — omits the usageLocation requirement entirely

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Your organization enables self-service password reset (SSPR) for all users using the default reset policy configuration. What is the minimum number of authentication methods a user must verify to reset their own password?

A) 1
B) 2
C) 3
D) 0 — SSPR requires no verification

<details>
<summary>Answer</summary>

**Correct: B**

The default SSPR policy sets 'Number of methods required to reset' to 2, requiring users to verify two registered authentication methods before resetting their password.

**Why the others are wrong:**
- 1 method is the default for registration, not reset — the exam distinguishes registration count from reset count
- 3 exceeds the default configuration (though it can be manually raised)
- SSPR always requires identity verification; it cannot be configured with zero methods

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** How many Microsoft Entra tenants can a single Azure subscription trust at any given point in time?

A) Zero — subscriptions don't require a tenant
B) Up to five
C) Unlimited, one per resource group
D) Exactly one

<details>
<summary>Answer</summary>

**Correct: D**

An Azure subscription always trusts exactly one Microsoft Entra tenant for authentication and authorization at any given time, though an admin can change which tenant it trusts.

**Why the others are wrong:**
- Every subscription must trust a tenant to authenticate users and manage RBAC — it cannot exist tenant-less
- A subscription cannot simultaneously trust multiple tenants
- Trust is set at the subscription level, not per resource group, and still limited to one tenant at a time

</details>

---

