# Practice Test 2: AZ-104: Azure Administrator Associate Exam Prep

- **Questions:** 42
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A company uses Microsoft Entra ID. The IT helpdesk team must be able to reset passwords and manage licenses only for users in the Marketing department, without being granted directory-wide User Administrator permissions. Which feature should you implement?

A) Assign the helpdesk team the Global Administrator role scoped to the Marketing security group
B) Create an administrative unit containing the Marketing users and assign the helpdesk team the User Administrator role scoped to that administrative unit
C) Enable Privileged Identity Management (PIM) for the Marketing group and set eligible assignments for the helpdesk team
D) Create a custom Azure RBAC role and assign it at the Marketing resource group scope

---

**Q2.** You need to create a custom Azure role that allows a team to read blob data inside storage accounts but must NOT allow them to change storage account network rules or access keys. Which role definition element must you use to grant the blob data read permission?

A) "AssignableScopes": ["Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read"]
B) "NotActions": ["Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read"]
C) "DataActions": ["Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read"]
D) "Actions": ["Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read"]

---

**Q3.** An Azure Policy assignment at the subscription level denies creation of any resource without a CostCenter tag. A project team needs to deploy a short-term test VM without a CostCenter tag for a valid, documented business reason, without removing or modifying the policy assignment for all other resources. What should you configure?

A) Change the policy effect from Deny to Audit at the subscription level
B) Add a resource lock of type ReadOnly on the resource group
C) Create a policy exemption scoped to the test VM's resource group with a category of Waiver
D) Move the test VM's resource group into a new management group excluded from the subscription

---

**Q4.** You need to prevent an Azure SQL Database from being deleted while still allowing database administrators to scale the service tier and modify firewall rules. Which resource lock should you apply?

A) ReadOnly lock
B) Azure Policy with a Deny effect on the delete action
C) An RBAC Deny assignment on the Contributor role
D) CanNotDelete lock

---

**Q5.** A resource group was deployed via an Azure Blueprint that applied resource locks as part of the artifact. A user with the Owner role assigned at the resource group scope attempts to delete one of the locked resources and receives an authorization error, even though Owner normally includes delete permissions. What is the most likely cause?

A) The user's Owner role assignment has expired due to PIM time-bound settings
B) A system-generated deny assignment created by the blueprint lock is blocking the delete action regardless of the Owner role
C) The resource has an Azure Policy assignment with an Audit effect preventing deletion
D) The user is missing the Microsoft.Resources/deployments/write permission

---

**Q6.** Which statement correctly differentiates a Microsoft Entra ID role from an Azure RBAC role?

A) Entra ID roles control access to directory-level objects such as users, groups, and domains, while Azure RBAC roles control access to Azure resources such as VMs, storage, and networking
B) Azure RBAC roles are only used for read-only access, while Entra ID roles govern write access
C) Entra ID roles control access to Azure resources such as VMs and storage accounts, while RBAC roles control directory objects such as users and groups
D) Entra ID roles and Azure RBAC roles are the same and can be assigned interchangeably at any scope

---

**Q7.** A company needs to delegate password reset and license management rights over only the 300 user accounts in its EU subsidiary, without granting any rights over the remaining 5,000 users in the tenant or over any Azure subscriptions. Which solution BEST meets this requirement?

A) Create a custom RBAC role scoped to the resource group that contains the EU subsidiary's resources
B) Create a management group for the EU subscriptions and assign the Owner role at that management group
C) Create an administrative unit containing the EU subsidiary's user accounts and assign the User Administrator role scoped to that administrative unit
D) Create a dynamic security group for EU users and assign Global Administrator to the group's owner

---

**Q8.** An Azure Policy initiative enforcing 'Audit VMs that do not use managed disks' is assigned at the subscription scope. One resource group contains legacy VMs scheduled for decommissioning in 30 days that should stop appearing as non-compliant during that period, while the policy must continue to be enforced everywhere else in the subscription. What should the administrator do?

