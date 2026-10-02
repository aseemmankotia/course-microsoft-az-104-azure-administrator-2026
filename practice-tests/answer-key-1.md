# Answer Key — Practice Test 1

**Q1. Correct: D**

Administrative units let you scope a Microsoft Entra role such as Helpdesk Administrator to a defined subset of users or groups, restricting management capability to only the Marketing users.

---

**Q2. Correct: C**

Azure Policy with a deny effect evaluates resource creation requests and blocks non-compliant ones, making it the correct tool to enforce mandatory tagging.

---

**Q3. Correct: B**

DeployIfNotExists and Modify effects only apply automatically to new or updated resources going forward; a remediation task must be created and run to apply the deployment action to existing non-compliant resources.

---

**Q4. Correct: B**

A CanNotDelete lock allows authorized users to read and modify a resource (such as resizing or changing NIC settings) but blocks any delete operation, exactly matching the stated requirement.

---

**Q5. Correct: B**

AssignableScopes restricts the scopes at which a custom role definition is permitted to be assigned; the role can be used at that exact scope or any child scope beneath it (such as resources inside RG-Prod), but not above it.

---

**Q6. Correct: C**

Azure Budgets allow administrators to define a spending amount and set alert conditions at specific percentage thresholds, triggering automated email or action group notifications without impacting resources.

---

**Q7. Correct: A**

Administrative units let you restrict a Microsoft Entra role (like Helpdesk Administrator) to a defined subset of users, groups, or devices, giving least-privilege, scoped delegation that automatically applies to dynamic membership.

---

**Q8. Correct: C**

Custom RBAC roles let you combine specific data-plane actions — here, only start and restart actions plus read — into a role that grants exactly the required permissions without create, delete, or resize rights, assigned at the narrowest needed scope (resource group).

---

**Q9. Correct: D**

