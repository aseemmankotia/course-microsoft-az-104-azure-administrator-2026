# Practice Test 1: AZ-104: Azure Administrator Associate Exam Prep

- **Questions:** 42
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A company has a Microsoft Entra ID tenant with 5,000 users. The IT team wants to delegate password reset and basic user management permissions for only the 200 users in the Marketing department to a departmental helpdesk group, without granting them any permissions over other users in the tenant. What should the administrator configure?

A) Assign the Helpdesk Administrator Microsoft Entra role to the helpdesk group at the tenant level
B) Create a custom Azure RBAC role and assign it at the resource group scope containing Marketing resources
C) Create a dynamic security group for Marketing users and assign the Owner role at the subscription scope
D) Create an administrative unit containing the Marketing users and assign the Helpdesk Administrator role scoped to that administrative unit

---

**Q2.** An organization must ensure that every resource group created in any subscription automatically includes a 'CostCenter' tag, and that resource group creation is blocked if the tag is missing. Which Azure governance feature should be used?

A) A custom Azure RBAC role that requires a tag input parameter
B) A resource lock of type CanNotDelete applied to each resource group
C) Azure Policy with a 'deny' effect requiring the CostCenter tag
D) A Microsoft Entra administrative unit scoped to the resource groups

---

**Q3.** An administrator assigns an Azure Policy definition with a 'DeployIfNotExists' effect to enable diagnostic settings on all storage accounts in a subscription. After assignment, 40 pre-existing storage accounts remain non-compliant. What must the administrator do to bring these existing resources into compliance?

A) Change the policy effect to 'Deny' and reassign the policy
B) Create and run a remediation task for the policy assignment
C) Manually enable diagnostic settings on each of the 40 storage accounts
D) Wait 24 hours for the next policy compliance scan to automatically fix the resources

---

**Q4.** A production virtual machine must never be accidentally deleted, but administrators still need to resize the VM and modify its NIC configuration as operational needs change. Which configuration should be applied?

A) A ReadOnly lock on the virtual machine
B) A CanNotDelete lock on the virtual machine
C) An Azure Policy assignment with a 'Deny' effect on delete operations
D) Assign the RBAC Reader role to all administrators on the VM

---

**Q5.** An administrator creates a custom Azure RBAC role definition with AssignableScopes set to a single resource group: '/subscriptions/xxxx/resourceGroups/RG-Prod'. What is true about where this custom role can be assigned?

A) It can be assigned at any scope within the subscription, including other resource groups
B) It can only be assigned at RG-Prod or at resources within RG-Prod, not at the subscription or management group level
C) It can be assigned at the management group level immediately after creation
D) It automatically applies to all resource groups named 'RG-Prod' across every subscription in the tenant

---

**Q6.** A finance team wants to receive an automated email notification when a subscription's actual monthly spending reaches 80% of an allocated $10,000 budget, without blocking or altering any resources. Which Azure feature should be configured?

A) Azure Policy with an audit effect on cost thresholds
B) A resource lock set to ReadOnly triggered at 80% utilization
C) An Azure Budget with a cost alert condition set to 80% of the amount
D) Azure Advisor cost recommendations

---

**Q7.** Contoso Ltd. wants an IT helpdesk employee, Priya, to be able to reset passwords and manage licenses only for the 500 users in the Sales department in Microsoft Entra ID. Priya must not be able to view or manage any users outside Sales. The Global Administrator wants the least-privilege solution that scales as Sales employees are added or removed. Which solution BEST meets these requirements?

A) Create an administrative unit containing the Sales department users and assign Priya the Helpdesk Administrator role scoped to that administrative unit
B) Assign Priya the Global Administrator role and instruct her to only modify Sales users
C) Create a custom Azure RBAC role with Microsoft.Graph permissions and assign it at the resource group scope
D) Add Priya to the User Administrator role at the tenant (directory) scope

---

**Q8.** An Azure administrator needs to allow the 'Ops-OnCall' Microsoft Entra group to start and restart virtual machines in the 'rg-prod' resource group during incidents, but the group must NOT be able to create, delete, or resize any virtual machines. No built-in role matches this exact requirement. What should the administrator do?