A) Create a policy exemption scoped to the resource group with a waiver category and a 30-day expiration date
B) Change the policy assignment's effect from Audit to Disabled at the subscription scope
C) Apply a ReadOnly resource lock to the resource group containing the legacy VMs
D) Remove the resource group from the subscription's management group hierarchy for 30 days

---

**Q9.** An administrator must create a custom RBAC role that allows users to perform all operations on virtual machines except deleting them, and the role must be assignable at both the subscription scope and at individual resource group scopes within that subscription. Which role definition configuration meets this requirement?

A) Set AssignableScopes to the resource group ID only, and set Actions to 'Microsoft.Compute/virtualMachines/write'
B) Set AssignableScopes to the management group ID and add 'Microsoft.Compute/virtualMachines/delete' to Actions
C) Set AssignableScopes to the subscription ID, add 'Microsoft.Compute/virtualMachines/*' to Actions, and add 'Microsoft.Compute/virtualMachines/delete' to NotActions
D) Set AssignableScopes to '/' for the tenant root and add 'Microsoft.Compute/*' to NotActions

---

**Q10.** A subscription administrator applies a CanNotDelete lock to a resource group containing a virtual network. A network engineer who holds the Owner role at the subscription scope attempts to delete a subnet inside that virtual network using Azure CLI. What is the result?

A) The deletion succeeds because the Owner role overrides resource locks
B) The deletion succeeds because CanNotDelete locks only apply to top-level resources, not child resources like subnets
C) The deletion fails because CanNotDelete locks block delete operations for every user regardless of assigned RBAC role, until the lock is removed
D) The deletion fails only because it was attempted via CLI; the same operation would succeed in the Azure portal

---

**Q11.** A company has a StorageV2 account named storesrc in East US and wants to asynchronously replicate all blob changes to a secondary account named storedest in West US for compliance archiving. They create an object replication policy in the Azure portal, but validation fails with an error about a missing prerequisite. Both accounts currently have only blob soft delete enabled. Which change resolves the validation error?

A) Change the redundancy of storedest to GZRS
B) Enable the hierarchical namespace (Data Lake Storage Gen2) feature on both accounts
C) Enable blob versioning on both storesrc and storedest
D) Configure a lifecycle management policy on storesrc before creating the replication policy

---

**Q12.** A financial services company must store trade records in Blob Storage so that once written, records cannot be modified or deleted for exactly 7 years, the retention period must be extendable if regulations change, and the protection must not be removable early even by a Global Administrator. Which configuration meets this requirement?

A) Enable a version-level time-based retention policy locked at 2555 days on the container
B) Apply a legal hold with the tag "7-year-retention" on the container
C) Enable blob soft delete with a 2555-day retention period
D) Enable a time-based retention policy in the "unlocked" state set to 2555 days

---

**Q13.** You issued an ad-hoc service SAS (not tied to a stored access policy) scoped to a blob container, signed with the storage account's key, with an expiry 30 days out. Two days later the token leaks publicly. Other applications are actively using different SAS tokens signed with the same account key, and you cannot risk breaking their access. What is the outcome regarding revoking ONLY the leaked token?

A) Regenerate the storage account access key that signed the SAS
B) It cannot be selectively revoked—you must either wait for expiry or accept breaking other SAS tokens by rotating the key; this is why stored access policies should be used for revocable SAS
C) Delete and recreate the container
D) Enable Microsoft Entra ID authorization and disable Shared Key access entirely

---

**Q14.** You deploy Azure File Sync between an on-premises server endpoint and an Azure file share (cloud endpoint), with cloud tiering enabled and a volume free space policy of 20%. Six months later, users report that some recently uploaded files take a long time to open, while other older files near the start of the folder alphabetically open instantly — with no consistent pattern related to file name. What is the MOST likely cause?

A) Cloud tiering has converted the least recently accessed files into tiered stub files based on the free space policy; opening a tiered file requires recalling it from the Azure file share, causing the delay, and file name/position is unrelated
B) The cloud tiering policy is evaluated purely by file size, so large files are always tiered first regardless of access pattern
C) The Storage Sync Service change detection heuristic prioritizes files by name rather than by access recency
D) The cloud endpoint's access tier is set to Cool instead of Hot, causing higher latency on all read operations

