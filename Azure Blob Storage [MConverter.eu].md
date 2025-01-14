Azure Blob Storage is Microsoft\'s cloud-based object storage solution,
optimized for handling vast amounts of unstructured data such as text
and binary content. It is designed for various applications, including
serving images or documents directly to browsers, streaming media,
writing log files, and storing data for backup, disaster recovery, and
analysis

**Key Components:**

- **Storage Account**: The top-level container that provides a unique
  namespace for your Azure Storage data, accessible globally over HTTP
  or HTTPS.

- **Containers**: Within a storage account, containers organize blobs,
  similar to directories in a file system.

- **Blobs**: The individual pieces of data stored, which can be block
  blobs, append blobs, or page blobs, each optimized for different
  storage scenarios.

**Types of Storage Accounts:**

- **Standard General-Purpose v2**: Supports Blob Storage, Queue Storage,
  Table Storage, and Azure Files with various redundancy options like
  LRS, GRS, ZRS, and GZRS.

- **Premium**: Offers higher performance using solid-state drives (SSDs)
  and includes account types for block blobs, page blobs, or file
  shares, suitable for scenarios requiring low latency and high
  transaction rates.

**1. Locally Redundant Storage (LRS)**

- **Description**:  
  LRS replicates data **three times** within a single data center in a
  region.

- **Key Features**:

  - Copies exist in different fault domains and update domains within
    the same data center.

  - Cost-effective redundancy option.

  - Suitable for non-critical workloads or scenarios where regional
    outages are acceptable.

- **Durability**:  
  Offers **99.999999999% (11 nines)** durability for objects over a
  year.

- **Limitations**:

  - Data is not replicated outside the physical boundaries of the data
    center.

  - No protection against data center failures.

**2. Geo-Redundant Storage (GRS)**

- **Description**:  
  GRS replicates data across two geographic regions: the primary region
  (LRS replication) and a secondary region for disaster recovery.

- **Key Features**:

  - Six copies of data: **three copies in the primary region** (via LRS)
    and **three copies in a paired secondary region**.

  - Secondary data is read-only unless failover occurs.

  - Default replication for higher durability.

- **Durability**:  
  Offers **99.99999999999999% (16 nines)** durability for objects over a
  year.

- **Limitations**:

  - Higher latency for read access if secondary replication is required.

**3. Zone-Redundant Storage (ZRS)**

- **Description**:  
  ZRS replicates data across multiple availability zones in the same
  Azure region.

- **Key Features**:

  - Protects against zone-level failures within the region.

  - Each availability zone has an independent power source, cooling, and
    network.

  - Offers **low-latency** access to data since it remains in the same
    region.

- **Durability**:  
  Offers **99.9999999999% (12 nines)** durability for objects over a
  year.

- **Limitations**:

  - Data is not replicated to a geographically distant region.

**4. Geo-Zone Redundant Storage (GZRS)**

- **Description**:  
  GZRS combines the benefits of ZRS and GRS. Data is replicated across
  multiple zones in the primary region and is then replicated to a
  geographically distant secondary region.

- **Key Features**:

  - Combines zone-level redundancy (ZRS) and regional redundancy (GRS).

  - Offers protection from zone failures, regional failures, or both.

  - Six copies of data: three in different zones in the primary region,
    and three in a secondary paired region.

- **Durability**:  
  Offers **99.99999999999999% (16 nines)** durability for objects over a
  year.

- **Advantages**:

  - Best choice for mission-critical workloads requiring both regional
    and zone redundancy.

**Comparison Table**

