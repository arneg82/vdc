# Understanding environment types

There are two special _archetypes_ defined in the Azure Virtual Datacenter Automation Toolkit.
These are:
- simulated on-premises environment
- shared services environment

The toolkit performs special actions for these archetypes and you will need to identify them when using the toolkit. All other deployment types are identified as `workload`.

## Simulated on-premises environment
`on-premises`

This archetype defines a _simulated_ on-premises environment that is hosted in Azure. It is intended for testing VDC automation without needing to connect to your actual on-premise resources.

## Shared services environment
`shared-services`

This archetype provisions a set of serivces that are expected to be shared by multiple workloads. These include Active Directory Domain Services (AD DS), Azure Key Vault, Log Analytics, and a connection to the on-premises network.

See [Extend Active Directory Domain Services (AD DS) to Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain) for proven pracitces.

## Other environment types
`workload`

Deploys a workload virtual network where resources are deployed and securely connects this network to shared services network.