---

**Q15.** A company's storage account uses GZRS. During a regional outage affecting the primary region, the application must continue to READ data (read-only access is acceptable) immediately, without any manual intervention or failover. Which change should be made, and why?

A) Switch to LRS with a read-access endpoint, because LRS automatically provides a secondary readable endpoint
B) Switch to RA-GZRS, because it exposes a read-only endpoint in the secondary region that remains available during a primary region outage without requiring failover
C) No change is needed — GZRS already exposes an automatically available read-only secondary endpoint during outages
D) Initiate a customer-managed account failover on the GZRS account to swap primary and secondary, then read from the new primary

---

**Q16.** An enterprise needs to grant a partner application read and write access to a specific blob container for 4 hours. Policy prohibits storing or distributing storage account access keys anywhere, and requires that the credential used to sign the SAS be revocable independently, without regenerating account keys or invalidating other issued SAS tokens. Which SAS type should be issued?

A) Account SAS signed with the storage account key
B) Service SAS signed with the storage account key
C) User delegation SAS signed with a Microsoft Entra ID token obtained via Get User Delegation Key
D) Anonymous public read/write access configured on the container

---

**Q17.** A company has a general-purpose v2 storage account 'srcstore01' in East US with a container named 'sales-data'. They want to configure Object Replication so that new and updated blobs are asynchronously copied to a second storage account 'destore01' in West Europe for disaster recovery reporting. When creating the replication policy in the portal, the operation fails with a validation error. Which requirement, if unmet, would cause this failure?

A) The source and destination storage accounts must be in the same Azure region
B) Blob versioning must be enabled on both the source and destination accounts, and both must be standard general-purpose v2 (or premium block blob) accounts
C) The destination storage account must have lifecycle management policies disabled
D) Both storage accounts must have hierarchical namespace (Data Lake Storage Gen2) enabled

---

**Q18.** An administrator generated several service SAS tokens for third-party partners to access blobs in container 'reports', all signed using a stored access policy defined on that container. A security incident occurs and the partners' access must be revoked immediately, without affecting SAS tokens or applications using the storage account key for other containers. What should the administrator do?

A) Regenerate the storage account access keys
B) Delete or modify the stored access policy associated with the issued SAS tokens
C) Change the container's public access level to Private
D) Add a storage account firewall rule denying all public network access

---

**Q19.** A financial services company runs a tier of 6 identical VMs in a single Azure region. The workload requires 99.99% availability SLA and must survive the complete loss of a single datacenter within that region, while VMs must still be able to communicate with low latency. Which configuration BEST meets these requirements?

A) Deploy VMs across three Availability Zones in the region
B) Deploy VMs in an availability set spanning multiple fault domains
C) Deploy VMs in an availability set with the maximum number of update domains
D) Deploy VMs using a proximity placement group

---

**Q20.** A company needs to encrypt the OS disk, data disks, temporary disk, and disk caches of Azure VMs at rest without installing any encryption agent inside the guest OS, and with minimal performance overhead. Which feature BEST satisfies these requirements?

A) Enable Azure Disk Encryption (ADE) with a customer-managed key
B) Enable Server-Side Encryption (SSE) with platform-managed keys
C) Enable Encryption at Host
D) Enable Azure Backup with encryption enabled

---

**Q21.** A company built a custom VM image and now needs to distribute versions of that image to VMs in three Azure regions, control how many replicas exist per region, and share specific versions with another subscription. Which solution BEST meets these requirements?

A) Create a Managed Image and manually copy the VHD file to each target region
B) Push the VM disk as an artifact to Azure Container Registry
C) Store the VHD in a geo-redundant storage account and reference it directly from each region
D) Create a Shared Image Gallery, publish image versions, and configure target region replication

---

**Q22.** An administrator needs to update only the NIC configuration of a single VM in a resource group and deploys an ARM template using Complete mode. After the deployment finishes, several unrelated resources that previously existed in the resource group are gone. What is the MOST likely cause?

