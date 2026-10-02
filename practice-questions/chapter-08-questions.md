## Chapter 8: Containers and Azure App Service — Practice Questions

**Q1.** A company runs a nightly data-cleanup process that starts, runs for about 8 minutes, and then exits. There is no need for orchestration, scaling, or persistent endpoints. Which service is the MOST cost-effective choice?

A) Azure Container Apps with min replicas set to 0
B) App Service Plan (Premium tier) running a container
C) Azure Kubernetes Service with a CronJob
D) Azure Container Instances

<details>
<summary>Answer</summary>

**Correct: D**

ACI bills per second for exactly the compute consumed and requires no cluster, orchestration, or plan — ideal for short-lived, single-container batch jobs.

**Why the others are wrong:**
- Container Apps adds KEDA/Envoy overhead and is built for long-running or event-driven apps, not simple short batch jobs — more complex than needed.
- App Service Plan bills continuously per hour for the plan regardless of whether the container is running, making it far more expensive for an 8-minute job.
- AKS requires managing a cluster (nodes billed continuously) — massive overkill and cost for a single nightly task.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team is building a microservices application that must automatically scale out based on the length of an Azure Service Bus queue and scale to zero instances when the queue is empty. Which service should they use?

A) Azure Container Apps
B) Azure Container Instances
C) App Service Plan Standard tier with autoscale rules
D) Azure Container Registry Tasks

<details>
<summary>Answer</summary>

**Correct: A**

Azure Container Apps uses KEDA under the hood, natively supporting event-driven scalers (including Service Bus queue length) and scale-to-zero.

**Why the others are wrong:**
- ACI has no built-in autoscaling or event-driven scaling — you'd manage instances manually.
- App Service autoscale only reacts to metrics like CPU/memory/HTTP queue length, not custom KEDA scalers like Service Bus queue depth, and cannot scale to zero.
- ACR Tasks is for building/pushing container images, not running or scaling workloads.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A web application requires a staging slot for pre-production testing, the ability to swap staging into production with zero downtime, and a custom domain with a TLS/SSL certificate binding. Which service and minimum tier meets all requirements?

A) Azure Container Instances with a public IP
B) App Service Plan, Standard tier or higher
C) App Service Plan, Free tier
D) Azure Container Apps with two revisions

<details>
<summary>Answer</summary>

**Correct: B**

Deployment slots require Standard tier or higher (5 slots) and Standard tier also supports custom domain TLS/SSL bindings.

**Why the others are wrong:**
- ACI has no concept of deployment slots or slot swapping.
- Free tier does not support deployment slots or TLS/SSL bindings on a custom domain.
- Container Apps revisions support traffic splitting, but the scenario explicitly requires App Service deployment slot swap behavior and custom domain SSL binding, which are App Service features.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company needs a private container registry that supports geo-replication across three Azure regions to reduce pull latency for globally distributed deployments. Which Azure Container Registry SKU is required?

A) Basic
B) Standard
C) Classic
D) Premium

<details>
<summary>Answer</summary>

**Correct: D**

Geo-replication is only available on the Premium ACR SKU, which also provides the largest included storage and higher throughput.

**Why the others are wrong:**
- Basic offers limited storage and throughput and does not support geo-replication.
- Standard offers more storage/throughput than Basic but still lacks geo-replication.
- Classic is not a valid current ACR SKU option.

</details>

---

**Q5.** Which is the minimum App Service Plan tier that supports rule-based autoscale (scale based on CPU or other metrics)?

A) Free (F1)
B) Basic (B1-B3)
C) Standard (S1-S3)
D) Isolated (I1-I3)

<details>
<summary>Answer</summary>

**Correct: C**

Standard tier is the minimum tier that supports autoscale rules; Basic only allows manual scale-out to a maximum of 3 instances.

**Why the others are wrong:**
- Free tier runs on shared infrastructure with a single instance and no scale-out at all.
- Basic supports manual scaling to up to 3 instances only, not autoscale.
- Isolated does support autoscale, but it is not the MINIMUM tier — Standard already provides this capability.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An administrator swaps a staging slot into production and discovers the connection string still points to the staging database instead of production. What should have been configured before the swap?

A) Mark the connection string as a 'Deployment slot setting' (slot-sticky)
B) Set the connection string as an app setting instead of a connection string
C) Disable Always On for the staging slot
D) Enable auto-swap on the production slot

<details>
<summary>Answer</summary>

**Correct: A**

Marking a setting as a deployment slot setting makes it slot-sticky, meaning it stays attached to the slot (e.g., staging) rather than moving during a swap — this is exactly how you keep staging pointed to its own database.

**Why the others are wrong:**
- Changing type to app setting does not affect whether it swaps unless it's also marked slot-sticky.
- Always On controls whether the app stays loaded in memory; it has no effect on which settings swap.
- Auto-swap automatically triggers a swap after deployment — it does not control which values are sticky.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** How many total deployment slots (including the production slot) does the Standard App Service Plan tier support?

A) 3
B) 10
C) 5
D) 20

<details>
<summary>Answer</summary>

**Correct: C**

Standard tier supports 5 total slots including production. Premium and higher tiers support 20 total slots.

**Why the others are wrong:**
- 3 is not a slot limit for any tier — it is the max manual scale-out instance count for Basic tier.
- 10 is the max autoscale instance count for Standard tier, not the slot count.
- 20 is the slot count for Premium and Isolated tiers, not Standard.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the fundamental difference between manual scaling and autoscale in an Azure App Service Plan?

A) Manual scaling changes the VM size (scale up); autoscale only changes instance count (scale out)
B) Manual scaling sets a fixed instance count set by an admin; autoscale adjusts instance count automatically based on defined rules and metrics
C) Manual scaling is only available in Premium tier; autoscale is available in all tiers
D) Manual scaling applies to Linux plans only; autoscale applies to Windows plans only

<details>
<summary>Answer</summary>

**Correct: B**

Manual scaling means the administrator explicitly sets a static instance count; autoscale uses rules (based on metrics like CPU, memory, or schedules) to add/remove instances automatically within a defined range.

**Why the others are wrong:**
- Scaling up/down (changing VM size/tier) is a separate concept from scale-out; this option conflates scale up with manual scaling incorrectly.
- Manual scale-out is available starting at Basic tier, not just Premium, and autoscale is not available in every tier (not Free/Shared/Basic).
- Both manual scaling and autoscale work on both Windows and Linux App Service plans — OS is not the differentiator.

</details>

---

