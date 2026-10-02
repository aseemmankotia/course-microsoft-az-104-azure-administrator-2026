## Chapter 11 Cheat Sheet: Monitoring, Backup, and Site Recovery

### Metrics vs Logs
| Feature | Azure Monitor Metrics | Log Analytics Logs |
|---|---|---|
| Data type | Numeric time series | Structured records (KQL) |
| Latency | Near real-time | Minutes (ingestion delay) |
| Retention | 93 days | 30 days default, up to 730 days |
| Best for | Fast threshold alerts | Correlation, deep analysis |

### Alerts & Action Groups
- **Alert types:** Metric (near real-time, static/dynamic threshold), Log (scheduled KQL query), Activity Log, Service Health.
- **Action groups:** reusable notification/action sets — email, SMS (throttled to 1/5 min per number), voice, webhook, Azure Function, Logic App, ITSM.
- **Severity:** Sev0 (critical) → Sev4 (verbose).

### KQL Basics
```kql
TableName
| where TimeGenerated > ago(1h)
| summarize count() by bin(TimeGenerated, 5m)
| order by TimeGenerated desc
```
- Pipe `|` chains operators. `where` filters, `summarize...by` aggregates, `bin()` buckets time.
- No `group by` — that's SQL, not KQL.

### Application Insights
- Auto-instrumentation for app telemetry: requests, dependencies, exceptions.
- **Live Metrics:** ~1 second latency, for real-time app health.
- **Availability tests:** URL ping / multi-step tests from global points.

### Network Watcher
| Tool | Purpose |
|---|---|
| Connection Troubleshoot | Test connectivity, latency, hop-by-hop path |
| IP Flow Verify | Check if NSG rule allows/denies specific traffic |
| NSG Flow Logs (v2) | Log allowed/denied traffic per NSG; feed to Traffic Analytics (requires Log Analytics workspace) — being replaced by VNet Flow Logs |

### Azure Service Health
- **Service issues** – active Azure problems.
- **Planned maintenance** – upcoming changes.
- **Health advisories** – service changes/deprecations.
- **Security advisories** – security-related notices.
- Configure alerts via Action Groups for proactive notification.

### Backup vs Site Recovery
| | Azure Backup | Azure Site Recovery |
|---|---|---|
| Purpose | Data protection (restore) | Disaster recovery (failover) |
| Container | Recovery Services vault | Recovery Services vault |
| Key metric | Retention policy (daily/weekly/monthly/yearly) | RPO / RTO |
| Instant restore | Default 2 days (range 1-5) | N/A |
| Soft delete | 14 days (mandatory) | N/A |

### RPO/RTO Quick Rules
- **RPO** = how much data you can afford to lose (time since last recovery point).
- **RTO** = how long you can be down before failover completes.
- ASR for Azure VM-to-VM: crash-consistent replication continuously; app-consistent snapshot frequency is configurable (e.g., every 1-24 hours).

### Exam Traps
- Confusing Metrics retention (93 days) with Logs retention (30 days default).
- Assuming Backup provides regional failover — it does not; that's ASR.
- Forgetting NSG Flow Logs need a Log Analytics workspace for Traffic Analytics visuals (storage account alone only stores raw JSON).
- Thinking soft delete and instant restore are the same feature — they are not.
