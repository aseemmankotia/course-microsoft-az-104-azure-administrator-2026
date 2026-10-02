# Answer Key — Practice Test 2

**Q1. Correct: B**

Administrative units let you scope directory role assignments (like User Administrator) to a defined subset of users, groups, or devices, exactly what's needed here.

---

**Q2. Correct: C**

DataActions govern operations on the data plane, such as reading blob contents, separately from control-plane management operations.

---

**Q3. Correct: C**

Policy exemptions let you exclude a specific scope from an assignment's evaluation with documented justification, without touching the assignment itself or affecting other resources.

---

**Q4. Correct: D**

A CanNotDelete lock blocks delete operations only, while still permitting reads and modifications such as scaling tiers or updating firewall rules.

---

**Q5. Correct: B**

Blueprint-applied resource locks generate a system deny assignment that overrides ALL RBAC role assignments, including Owner, for the locked operation.

---

**Q6. Correct: A**

Microsoft Entra ID roles (e.g., Global Administrator, User Administrator) govern the directory itself, while Azure RBAC roles (e.g., Owner, Contributor) govern access to Azure resources at management group, subscription, resource group, or resource scope.

---

**Q7. Correct: C**

Administrative units scope Microsoft Entra ID administrative roles to a defined subset of users or groups. Assigning User Administrator at the administrative unit scope grants password reset and license management rights only over the members of that unit, satisfying least privilege.

---

**Q8. Correct: A**

Policy exemptions let an administrator exclude a specific scope from policy evaluation temporarily, with a category (Waiver or Mitigated) and an expiration date, while leaving the policy assignment fully enforced everywhere else.

---

**Q9. Correct: C**

Setting AssignableScopes to the subscription ID allows the role to be assigned at the subscription or at any child resource group. Granting the wildcard VM action and then subtracting only the delete action via NotActions grants full VM management except delete, exactly as required.

---

**Q10. Correct: C**

Resource locks operate independently of RBAC permissions. A CanNotDelete lock on a resource group prevents delete operations on that resource group and its child resources for all users and all management interfaces, regardless of RBAC role, until the lock itself is removed.

---

**Q11. Correct: C**

Object replication requires blob versioning to be enabled on BOTH the source and destination accounts (and change feed on the source) before a policy can be validated and created. Soft delete alone does not satisfy this prerequisite.

---

**Q12. Correct: A**

A locked time-based retention policy enforces true WORM protection: no user, including a Global Administrator, can delete or modify blobs before the retention date, and locked policies explicitly allow the retention period to be extended (up to 5 times, by up to 10 years) but never shortened or removed.

---

**Q13. Correct: B**

An ad-hoc SAS with no stored access policy has no independent revocation mechanism. The only way to invalidate it early is to rotate the account key that signed it, which invalidates every other SAS signed with that same key — violating the constraint of not breaking other applications. This scenario is the exact reason Microsoft recommends stored access policies, which allow individual policy-level revocation.

---

**Q14. Correct: A**

Cloud tiering replaces the content of infrequently accessed files with lightweight stub (reparse point) files on the server endpoint once the volume free space threshold is reached, prioritizing the coldest files by access recency and heat, not alphabetical order. Opening a tiered file triggers an on-demand recall from the Azure file share, which is slower than reading a locally cached file — explaining the described symptom, with the alphabetical observation being coincidental.

---

**Q15. Correct: B**

RA-GZRS (Read-Access Geo-Zone-Redundant Storage) adds a separate read-only endpoint in the secondary region that is continuously available, including during a primary region outage, with no failover action required.

---

**Q16. Correct: C**

A user delegation SAS is signed using a key derived from Microsoft Entra ID credentials (via Get User Delegation Key) rather than the storage account key, so no account key is ever stored or distributed. It can be revoked by revoking the underlying Entra ID role assignment or by the delegation key's own short expiration, without touching account keys or affecting other SAS tokens.

---

**Q17. Correct: B**

Object Replication requires blob versioning enabled on both source and destination accounts (change feed must also be enabled on the source), and both accounts must be standard GPv2 or premium block blob storage accounts. Without versioning enabled, the replication policy creation fails validation.

---

**Q18. Correct: B**

SAS tokens tied to a stored access policy inherit their permissions and expiry from that policy. Deleting or modifying the stored access policy immediately invalidates every SAS token issued against it, without requiring account key regeneration.

---

**Q19. Correct: A**

Availability Zones map to physically separate datacenters within a region, each with independent power, cooling, and networking. Spreading VMs across zones is the only construct that provides the 99.99% SLA and protects against full datacenter loss.

---

**Q20. Correct: C**

Encryption at Host encrypts data on the physical host itself, covering OS disks, data disks, temporary disks, and caches, all without requiring BitLocker/DM-Crypt agents inside the guest OS, and with negligible performance impact since it happens below the VM layer.

---

**Q21. Correct: D**

Shared Image Gallery supports image versioning, configurable per-region replica counts, multi-region replication, and RBAC-based sharing across subscriptions and tenants — exactly what's described.

---

**Q22. Correct: A**

In Complete deployment mode, Resource Manager deletes resources that exist in the resource group but are not defined in the template. Since only the VM/NIC was included, everything else in the group was removed.

---

**Q23. Correct: B**

The cooldown period defines the minimum time to wait after a scale action before evaluating metrics again. A short cooldown causes autoscale to react to transient spikes, triggering rapid scale-out/scale-in cycles. Increasing it smooths out this flapping.