A) Assign the built-in Reader role to the Ops-OnCall group at the rg-prod scope
B) Assign the built-in Virtual Machine Contributor role to the Ops-OnCall group at the rg-prod scope
C) Create a custom RBAC role granting only Microsoft.Compute/virtualMachines/start/action and restart/action (plus read), then assign it to Ops-OnCall at the rg-prod scope
D) Assign the Ops-OnCall group the Contributor role at the subscription scope

---

**Q9.** An administrator assigns an Azure Policy definition with a 'Modify' effect and a system-assigned managed identity to automatically add the tag CostCenter=IT to all newly created storage accounts in a subscription. After the assignment, the administrator notices that storage accounts created BEFORE the policy assignment still do not have the CostCenter tag. What should the administrator do to bring the existing non-compliant resources into compliance?

A) Change the policy effect from 'Modify' to 'Deny' so existing resources are automatically updated
B) Apply a resource lock of type CanNotDelete to the non-compliant storage accounts
C) Wait 24 hours for the policy compliance scan to automatically add the tag without any further action
D) Create and run a remediation task against the policy assignment to apply the Modify effect to existing non-compliant resources

---

**Q10.** Which statement correctly differentiates Azure RBAC from Azure Policy?

A) Azure Policy grants or denies specific management actions to a security principal, while RBAC evaluates whether a resource's configuration is compliant with organizational rules
B) RBAC and Azure Policy both function identically, granting access permissions that can be assigned at management group, subscription, resource group, or resource scope
C) Azure Policy is only used to grant read-only access to management groups, while RBAC is used exclusively to enforce naming conventions and tags
D) Azure RBAC controls what actions a security principal can perform on Azure resources, while Azure Policy evaluates and enforces the properties/configuration of resources regardless of who created them

---

**Q11.** A company runs a mission-critical application that must remain available if an entire datacenter within the primary region fails, and must also allow read access to data from a secondary region if the primary region becomes completely unavailable. Which storage redundancy option BEST meets these requirements?

A) LRS
B) RA-GZRS
C) ZRS
D) GRS

---

**Q12.** A media company stores raw video footage that is accessed frequently for editing during the first 30 days after upload, rarely accessed afterward, and must be retained for compliance after one year with access latency of several hours being acceptable. Which lifecycle management tier progression BEST meets these requirements?

A) Cool tier for first 30 days, then Hot, then delete after 1 year
B) Hot tier for first 30 days, then Cool tier, then Archive tier after 1 year
C) Hot tier permanently for the entire lifecycle
D) Archive tier immediately, rehydrate to Hot after 30 days

---

**Q13.** An administrator needs to grant a third-party application temporary write access to a specific blob container for 24 hours, without exposing the storage account key and without granting access to other containers in the account. Which mechanism should be used?

A) Create a Service SAS scoped to the specific container with a 24-hour expiry
B) Grant access using the storage account key directly
C) Create an Account SAS scoped to all blob services
D) Enable public read access at the container level

---

**Q14.** A storage account must only be accessible from resources within a specific virtual network subnet, public internet access must be denied by default, and trusted Azure services such as Azure Backup must still be able to access the account. Which combination of storage account network settings should be configured?

A) Set default network action to Allow and add IP firewall rules for the corporate network
B) Set default network action to Deny, add a VNet service endpoint for the subnet, and enable the 'Allow trusted Microsoft services' exception
C) Disable the storage firewall entirely and rely on SAS tokens
D) Set default network action to Deny and add only IP address rules for on-premises addresses

---

**Q15.** Which of the following is a strict requirement for enabling Azure Blob object replication between a source and destination storage account?

A) Blob versioning must be enabled on both the source and destination accounts, and change feed must be enabled on the source account
B) Both accounts must use Locally Redundant Storage (LRS)
C) Both storage accounts must be located in the same Azure region
D) Both accounts must have hierarchical namespace (Data Lake Storage Gen2) enabled

---

