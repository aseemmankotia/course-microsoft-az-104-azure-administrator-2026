## Chapter 8: Containers and Azure App Service — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Azure Container Instances default max vCPU/memory per Linux container group? | 4 vCPU / 16 GB memory (default, without a support request increase). Exam tip: ACI has no built-in autoscaling or orchestration — it's for single or simple multi-container groups. |
| 2 | Standard App Service Plan tier: max deployment slots (including production)? | 5 total slots. Premium and Isolated tiers support 20 total slots. Exam tip: Basic tier supports NO deployment slots. |
| 3 | Standard tier App Service Plan: max autoscale instance count? | 10 instances. Premium tier autoscale max is 30 instances. Exam tip: Basic tier only supports MANUAL scale-out, up to 3 instances (no autoscale rules). |
| 4 | Basic App Service Plan tier: manual scale-out limit? | Up to 3 instances, manual only — no autoscale rules supported at this tier. |
| 5 | ACI vs Container Apps vs App Service for Containers — when to use each? | ACI: single/simple container groups, short-lived or burst jobs, billed per second, no scaling. Container Apps: microservices needing KEDA event-driven autoscaling, scale-to-zero, Dapr, revisions/traffic-split. App Service: web apps needing deployment slots, custom domains/TLS, easy auth, VNet integration. |
| 6 | ACR SKU differences: Basic vs Standard vs Premium? | Basic: least storage/throughput. Standard: more storage/throughput than Basic. Premium: highest storage/throughput PLUS geo-replication and content trust support. Exam tip: geo-replication = Premium only. |
| 7 | az CLI command to swap a deployment slot into production? | az webapp deployment slot swap --resource-group <rg> --name <app> --slot staging --target-slot production |
| 8 | az CLI command to build an image using ACR Tasks (cloud build, no local Docker needed)? | az acr build --registry <registryName> --image myapp:v1 . |
| 9 | az CLI command to create a Premium-tier Container Registry? | az acr create --name <registryName> --resource-group <rg> --sku Premium |
| 10 | What settings are 'slot-sticky' and do NOT move during a deployment slot swap? | Custom domain names, TLS/SSL certificate bindings, scale settings, IP restrictions, WebJobs schedulers, Always On, VNet integration, managed identities, and any app setting/connection string explicitly marked as 'Deployment slot setting.' |
| 11 | How do Container Apps revisions support blue/green deployments? | Each deployment creates a new revision; traffic can be split by percentage between the old and new revision (e.g., 90/10), allowing gradual rollout before shifting 100% traffic to the new revision. |
| 12 | What are the key limitations of the Free (F1) and Shared (D1) App Service tiers? | No deployment slots, no autoscale, no custom domain TLS/SSL binding, single shared-compute instance, CPU quota limits per day. Exam tip: use for dev/test only, never for production workloads requiring scale or SSL. |