---

**Q24. Correct: C**

Azure Container Apps is a fully managed serverless container platform built on Kubernetes, KEDA, and Dapr under the hood, exposing KEDA-based event-driven autoscaling and Dapr integration natively — without requiring the customer to provision or manage the underlying cluster.

---

**Q25. Correct: A**

Flexible orchestration mode allows mixing VM sizes and images within one scale set, supports per-instance unique data disks, and can register instances with both a Load Balancer and an Application Gateway simultaneously — capabilities Uniform mode does not fully support.

---

**Q26. Correct: B**

App Service deployment slots support 'routing rules' that send a configurable percentage of production traffic to a non-production slot for testing, and a slot swap can then promote the slot to 100% production traffic instantly with warm-up — all within the existing plan.

---

**Q27. Correct: A**

Encryption at Host encrypts data on the physical host so it never leaves unencrypted, covers OS, data, and temp/cache disks, requires no in-guest agent, and can be configured to use customer-managed keys via the disk encryption set integration with Key Vault.

---

**Q28. Correct: A**

Azure Container Apps is built on Kubernetes/KEDA under the hood but abstracts cluster management away, natively supports scale-to-zero, built-in HTTPS ingress, and revision management with traffic-splitting for blue-green or canary deployments.

---

**Q29. Correct: D**

When NSGs exist at both the subnet and NIC level, inbound traffic must be explicitly allowed by both NSGs to reach the VM. Priority numbers are only compared within the same NSG, not across NSGs. Since NSG-A's deny rule at the NIC level blocks the traffic outright, NSG-B's allow rule at the subnet level is irrelevant — the traffic never reaches the VM.

---

**Q30. Correct: A**

A private endpoint assigns the storage account a private IP address inside the VNet. For on-premises clients to resolve the storage account's FQDN to that private IP, the Private DNS zone must be linked to the VNet, and on-premises DNS must forward the relevant zone to a DNS server (or Azure DNS Private Resolver) reachable in Azure. This achieves fully private connectivity and correct name resolution.

---

**Q31. Correct: D**

Gateway transit lets a spoke VNet use a gateway deployed in the hub VNet instead of deploying its own. The hub side of the peering must have 'Allow gateway transit' enabled, and the spoke side must have 'Use remote gateways' enabled. Once configured, Azure automatically propagates the necessary routes.

---

**Q32. Correct: B**

To force traffic through an NVA, you create a UDR with the destination prefix 0.0.0.0/0 and next hop type 'Virtual appliance', pointing to the NVA's private IP address. This overrides the default system route to the internet and directs all outbound traffic through the NVA for inspection first.

---

**Q33. Correct: B**

Application Gateway operates at Layer 7, supports SSL/TLS termination, and can route based on URL path (path-based routing rules) to different backend pools. The WAF_v2 SKU adds Web Application Firewall capability to inspect and block OWASP threats like SQL injection and XSS — matching all stated requirements.

---

**Q34. Correct: D**

Active-active mode requires a Route-based VPN Gateway using a non-Basic SKU (VpnGw1 and above support it). In active-active mode, both gateway instances are active simultaneously, and each instance is assigned its own public IP address so on-premises devices can establish tunnels to both.

---

**Q35. Correct: D**

Azure route selection always applies longest prefix match first. Since 10.0.1.0/24 is more specific than 10.0.0.0/16, the BGP-learned route wins even though UDRs normally outrank BGP routes — that priority order (UDR > BGP > System) only applies when prefixes are equally specific.

---

**Q36. Correct: D**

Private DNS zones must be explicitly linked to every VNet that needs to resolve names in that zone. VNet peering does not propagate DNS zone links automatically, so the Spoke VNet needs its own virtual network link to the privatelink.database.windows.net zone to resolve the FQDN to the private endpoint's IP.

---

**Q37. Correct: B**

Azure-to-Azure VM replication in Site Recovery continuously replicates data at the disk-write level (not on a scheduled interval), which typically results in an RPO well under a minute. The 15-minute RPO target is already met without any configuration change; app-consistent snapshot frequency only affects the frequency of application-consistent recovery points, not the underlying crash-consistent RPO.

---

**Q38. Correct: D**

IP flow verify checks whether a packet matching a specified source/destination IP, port, and protocol (the 5-tuple) is allowed or denied by NSGs applied to a VM's NIC, and it does this without sending actual traffic — it evaluates the rule set directly.

---

**Q39. Correct: D**

Soft delete for Azure Backup retains deleted backup data in a recoverable state for a default retention period (14 days, extendable up to 180 days for vaulted backups), allowing you to undelete and restore the backup even after a deletion operation.

---

**Q40. Correct: C**

Query C correctly filters raw rows by time range and counter name first, then aggregates with summarize to compute the average per computer, and finally applies the AvgCPU > 80 filter after the alias exists — this is the valid and semantically correct order of operations in KQL.

---

**Q41. Correct: D**

Metric alerts operate on the metrics pipeline and can be evaluated as frequently as every 1 minute against near real-time data. Log alerts run a scheduled KQL query against a Log Analytics workspace (or Application Insights), with a minimum supported evaluation frequency of 5 minutes, introducing inherent query/ingestion latency.

---

**Q42. Correct: A**

Azure Service Health tracks service issues, planned maintenance, health advisories, and security advisories at the subscription, region, and service level, and supports configuring Service Health alerts (via action groups) to notify subscribers, such as by email, when planned maintenance is scheduled for the relevant region/service.

---

