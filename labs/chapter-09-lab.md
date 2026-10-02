# Chapter 9 Lab: Virtual Networks, DNS, and Network Security

**Estimated time:** 25 minutes

## Exercise

Create two virtual networks and peer them using az network vnet peering create, deploy an NSG with a custom rule allowing HTTPS inbound only from a specific application security group, then deploy Azure Bastion in one VNet to securely connect to a VM with no public IP.

## Key takeaway

Network segmentation and security in Azure is built from VNets, peering, NSGs, and ASGs together — know exactly what each layer does and does not provide before reaching for Azure Firewall.
