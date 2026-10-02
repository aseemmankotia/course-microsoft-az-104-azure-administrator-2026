## Chapter 11: Monitoring, Backup, and Site Recovery — Practice Questions

**Q1.** A company wants an alert fired within 1 minute when any VM's CPU exceeds 90%, and also needs to run complex correlation queries across CPU, disk, and application logs for the past 30 days. Which combination of tools BEST meets both requirements?

A) Use Log Analytics alerts for both the CPU threshold and the correlation queries
B) Use Application Insights Live Metrics for both requirements
C) Use Network Watcher Connection Troubleshoot for the CPU threshold and Metrics Explorer for the correlation queries
D) Use an Azure Monitor Metrics alert for the CPU threshold and Log Analytics (KQL) for the correlation queries

<details>
<summary>Answer</summary>

**Correct: D**

Metrics alerts evaluate near real-time numeric time-series data with sub-minute latency — ideal for CPU thresholds. Log Analytics stores detailed records queryable with KQL, suited for multi-source correlation over time.

**Why the others are wrong:**
- Log alerts run on a schedule (minimum 1-5 min evaluation frequency plus ingestion latency) and are not truly near real-time for a 1-minute CPU alert
- Application Insights is for application telemetry, not VM CPU or cross-source infrastructure correlation
- Network Watcher tests connectivity, not CPU thresholds

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A company needs to protect its Azure VMs against a full regional outage by replicating them to a secondary Azure region so they can be failed over with an RTO measured in minutes. Which service should they deploy?

A) Azure Backup
B) Geo-redundant storage (GRS) on the VM disks
C) Azure Site Recovery
D) Azure Traffic Manager

<details>
<summary>Answer</summary>

**Correct: C**

Azure Site Recovery replicates VMs to a secondary region and orchestrates failover, meeting disaster recovery RPO/RTO objectives.

**Why the others are wrong:**
- Azure Backup restores point-in-time data but does not provide continuous replication or fast regional failover
- GRS replicates storage account data asynchronously but doesn't orchestrate VM failover or maintain application consistency
- Traffic Manager routes traffic but does not replicate or fail over compute resources

</details>

---

**Q3.** Which service must NSG Flow Logs be linked to in order to generate Traffic Analytics visualizations?

A) A storage account only
B) A Log Analytics workspace
C) Application Insights
D) Azure Monitor Metrics namespace

<details>
<summary>Answer</summary>

**Correct: B**

Traffic Analytics processes NSG flow log data and requires a Log Analytics workspace to store and visualize the processed traffic patterns.

**Why the others are wrong:**
- A storage account is required to store the raw flow log JSON, but Traffic Analytics itself needs a Log Analytics workspace to render insights
- Application Insights is for application telemetry, not network flow data
- Metrics namespaces store numeric time series, not flow log records

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An administrator configures an alert rule that must send an SMS to the on-call engineer, an email to the team, and trigger an Azure Function for auto-remediation when it fires. Which resource should be attached to the alert rule to achieve this?

A) An action group
B) A diagnostic setting
C) A Log Analytics saved search
D) A Recovery Services vault

<details>
<summary>Answer</summary>

**Correct: A**

Action groups define a reusable set of notification and automated actions (SMS, email, Function, Logic App, webhook, etc.) that alert rules invoke when triggered.

**Why the others are wrong:**
- Diagnostic settings route resource logs/metrics to destinations like Log Analytics; they don't send notifications
- Saved searches store KQL queries for reuse, not notification logic
- Recovery Services vaults manage backup and ASR, unrelated to alert notifications

</details>

---

**Q5.** Which KQL query correctly returns the count of Heartbeat events grouped into 5-minute intervals over the last hour?

A) Heartbeat | where TimeGenerated > ago(1h) | summarize count() by bin(TimeGenerated, 5m)
B) Heartbeat | group by bin(TimeGenerated, 5m) | where TimeGenerated > ago(1h) | count()
C) Heartbeat | summarize count() | where TimeGenerated > ago(1h) by bin(TimeGenerated, 5m)
D) Heartbeat | filter TimeGenerated > ago(1h) | count() by bin(TimeGenerated, 5m)

<details>
<summary>Answer</summary>

**Correct: A**

Correct KQL pipeline order: filter first with 'where', then aggregate with 'summarize ... by bin(...)'. This is the standard time-bucketing pattern.

**Why the others are wrong:**
- KQL has no 'group by' clause — that's SQL syntax
- 'where' cannot appear after 'summarize' in that position, and 'by' must follow the aggregation function, not the filter
- 'filter' is not a native KQL operator (the correct operator is 'where'), and syntax order is invalid

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** What is the fundamental difference between Azure Monitor Metrics and Log Analytics logs?

A) Metrics are lightweight numeric time-series data with near real-time evaluation; logs are structured records queried via KQL with some ingestion latency
B) Metrics are stored indefinitely while logs expire after 30 days with no option to extend
C) Metrics require a Log Analytics workspace while logs do not require any storage
D) Metrics can only be viewed in Application Insights while logs can only be viewed in Azure Monitor

<details>
<summary>Answer</summary>

**Correct: A**

Metrics are optimized for fast, near real-time numeric alerting (up to 93 days retention). Logs are text/record-based, ingested with a short delay, and queried with KQL for deep analysis.

**Why the others are wrong:**
- Metrics have a 93-day retention limit in Metrics Explorer, not indefinite; log retention is configurable up to 730 days interactive
- Metrics do not require a Log Analytics workspace — they use the Azure Monitor metrics database
- Both metrics and logs can be viewed in Azure Monitor; Application Insights is only one metrics/log source

</details>

---

**Q7.** A company enabled instant restore for its Azure VM backup policy but did not change the default setting. For how many days are instant restore snapshots retained by default?

A) 1 day
B) 2 days
C) 7 days
D) 30 days

<details>
<summary>Answer</summary>

**Correct: B**

The default instant restore snapshot retention for Azure VM backup is 2 days, configurable in a range of 1-5 days.

**Why the others are wrong:**
- 1 day is the minimum configurable value, not the default
- 7 days exceeds the maximum allowed range (1-5 days) for instant restore snapshots
- 30 days is far beyond the instant restore snapshot window; that duration applies to recovery point retention policies, not snapshots

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A backup administrator accidentally deletes a backup item from a Recovery Services vault with soft delete enabled. How long will the backup data be retained before it is permanently deleted?

A) 7 days
B) 30 days
C) 14 days
D) 90 days

<details>
<summary>Answer</summary>

**Correct: C**

Recovery Services vault soft delete (now mandatory for Azure Backup) retains deleted backup data for 14 days, allowing recovery from accidental or malicious deletion.

**Why the others are wrong:**
- 7 days is shorter than the actual documented soft-delete window
- 30 days is not the soft-delete retention period for Recovery Services vaults
- 90 days is not correct for backup soft delete; it's sometimes confused with other Azure soft-delete features

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