A) Complete mode deletes any resource in the target scope that is not defined in the template
B) Incremental mode was actually applied and merged the resources incorrectly
C) The template contained a destroy() function that ran automatically
D) An Azure Policy assignment triggered automatic deletion of noncompliant resources

---

**Q23.** A Virtual Machine Scale Set configured with autoscale is rapidly scaling out and then back in every few minutes in response to short CPU spikes, causing instability and unnecessary cost. Which setting should be adjusted to resolve this scale flapping?

A) Increase the maximum instance count for the scale set
B) Increase the cooldown period between scaling actions
C) Change the scale-in policy from Default to NewestVM
D) Add a custom autoscale metric based on CPU

---

**Q24.** A company is building a microservices application that needs event-driven autoscaling based on message queue length, built-in Dapr service-to-service invocation and state management, and must NOT require the team to provision or manage any Kubernetes cluster infrastructure. Which Azure service BEST meets these requirements?

A) Azure Kubernetes Service (AKS) with the KEDA add-on enabled
B) Azure Container Instances (ACI) using a multi-container container group
C) Azure Container Apps
D) Azure App Service using a custom container

---

**Q25.** A company is designing a Virtual Machine Scale Set to host a fleet of API servers. The requirements are: mix different VM sizes within the same scale set, attach unique persistent data disks to individual instances, and register instances with both an Azure Load Balancer and an Application Gateway at the same time. Which orchestration mode should the scale set use?

A) Flexible orchestration mode
B) Uniform orchestration mode
C) Availability set with manual scaling
D) Azure Dedicated Host with a scale set overlay

---

**Q26.** A company runs a business-critical API on an Azure App Service Premium v3 plan. Before a major version release, they want real production users to hit the new code for only 5% of requests while the rest continue to reach the current version, with the ability to instantly send 100% of traffic to the new version once validated, and without provisioning any new App Service Plan. Which approach BEST meets these requirements?

A) Deploy the new version directly to the production slot and use Azure Front Door origin groups to split traffic
B) Create a deployment slot, deploy the new version to it, configure a traffic routing percentage to send 5% of production traffic to the slot, then perform a full slot swap once validated
C) Create a second App Service Plan in the same region and use Traffic Manager weighted routing between the two plans
D) Deploy the new version to a Virtual Machine Scale Set and configure a rolling upgrade policy alongside the existing App Service

---

**Q27.** A company must encrypt the OS disk, all data disks, AND the temporary disk of their Azure VMs using keys they manage in Azure Key Vault, without installing any encryption extension or agent inside the guest operating system. Which solution meets this requirement?

A) Encryption at Host with customer-managed keys
B) Azure Disk Encryption (ADE) using BitLocker/DM-Crypt
C) Azure Storage Service Encryption with Microsoft-managed keys
D) Azure File Sync encryption in transit

---

**Q28.** A development team needs to run a containerized HTTP API that automatically scales to zero instances when idle, supports built-in HTTPS ingress, and provides revision-based traffic splitting for blue-green releases — all without provisioning or managing an underlying Kubernetes cluster. Which Azure service should they choose?

A) Azure Container Apps
B) Azure Kubernetes Service (AKS) with the HTTP application routing add-on
C) Azure Container Instances (ACI) with a public IP and DNS label
D) Azure App Service on Linux with a custom container

---

**Q29.** A VM's NIC is associated with NSG-A, which has a rule at priority 100 denying all inbound traffic from the Internet. The subnet containing the VM is associated with NSG-B, which has a rule at priority 100 allowing inbound TCP 443 from the Internet. Users report that HTTPS traffic never reaches the VM. What is the cause?

A) The priority number of NSG-B's allow rule must be set lower than NSG-A's deny rule for traffic to pass through
B) NSGs can only be associated with either a subnet or a NIC, not both simultaneously, so this configuration is invalid and traffic is dropped by default
C) The default NSG rules automatically override any custom rule, regardless of its priority number
D) Traffic must be permitted by both the subnet NSG and the NIC NSG; because NSG-A denies all inbound traffic at the NIC level, the traffic is blocked regardless of NSG-B's allow rule

---