**Q16.** A company has a file server in an on-premises branch office that needs a local cached copy of frequently accessed files for low-latency access, while the complete data set is centrally stored and managed in Azure. Files that are not accessed recently should automatically be tiered to Azure to conserve local disk space. Which solution should be implemented?

A) Azure Files with SMB Multichannel enabled
B) AzCopy configured as a scheduled task
C) Azure File Sync with cloud tiering enabled on the server endpoint
D) Azure Data Box for one-time data transfer

---

**Q17.** A company grants a third-party vendor read and write access to blobs in a single container named 'vendor-uploads' for the next 30 days. The security team requires the ability to immediately revoke the vendor's access at any time before expiration without rotating the storage account access keys. Which solution BEST meets these requirements?

A) Generate an account SAS scoped to the Blob service with a 30-day expiry and share it with the vendor
B) Share one of the storage account access keys directly with the vendor and rotate it after 30 days
C) Create a stored access policy on the 'vendor-uploads' container and generate a service SAS that references the stored access policy
D) Assign the vendor's Microsoft Entra identity the Storage Blob Data Contributor role scoped to the container

---

**Q18.** An administrator configures a storage account's networking settings to 'Selected networks' and adds a specific virtual network subnet, denying all public internet traffic. The company also uses Azure Backup, which needs to write backup data to this storage account without being explicitly added as a subnet. What should the administrator configure to allow this?

A) Create a private endpoint for the storage account and connect it to the Azure Backup vault's virtual network
B) Set the storage account networking rule back to 'Allow access from all networks'
C) Enable the 'Allow trusted Microsoft services to access this storage account' exception under the storage account firewall settings
D) Add the public IP address range of the Azure Backup service to the storage account's IP firewall rules

---

**Q19.** A company runs a two-tier web application on two Azure VMs. The finance team requires the solution to meet a 99.99% uptime SLA in the event of a datacenter-level failure. Which configuration meets this requirement?

A) Place both VMs in the same Availability Set with two fault domains
B) Deploy each VM into a different Availability Zone within the same region
C) Deploy both VMs in the same Availability Zone using Premium SSD disks
D) Deploy a single VM and configure Azure Site Recovery for failover

---

**Q20.** A development team needs to run a single containerized batch job that executes for about 3 minutes, requires no orchestration, has no persistent state, and should be billed only for the seconds it actually runs. Which Azure service is the BEST fit?

A) Azure Kubernetes Service (AKS)
B) Azure App Service for Containers
C) Azure Container Apps
D) Azure Container Instances (ACI)

---

**Q21.** In an Azure Virtual Machine Scale Set autoscale setting, which setting controls how long Autoscale waits after a scaling action completes before it evaluates the rules again?

A) Time grain
B) Cooldown period
C) Scale-out threshold
D) Aggregation type

---

**Q22.** A team wants to deploy a new version of their Azure App Service web app with zero downtime and the ability to validate the new version under production-like conditions before it becomes fully live. Which approach should they use?

A) Deploy directly to the production slot during a scheduled maintenance window
B) Scale the App Service plan to a higher pricing tier before deploying
C) Deploy to a staging deployment slot, warm it up, then swap it with production
D) Enable CPU-based autoscale rules on the App Service plan before deploying

---

**Q23.** A company must ensure that all data on Azure VM OS disks, data disks, and temporary disks — including the disk caches — is encrypted using platform-managed keys, without installing any encryption agent inside the guest OS. Which feature should they enable?

A) Azure Disk Encryption (ADE) with BitLocker
B) Storage Service Encryption (SSE) for managed disks only
C) Azure Backup with Soft Delete
D) Encryption at Host

---

**Q24.** Which statement correctly describes how Azure processes a Bicep file during deployment?

A) Bicep files are transpiled into ARM JSON templates, which Azure Resource Manager then deploys
B) Azure Resource Manager natively parses and executes Bicep syntax without any conversion
C) Bicep replaces Azure Resource Manager entirely as the deployment engine
D) Bicep files must first be converted to Terraform HCL before they can be deployed

---

