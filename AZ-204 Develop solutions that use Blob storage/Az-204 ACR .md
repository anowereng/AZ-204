<https://www.kodez.com.au/post/deciphering-azure-container-services-a-guide-to-select-between-aca-aci-and-aks>

**Azure container registry**

Azure Container Registry (ACR) is a managed registry service Create and
maintain Azure container registries to store and manage your container
images and related artifacts.

Use the ACR service with your existing container development and
deployment pipelines, or use Azure Container Registry Tasks to build
container images in Azure. Build on demand, or fully automate builds
with triggers such as source code commits and base image updates.

**Use cases**

-   Scalable orchestration systems that manage containerized
    applications

-   Azure services that support building and running applications at
    scale.

**Azure Container Registry service tiers**

Azure Container Registry is available in multiple service tiers.

Basic: A cost-optimized entry point for developers learning about Azure
Container Registry.

Standard: same capabilities as Basic, with increased included storage
and image throughput.

Premium:

-   highest amount of included storage and concurrent operations.

-   higher image throughput

-   geo-replication for managing a single registry across multiple
    regions

-   content trust for image tag signing

-   private link with private endpoints to restrict access to the
    registry.

Automated image builds

Use [Azure Container Registry
Tasks](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview) (ACR
Tasks) to streamline building, testing, pushing, and deploying images in
Azure. Configure build tasks to automate your container OS and framework
patching pipeline, and build images automatically when your team commits
code to source control.

**Explore storage capabilities**

**Encryption-at-rest:** Azure automatically encrypts an image before
storing it, and decrypts it on-the-fly when you or your applications and
services pull the image.

**Regional storage:** 

\- Azure Container Registry stores data in the region where the registry
is created , to help customers meet data residency and compliance
requirements. 

\- Azure Container Registry stores data in the region where the registry
is created, Azure might also store registry data in a paired region in
the same geography.

*If a regional outage occurs, the registry data might become unavailable
and isn\'t automatically recovered. Customers who wish to have their
registry data stored in multiple regions for better performance across
different geographies, or who wish to have resiliency in a regional
outage event, should enable geo-replication*.

Geo-replication:  For scenarios requiring high-availability assurance,
consider using the geo-replication feature of Premium registries.

**Zone redundancy:** A feature of the Premium service tier, zone
redundancy uses Azure availability zones to replicate your registry to a
minimum of three separate zones in each enabled region.

**Scalable storage:** Azure Container Registry allows you to create as
many repositories, images, layers, or tags as you need, up to the
registry [storage
limit](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-skus#service-tier-features-and-limits).

High numbers of repositories and tags can impact the performance of your
registry. Periodically delete unused repositories, tags, and images as
part of your registry maintenance routine. Deleted registry resources
like repositories, images, and tags *can\'t* be recovered after
deletion.