**Q30.** A company's on-premises network is connected to an Azure VNet via a Site-to-Site VPN Gateway. The company needs on-premises servers to reach an Azure Storage account using a private IP address, with name resolution working correctly from on-premises, and without traffic traversing the public internet. Which solution meets these requirements?

A) Deploy a private endpoint for the storage account, link a Private DNS zone to the VNet, and configure DNS forwarding from on-premises to a DNS server in Azure
B) Configure a service endpoint for Microsoft.Storage on the VNet subnet
C) Enable the 'Allow trusted Microsoft services' exception on the storage account's firewall
D) Deploy a NAT gateway on the subnet and associate it with the storage account

---

**Q31.** A Hub VNet contains a VPN Gateway connected to an on-premises network. A Spoke VNet is peered with the Hub VNet. You need on-premises resources to reach VMs in the Spoke VNet through the Hub's VPN Gateway, without deploying a separate gateway in the Spoke. What must you configure?

A) Enable 'Allow forwarded traffic' on both the Hub-to-Spoke and Spoke-to-Hub peerings
B) Create a route table on the Hub subnet with a route pointing to the Spoke VNet's address space
C) On the Hub-to-Spoke peering, enable 'Use remote gateways'
D) On the Spoke-to-Hub peering, enable 'Use remote gateways'; on the Hub-to-Spoke peering, enable 'Allow gateway transit'

---

**Q32.** You deploy a third-party firewall Network Virtual Appliance (NVA) in a Hub VNet. You need all internet-bound traffic from VMs in a peered Spoke subnet to be inspected by the NVA before leaving Azure. What should you configure on the Spoke subnet?

A) A user-defined route for 0.0.0.0/0 with next hop type 'Virtual network gateway'
B) A user-defined route for 0.0.0.0/0 with next hop type 'Virtual appliance', specifying the NVA's private IP address as the next hop
C) An NSG rule that denies all outbound traffic except traffic destined for the NVA's IP address
D) A service endpoint for Microsoft.Network on the Spoke subnet

---

**Q33.** Contoso hosts a web application at contoso.com. Requests to /images and /api must route to two different backend pools, TLS must be terminated at the edge, and the solution must inspect and block SQL injection and cross-site scripting attempts. Which Azure service configuration BEST meets these requirements?

A) Azure Load Balancer Standard SKU with HTTP health probes on each backend pool
B) Azure Application Gateway using the WAF_v2 SKU with path-based routing rules
C) Azure Bastion configured with custom inbound routing rules for each path
D) Azure Traffic Manager using the priority routing method

---

**Q34.** You need to configure an Azure VPN Gateway in active-active mode so that two on-premises VPN devices can each maintain simultaneous active tunnels to both gateway instances for maximum resiliency. Which requirement must be met to enable this configuration?

A) The VPN Gateway must use the Basic SKU
B) BGP must be disabled on the gateway before active-active mode can be enabled
C) Only a Policy-based VPN type supports active-active mode
D) The VPN Gateway must use a non-Basic SKU (such as VpnGw1 or higher), and each gateway instance must be assigned its own public IP address

---

**Q35.** A hub-and-spoke topology uses a Network Virtual Appliance (NVA) in the hub for traffic inspection. A route table applied to the spoke subnet contains a user-defined route with prefix 10.0.0.0/16 pointing to the NVA's private IP as next hop. The VPN Gateway in the hub also advertises a BGP route for on-premises network 10.0.1.0/24. A VM in the spoke sends traffic to 10.0.1.5 (on-premises). Which route does Azure use for this traffic?

A) The UDR to the NVA (10.0.0.0/16), because user-defined routes always take precedence over BGP routes regardless of prefix length
B) The system default route, because a routing conflict between UDR and BGP causes Azure to fall back to the system route
C) The traffic is dropped because Azure cannot resolve conflicting routes of different types
D) The BGP route to the VPN Gateway (10.0.1.0/24), because Azure route selection uses longest prefix match first, and only uses route-type priority (UDR > BGP > System) to break ties within the same prefix length

---