**Q25.** A company wants to deploy a Virtual Machine Scale Set where individual VMs can use different VM sizes and disk types, can mix Azure Spot and standard priority VMs in the same set, and each instance is individually addressable via Azure CLI similar to a standalone VM. Which orchestration mode should they choose?

A) Uniform orchestration mode
B) An availability set with manual scaling scripts
C) Flexible orchestration mode
D) An AKS node pool with cluster autoscaler

---

**Q26.** A development team needs to run several stateless HTTP-triggered microservices that automatically scale to zero instances when idle, without provisioning or managing an underlying Kubernetes cluster. Which Azure service best meets this requirement?

A) Azure Container Apps
B) Azure Container Instances
C) Azure Kubernetes Service (AKS)
D) Azure Container Registry

---

**Q27.** An App Service app has an app setting named 'ConnectionString' marked as a slot setting (sticky) in both the staging slot (pointing to a test database) and the production slot (pointing to the production database). After you swap the staging slot into production, which connection string will the resulting production slot use?

A) The connection string from staging, pointing to the test database
B) A merged connection string combining both the staging and production values
C) No connection string is available, causing the app to fail to start
D) The connection string that was previously configured in production, pointing to the production database

---

**Q28.** Which statement about encryption of Azure Managed Disks is correct?

A) Azure Disk Encryption (ADE) is automatically enabled by default on every newly created managed disk
B) Server-side encryption (SSE) with platform-managed keys is enabled by default on all managed disks at no additional cost
C) Server-side encryption can only be used if you configure customer-managed keys in Azure Key Vault
D) Managed disks remain unencrypted unless a VM extension is manually installed on the virtual machine

---

**Q29.** VNet-A is peered with VNet-B, and VNet-B is peered with VNet-C. VNet-A is NOT peered with VNet-C. A VM in VNet-A needs to communicate directly with a VM in VNet-C using private IP addresses. What should you do?

A) Create a direct VNet peering connection between VNet-A and VNet-C
B) Do nothing — VNet peering is transitive, so VNet-A can already reach VNet-C through VNet-B
C) Deploy a VPN Gateway in VNet-B and configure gateway transit for VNet-A and VNet-C
D) Add a user-defined route in VNet-A pointing traffic for VNet-C's address space to the VNet-B gateway

---

**Q30.** You create an Azure Private DNS zone named contoso.internal and add an A record for a VM. VMs in VNet1 still cannot resolve contoso.internal names, even though they use the default Azure-provided DNS. What is the most likely cause?

A) Private DNS zones require a custom DNS server IP to be manually configured on each VM
B) The A record TTL is too high and has not expired yet
C) The private DNS zone has not been linked to VNet1 via a virtual network link
D) Private DNS zones only work with VNets that have a VPN Gateway attached

---

**Q31.** Which statement correctly describes an Azure Application Security Group (ASG)?

A) An ASG independently filters inbound and outbound traffic without needing an NSG
B) An ASG logically groups VM network interfaces so they can be used as the source or destination in NSG security rules
C) An ASG can be assigned directly as a rule target on a subnet in place of an NSG
D) An ASG replaces the need for NSGs by providing application-layer (Layer 7) filtering

---

**Q32.** You configure a health probe on an Azure Standard Load Balancer backend pool using TCP on port 80, with an Interval of 5 seconds and an Unhealthy Threshold of 2 consecutive failures. Approximately how long after an instance stops responding will the Load Balancer mark it unhealthy and stop sending it new traffic?

A) 5 seconds
B) 10 seconds
C) 15 seconds
D) 20 seconds

---

**Q33.** A web application uses two backend server pools: one serving requests for /images and another for /api. All traffic must be SSL-terminated and inspected for OWASP Top 10 vulnerabilities such as SQL injection before reaching the backends. Which Azure service should you deploy?

A) Application Gateway with Web Application Firewall (WAF_v2 tier)
B) Azure Load Balancer (Standard SKU)
C) Azure Firewall
D) Traffic Manager

---