Policies with 'Modify' or 'DeployIfNotExists' effects only apply automatically to new or updated resources; a remediation task must be created (manually or via the assignment's Remediation tab) to apply the effect retroactively to already-existing non-compliant resources.

---

**Q10. Correct: D**

RBAC is an authorization system answering 'who can do what' on which resources by assigning roles to security principals; Azure Policy is a governance system that audits or enforces resource properties and configurations (like allowed SKUs, required tags, or allowed regions) independent of user identity.

---

**Q11. Correct: B**

RA-GZRS combines zone-redundant storage within the primary region (protecting against datacenter/zone failure) with geo-replication to a secondary region and read access (RA) to that secondary region during an outage — the only option satisfying both requirements.

---

**Q12. Correct: B**

Hot tier is optimized for frequent access during the active editing period, Cool tier reduces storage cost for infrequently accessed data after 30 days, and Archive tier offers the lowest cost for long-term compliance retention where hours-long rehydration latency is acceptable.

---

**Q13. Correct: A**

A Service SAS can be scoped to a single container, granted specific permissions (such as write), and given a defined expiry time, meeting the requirement without exposing the account key or granting broader access.

---

**Q14. Correct: B**

Setting the default action to Deny blocks public access, adding a VNet service endpoint permits traffic only from the specified subnet, and the 'Allow trusted Microsoft services' exception explicitly permits access from Microsoft-managed services like Azure Backup even though the default action is Deny.

---

**Q15. Correct: A**

Object replication requires blob versioning enabled on both the source and destination accounts to track blob changes, and change feed enabled on the source account to record and replay create, update, and delete operations to the destination.

---

**Q16. Correct: C**

Azure File Sync synchronizes an Azure file share with on-premises Windows Server, and cloud tiering automatically moves infrequently accessed files to Azure while keeping a local cache of frequently accessed files, exactly matching the described low-latency and space-saving requirements.

---

**Q17. Correct: C**

A service SAS tied to a stored access policy lets administrators change permissions or revoke access instantly by modifying or deleting the policy on the container, without needing to regenerate account keys or issue a new token.

---

**Q18. Correct: C**

The 'Allow trusted Microsoft services' exception permits specific first-party Azure services, including Azure Backup, to bypass the storage account firewall and access the account even when public network access is otherwise restricted to selected networks.

---

**Q19. Correct: B**

Two or more VMs deployed across different Availability Zones and running in the same zone-redundant configuration are covered by Microsoft's 99.99% SLA, since zones are physically separate datacenters with independent power, cooling, and networking.

---

**Q20. Correct: D**

ACI is designed for running single, standalone containers with no orchestration overhead, billed per second of vCPU/memory consumption — ideal for short-lived, stateless batch jobs.

---

**Q21. Correct: B**

The cooldown period (default 5 minutes) is the amount of time Autoscale waits after completing a scale action before it evaluates the rules again, preventing rapid, repeated scaling flapping.

---

**Q22. Correct: C**

Deployment slots let you deploy and warm up a new version in an isolated slot with its own hostname, then perform a swap operation that exchanges the slots virtually instantaneously with no downtime, and the swap can be rolled back if issues are found.

---

**Q23. Correct: D**

Encryption at Host encrypts data on the VM host itself, covering the OS disk, data disks, disk caches, and temporary disk end-to-end, and it requires no in-guest agent since encryption happens at the underlying hardware/host layer.

---

**Q24. Correct: A**

Bicep is a domain-specific language (DSL) that provides a cleaner authoring experience; the Bicep CLI (or integrated tooling) transpiles .bicep files into standard ARM JSON templates, and Azure Resource Manager deploys that resulting JSON exactly as it would a hand-written ARM template.

---

**Q25. Correct: C**

Flexible orchestration mode allows mixing VM sizes, disk types, and pricing models (Spot and standard) within one scale set, and each VM instance behaves and can be managed like a standalone VM while still supporting up to 1000 instances and high availability across zones.

---

**Q26. Correct: A**

Azure Container Apps is built on Kubernetes and KEDA under the hood but abstracts cluster management, and natively supports HTTP-based autoscaling rules including scale-to-zero for idle workloads.

---

**Q27. Correct: D**

Slot settings marked as sticky are pinned to the slot itself and never move during a swap. Only the deployed code and non-sticky settings swap between slots, so the production slot retains its own sticky ConnectionString value pointing to the production database after the swap completes.

---

**Q28. Correct: B**

All Azure Managed Disks are encrypted at rest by default using server-side encryption (SSE) with platform-managed keys, transparently and at no extra cost, with no configuration or extension required.

---

**Q29. Correct: A**

Azure VNet peering is non-transitive by design. Even though A-B and B-C are peered, A and C have no relationship unless a direct peering is explicitly created between them.

---

**Q30. Correct: C**

A Private DNS zone only resolves names for VNets that have an explicit virtual network link created (either with or without auto-registration). Without the link, the zone is invisible to VMs in that VNet.

---

**Q31. Correct: B**

ASGs let you group VMs by application role (e.g., 'WebServers', 'DBServers') and reference that group name in NSG rules instead of hardcoding IP addresses, simplifying management as VMs scale.

---

**Q32. Correct: B**

The time to mark an instance unhealthy is Interval x Unhealthy Threshold = 5s x 2 = 10 seconds. This calculation is directly tested on the exam.

---

**Q33. Correct: A**

Application Gateway operates at Layer 7 and natively supports URL path-based routing to different backend pools, SSL termination, and WAF integration to inspect for OWASP Top 10 threats — exactly matching all three requirements.

---

**Q34. Correct: C**

A Private Endpoint provisions a NIC with a private IP address from the VNet directly mapped to the SQL Database resource, and combined with disabling public network access, the database becomes completely unreachable over the internet — this is the key distinction from Service Endpoints.

---

**Q35. Correct: D**

Application Gateway is a layer 7 (HTTP/HTTPS) load balancer that supports SSL/TLS termination, URL path-based routing, and multiple backend pools based on request content — exactly what's required here.

---

**Q36. Correct: A**

A Private Endpoint assigns a private IP address from the VNet to the SQL Database via Azure Private Link, keeping traffic entirely on the Microsoft backbone. Combined with disabling public network access, the database becomes unreachable from any public endpoint, satisfying full isolation.

---

**Q37. Correct: D**

Azure Site Recovery continuously replicates VM disk changes to a secondary region, achieving an RPO as low as 30 seconds to a few minutes, and allows failover within minutes to meet the 15-minute RTO.

---

**Q38. Correct: A**

Connection Troubleshoot performs an actual connection test to a destination and reports hop-by-hop results, identifying whether NSGs, user-defined routes, or other configuration issues are blocking traffic.

---

**Q39. Correct: D**

A metric alert rule can evaluate the Percentage CPU metric against an 80% threshold over a 5-minute aggregation window, and an action group can fan out to both an email receiver and a Logic App receiver when the alert fires.

---

**Q40. Correct: A**

A single Azure Backup policy supports multiple retention ranges (daily, weekly, monthly, yearly) within the same policy, letting you keep daily points for 30 days while also retaining a designated weekly point for 12 weeks.

---

**Q41. Correct: A**

Metrics are numerical values collected at regular intervals and stored in a time-series database for fast, near real-time charting and alerting, while Logs are event/record data stored in a Log Analytics workspace and queried with Kusto Query Language for richer, correlated analysis.

---

**Q42. Correct: D**

Test Failover creates an isolated copy of the replicated VMs in a designated test network, allowing you to validate the DR configuration without disrupting ongoing replication or affecting the production environment.

---