**Q36.** A company uses a hub-and-spoke architecture. A Private Endpoint for an Azure SQL Database was created in a subnet in the Hub VNet, and the associated Private DNS zone (privatelink.database.windows.net) is linked only to the Hub VNet. VMs in a Spoke VNet, peered to the Hub, can reach the private endpoint's IP over the peering connection but their DNS queries for the SQL server's FQDN still resolve to the database's public IP address. What should the administrator do to fix name resolution for the Spoke VNet VMs?

A) Enable 'Allow Gateway Transit' on the VNet peering connection between Hub and Spoke
B) Create a Service Endpoint for Microsoft.Sql on the Spoke subnet
C) Configure a user-defined route in the Spoke subnet directing SQL traffic to the private endpoint's IP address
D) Add a virtual network link from the existing Private DNS zone to the Spoke VNet

---

**Q37.** A company replicates a set of business-critical Azure VMs from Region A to Region B using Azure Site Recovery (Azure-to-Azure replication). The business requirement is an RPO of 15 minutes for these VMs. The current replication policy has an app-consistent snapshot frequency of 4 hours and a recovery point retention of 24 hours. Which statement correctly describes what is needed to meet the 15-minute RPO?

A) Increase the app-consistent snapshot frequency to every 15 minutes to guarantee the RPO
B) For Azure-to-Azure replication, ASR continuously replicates disk writes and typically achieves an RPO of under 1 minute; no change is required to meet a 15-minute RPO
C) Reduce the recovery point retention setting in the replication policy to 15 minutes
D) Add the VMs to a multi-VM consistency group and set its failover frequency to 15 minutes

---

**Q38.** A VM in a subnet cannot reach a specific destination IP address on TCP port 443. You suspect an NSG rule is silently blocking the traffic and want to verify, without generating any actual network traffic, whether a packet matching this 5-tuple would be allowed or denied. Which Network Watcher tool should you use?

A) Connection troubleshoot
B) NSG flow logs
C) Effective security rules
D) IP flow verify

---

**Q39.** A Recovery Services vault protects several VMs. The security team requires that if backup data is deleted (accidentally or maliciously), it must remain recoverable for 14 days after the deletion occurs. Which feature meets this requirement?

A) Multi-user authorization (MUA) using Azure Resource Guard
B) Cross Region Restore
C) Immutable vault
D) Soft delete

---

**Q40.** You need to query the Perf table in a Log Analytics workspace to find, for each computer, the average '% Processor Time' over the last 24 hours, returning only computers whose average exceeds 80%. Which KQL query is correct?

A)
Perf
| where CounterName == "% Processor Time"
| where AvgCPU > 80
| summarize avg(CounterValue) by Computer, ago(24h)

B)
Perf
| summarize AvgCPU = avg(CounterValue) by Computer
| where TimeGenerated > ago(24h) and CounterName == "% Processor Time" and AvgCPU > 80

C)
Perf
| where TimeGenerated > ago(24h) and CounterName == "% Processor Time"
| summarize AvgCPU = avg(CounterValue) by Computer
| where AvgCPU > 80

D)
Perf
| where TimeGenerated > ago(24h)
| where CounterName == "% Processor Time"
| where CounterValue > 80
| summarize by Computer

A) Query A
B) Query B
C) Query C
D) Query D

---

**Q41.** Which statement correctly differentiates Azure Monitor metric alerts from log alerts (log search alerts)?

A) Both alert types use the same underlying rule engine and share an identical minimum evaluation frequency of 1 minute
B) Log alerts can only trigger action groups configured for email notification, while metric alerts can trigger any action group type
C) Metric alerts require a Log Analytics workspace as their data source, while log alerts do not
D) Metric alerts evaluate near real-time platform metric data at frequencies as low as 1 minute, whereas log alerts run a scheduled Log Analytics query with a minimum evaluation frequency of 5 minutes

---

**Q42.** A subscription owner wants to be automatically notified by email whenever Microsoft schedules planned maintenance that could affect the Azure region hosting their VMs — separate from monitoring the health of any individual VM resource. Which service should be configured with an alert to meet this requirement?

A) Azure Service Health
B) Azure Resource Health
C) Azure Monitor Activity Log alerts
D) Network Watcher

---