**Q34.** A company requires that all traffic from a VNet to an Azure SQL Database use a private IP address from within the VNet's own address space, ensuring the database is not reachable via any public endpoint at all. Which solution meets this requirement?

A) Configure a Service Endpoint for Microsoft.Sql on the subnet
B) Add an NSG rule on the subnet that denies all inbound internet traffic
C) Deploy a Private Endpoint for the Azure SQL Database and disable the public network access setting
D) Configure a User-Defined Route sending 0.0.0.0/0 traffic to the SQL server's public IP

---

**Q35.** A company hosts a web application on a set of Azure VMs in a backend pool. Requirements: terminate SSL/TLS at the network layer, route traffic based on URL path (e.g., /images to one pool, /api to another), and provide layer 7 load balancing. Which service should the administrator deploy?

A) Azure Load Balancer (Standard SKU) with a single backend pool
B) Azure Traffic Manager with priority routing
C) Network Security Group with application security groups
D) Azure Application Gateway with path-based routing rules

---

**Q36.** A company needs VMs in a VNet to connect to an Azure SQL Database using a private IP address from the VNet's address space. The connection must not traverse the public internet at any point, and the SQL Database must remain completely inaccessible from any public endpoint, including other Azure services. Which solution meets these requirements?

A) Deploy a Private Endpoint for the SQL Database and disable public network access
B) Configure a Service Endpoint for Microsoft.Sql on the subnet
C) Configure a User-Defined Route to force traffic through a virtual appliance
D) Establish a Site-to-Site VPN Gateway connection to the SQL Database

---

**Q37.** A company requires an RPO of under 5 minutes and an RTO of under 15 minutes for its production VMs in the event of a regional outage. Which solution BEST meets this requirement?

A) Azure Backup configured with a daily backup policy
B) A Recovery Services vault snapshot with weekly retention
C) Azure Backup using an enhanced policy that takes backups every 4 hours
D) Azure Site Recovery replicating the VMs to a secondary Azure region

---

**Q38.** A VM in Azure cannot reach a specific external website. You need to test the actual network path and pinpoint whether an NSG rule, user-defined route, or other configuration is blocking the connection. Which Network Watcher tool should you use?

A) Network Watcher Connection Troubleshoot
B) Network Watcher IP Flow Verify
C) Azure Monitor Network Diagnostics
D) NSG flow logs

---

**Q39.** You need to be notified by email and have a Logic App triggered whenever CPU usage on a VM exceeds 80% for 5 consecutive minutes. Which configuration meets this requirement?

A) Create a Log Analytics scheduled query alert that runs once per day
B) Configure an Application Insights availability test on the VM
C) Configure an Azure Service Health alert for the subscription
D) Create a metric alert rule with a threshold condition of CPU > 80% over a 5-minute window, tied to an action group containing an email and Logic App action

---

**Q40.** You need to configure an Azure Backup policy for a VM that retains daily backup points for 30 days, and additionally keeps one backup per week for 12 weeks. Which approach correctly implements this?

A) Configure a single backup policy with a daily schedule and a 30-day daily retention range, plus a weekly retention range of 12 weeks selecting one of the daily backup points
B) Set the daily retention range to 30 days only, and no weekly retention is needed
C) Enable Cross Region Restore on the vault and set retention to 30 days
D) Create two separate backup policies — one daily and one weekly — and assign both to the VM

---

**Q41.** What is the primary difference between Azure Monitor Metrics and Azure Monitor Logs?

A) Metrics store lightweight numerical time-series data optimized for near real-time analysis, while Logs store structured and unstructured data queried using KQL for deeper analysis
B) Metrics require a Log Analytics workspace to store data, while Logs do not
C) Logs only capture VM performance counters, while Metrics capture application traces
D) Metrics data is retained indefinitely, while Logs data always expires after 93 days

---

**Q42.** You are using Azure Site Recovery to protect on-premises Hyper-V VMs by replicating them to Azure. You want to validate that failover will work correctly without impacting ongoing replication or production workloads. Which ASR feature should you use?

A) Planned Failover
B) Unplanned Failover
C) Failback
D) Test Failover

---

