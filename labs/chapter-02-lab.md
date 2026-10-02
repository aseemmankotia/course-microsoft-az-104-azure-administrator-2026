# Chapter 2 Lab: Azure RBAC: Roles, Scopes, and Assignments

**Estimated time:** 20 minutes

## Exercise

Use Azure CLI to run az role assignment create to grant Contributor at a resource group scope, then create a custom role from a JSON file with az role definition create that allows starting/restarting VMs but not deleting them.

## Key takeaway

Azure RBAC controls who can do what to Azure resources at a chosen scope, and that scope always inherits downward — never confuse it with Azure Policy, which controls resource configuration compliance.