| **Feature**           | **LRS**                                | **GRS**                                       | **ZRS**                    | **GZRS**                                       |
|-----------------------|----------------------------------------|-----------------------------------------------|----------------------------|------------------------------------------------|
| **Replication Scope** | Single Data Center                     | Primary + Secondary Region                    | Across Zones (Same Region) | Across Zones + Secondary Region                |
| **Number of Copies**  | 3                                      | 6 (3 Primary, 3 Secondary)                    | 3                          | 6 (3 Primary, 3 Secondary)                     |
| **Durability**        | 11 nines                               | 16 nines                                      | 12 nines                   | 16 nines                                       |
| **Read Access**       | Single Region                          | Primary Only (Secondary Readable with RA-GRS) | Single Region              | Primary Only (Secondary Readable with RA-GZRS) |
| **Cost**              | Least Expensive                        | More Expensive                                | Moderate                   | Most Expensive                                 |
| **Best Use Case**     | Cost-sensitive, Non-critical workloads | Disaster recovery, critical data              | Zone failure resilience    | Mission-critical with disaster recovery        |
|                       |                                        |                                               |                            |                                                |

**Comparison of Blob Types**

| **Feature**         | **Block Blob**                 | **Append Blob**               | **Page Blob**             |
|---------------------|--------------------------------|-------------------------------|---------------------------|
| **Optimization**    | Large unstructured data        | Append-only operations        | Random read/write access  |
| **Block/Page Size** | 64 KB - 100 MB (default 4 MiB) | 64 KB - 100 MB                | 512-byte pages            |
| **Maximum Size**    | Up to 190.7 TiB                | Same as block blob            | 8 TiB                     |
| **Use Case**        | Media, backups, documents      | Logs, telemetry, audit trails | Virtual disks, legacy VMs |
| **Write Behavior**  | Overwrite supported            | Append-only                   | Random access             |

**Key Takeaways**

- Use **block blobs** for general-purpose storage.

- Use **append blobs** for log files and sequential writes.

- Use **page blobs** for scenarios like Azure VM disks requiring random
  read/write access.

Blob storage tier:

Hot: Optimized for data that is accessed frequently; it has higher
storage costs but lower access costs.

Cool: Suitable for data that is infrequently accessed and stored for at
least 30 days; it offers lower storage costs and higher access costs
compared to the Hot tier.

Archive: Ideal for data that can tolerate several hours of retrieval
latency and is stored for a minimum of 180 days; it provides the lowest
storage costs with higher access costs.

**Key Points and Notes: Azure Blob Storage Automation and Access
Management**

**Automation with Azure Blob Lifecycle Management**

**Lifecycle Management** policies automate the movement of blobs between
tiers based on rules.

**Steps to configure:**

1.  **Define Rules**: Create rules to move blobs to cooler tiers based
    on conditions such as age or last access time.

2.  **Action Options**:

    - Move to Cool Tier

    - Move to Archive Tier

    - Delete blobs

3.  **Conditions**:

    - Blob age (e.g., move to cool tier if not modified for 30 days).

    - Blob type (block blob, append blob, etc.).

    - Blob prefix or tag filters.

**Storage Access**

- **Public vs. Private Access**:

  - **Public Access**:

    - All blobs in a public container are accessible anonymously.

    - Commonly used for public assets like images or videos for
      websites.

  - **Private Access**:

    - Ensures that only authorized users or applications can access
      blobs.

    - Entire storage accounts or individual containers can be locked
      into private access.

- **Blob URL Pattern**:

  - Example:
    https://\<storage-account-name\>.blob.core.windows.net/\<folder\>/\<blob-name\>

  - Folder structure is virtual unless using hierarchical namespaces
    (e.g., Data Lake).

**Shared Access Signature (SAS) Tokens**

- **Purpose**:  
  Allows controlled access to blobs in private containers without
  sharing account keys.

- **Types of SAS Tokens**:

  1.  **Individual (Ad Hoc) Tokens**:

      - Issued for specific blobs or containers.

      - Permissions: Read, write, delete, etc.

      - Limitations:

        - Cannot manage after creation.

        - To revoke access, regenerate the account key.

  2.  **Policy-Issued Tokens**:

      - Linked to a shared access policy.

      - Benefits:

        - Tokens can be rescinded by invalidating the policy.

        - Safer for managing access and business continuity.

      - Policies share lifecycle and access permissions across all
        tokens issued under them.

- **Token Customization**:

  - Permissions: Read, write, delete, etc.

  - Expiration: Set duration for validity.

  - IP Filters: Restrict access to specific IP ranges.

  - Protocols: Specify HTTP/HTTPS-only access.
