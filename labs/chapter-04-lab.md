# Chapter 4 Lab: Storage Accounts: Redundancy, Tiers, and Secure Access

**Estimated time:** 25 minutes

## Exercise

Use Azure CLI to create a storage account with GZRS redundancy (az storage account create --sku Standard_GZRS), then generate a service SAS scoped to a single container with az storage container generate-sas restricted to read-only, 2-hour expiry.

## Key takeaway

Every AZ-104 storage scenario reduces to matching redundancy, tier, and access mechanism to stated availability, cost, and security requirements — memorize the tradeoffs, not just the names.
