## Chapter 1: Microsoft Entra ID: Users, Groups, and Administrative Units — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Security group vs Microsoft 365 group — which can contain devices as members? | Security group. Microsoft 365 groups support only user members. Exam tip: if the scenario mentions devices or Azure RBAC assignment, pick Security group. |
| 2 | Member user vs Guest (B2B) user — key directory attribute that differs | UserType property: 'Member' vs 'Guest'. Guests authenticate with their own home credentials; exam scenario clue = 'external vendor/partner using their own credentials' → Guest. |
| 3 | Microsoft Entra joined vs Hybrid joined vs Registered — which requires an on-prem AD DS join? | Hybrid joined only. Entra joined = cloud-only corporate device. Registered = BYOD/personal device (Entra ID recognizes it but doesn't own it). |
| 4 | Dynamic group membership rule syntax operator style | PowerShell-style: -eq, -ne, -and, -or, -contains, -notContains. Example: (user.department -eq "Sales") -and (user.usageLocation -eq "US") |
| 5 | License required for dynamic group membership rules | Microsoft Entra ID P1 or P2. Free/Basic tier tenants cannot use dynamic membership groups. Exam trap: 'wants dynamic group but has no P1 license' → must upgrade first. |
| 6 | What can an Administrative Unit contain? | Users, groups, and devices only — NOT resource groups or subscriptions. AUs scope Microsoft Entra directory roles, not Azure RBAC. |
| 7 | Default SSPR: methods required to REGISTER vs methods required to RESET | Register default = 1 method. Reset default = 2 methods. Exam distinguishes these two settings — don't confuse them. |
| 8 | Administrative Unit primary exam use case | Delegating directory-role administration (e.g., User Administrator, Helpdesk Administrator) to a limited scope of users/groups/devices — e.g., 'regional IT team manages only their branch's users.' |
| 9 | One Azure subscription trusts how many Microsoft Entra tenants at once? | Exactly one. It can be changed to trust a different tenant, but never trusts multiple simultaneously. |
| 10 | Assigned membership vs Dynamic membership group | Assigned = manual add/remove, works on any tier for free. Dynamic = rule-based automatic membership, requires Entra ID P1/P2 and evaluates attributes (department, jobTitle, etc.). |
| 11 | Which device join type is used for personal/BYOD phones accessing Outlook via app protection policies? | Microsoft Entra registered. The device is known to Entra ID but not owned/fully managed by the organization like a joined device. |
| 12 | PowerShell cmdlet property to enable dynamic membership when creating a group | Set GroupTypes to include "DynamicMembership" and set MembershipRuleProcessingState to "On" with New-MgGroup / Update-MgGroup. |
