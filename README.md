# azure-glitch-sim

## SNAT Glitch on AKS

This repository contains a sample application that demonstrates how a bad code practice can cause SNAT issues on Azure Kubernetes Service (AKS). The application is designed to simulate a scenario where a client makes multiple requests to a service, and the service experiences a SNAT glitch.

## Bad Async Pattern Sample

The repository contains a sample application that demonstrates a bad async pattern. The application is designed to leave some operations running in the background (call to log) and cause possible failures in the main thread. This is a bad practice and should be avoided in production code.

## Use of AZAPI

Use of AZ API to create a Bing Seaarch Service respurce and connect it to AI Foundry.

## AKS Platform Logs

If you want to know who does what in your AKS clusters you need to enabale platform logs (diagnostic se ttings) to have access to the audit logs:

```kql
AKSAuditAdmin
| where _ResourceId contains "aks-snat-glitch"
| where Stage == "ResponseComplete" and ResponseStatus.code == "200" and Verb == "delete" and ObjectRef.resource == "deployments" 
| project TimeGenerated, User = User.username, Verb, Resource = ObjectRef.resource, Namespace = ObjectRef.namespace, resourceName = ObjectRef.name
| order by TimeGenerated desc 
```
