# Chapter 7 Lab: ARM Templates, Bicep, and Scale Sets with Autoscale

**Estimated time:** 25 minutes

## Exercise

Write a Bicep file that defines a VM Scale Set with an autoscale rule that scales out when average CPU exceeds 70% and scales in below 30%, then deploy it with az deployment group create --template-file.

## Key takeaway

Infrastructure-as-code and autoscale are tested together — know exactly what Complete mode deletes and what metric-based rules trigger scale-out versus scale-in.
