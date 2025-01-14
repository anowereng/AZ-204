#[Explore Azure Blob storage]

Azure Blob Storage is Microsoft\'s cloud-based object storage solution,
optimized for handling vast amounts of unstructured data such as text
and binary content. It is designed for various applications, including
serving images or documents directly to browsers, streaming media,
writing log files, and storing data for backup, disaster recovery, and
analysis

**Key Components:**

-   **Storage Account**: The top-level container that provides a unique
    namespace for your Azure Storage data, accessible globally over HTTP
    or HTTPS.

-   **Containers**: Within a storage account, containers organize blobs,
    similar to directories in a file system.

-   **Blobs**: The individual pieces of data stored, which can be block
    blobs, append blobs, or page blobs, each optimized for different
    storage scenarios.

**Types of Storage Accounts:**

-   **Standard General-Purpose v2**: Supports Blob Storage, Queue
    Storage, Table Storage, and Azure Files with various redundancy
    options like LRS, GRS, ZRS, and GZRS.

-   **Premium**: Offers higher performance using solid-state drives
    (SSDs) and includes account types for block blobs, page blobs, or
    file shares, suitable for scenarios requiring low latency and high
    transaction rates.

**1. Locally Redundant Storage (LRS)**

-   **Description**:\
    LRS replicates data **three times** within a single data center in a
    region.

-   **Key Features**:

    -   Copies exist in different fault domains and update domains
        within the same data center.

    -   Cost-effective redundancy option.

    -   Suitable for non-critical workloads or scenarios where regional
        outages are acceptable.

-   **Durability**:\
    Offers **99.999999999% (11 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated outside the physical boundaries of the
        data center.

    -   No protection against data center failures.

**2. Geo-Redundant Storage (GRS)**

-   **Description**:\
    GRS replicates data across two geographic regions: the primary
    region (LRS replication) and a secondary region for disaster
    recovery.

-   **Key Features**:

    -   Six copies of data: **three copies in the primary region** (via
        LRS) and **three copies in a paired secondary region**.

    -   Secondary data is read-only unless failover occurs.

    -   Default replication for higher durability.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Limitations**:

    -   Higher latency for read access if secondary replication is
        required.

**3. Zone-Redundant Storage (ZRS)**

-   **Description**:\
    ZRS replicates data across multiple availability zones in the same
    Azure region.

-   **Key Features**:

    -   Protects against zone-level failures within the region.

    -   Each availability zone has an independent power source, cooling,
        and network.

    -   Offers **low-latency** access to data since it remains in the
        same region.

-   **Durability**:\
    Offers **99.9999999999% (12 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated to a geographically distant region.

**4. Geo-Zone Redundant Storage (GZRS)**

-   **Description**:\
    GZRS combines the benefits of ZRS and GRS. Data is replicated across
    multiple zones in the primary region and is then replicated to a
    geographically distant secondary region.

-   **Key Features**:

    -   Combines zone-level redundancy (ZRS) and regional redundancy
        (GRS).

    -   Offers protection from zone failures, regional failures, or
        both.

    -   Six copies of data: three in different zones in the primary
        region, and three in a secondary paired region.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Advantages**:

    -   Best choice for mission-critical workloads requiring both
        regional and zone redundancy.

**Comparison Table**

  -----------------------------------------------------------------------------------
  **Feature**      **LRS**           **GRS**          **ZRS**      **GZRS**
  ---------------- ----------------- ---------------- ------------ ------------------
  **Replication    Single Data       Primary +        Across Zones Across Zones +
  Scope**          Center            Secondary Region (Same        Secondary Region
                                                      Region)      

  **Number of      3                 6 (3 Primary, 3  3            6 (3 Primary, 3
  Copies**                           Secondary)                    Secondary)

  **Durability**   11 nines          16 nines         12 nines     16 nines

  **Read Access**  Single Region     Primary Only     Single       Primary Only
                                     (Secondary       Region       (Secondary
                                     Readable with                 Readable with
                                     RA-GRS)                       RA-GZRS)

  **Cost**         Least Expensive   More Expensive   Moderate     Most Expensive

  **Best Use       Cost-sensitive,   Disaster         Zone failure Mission-critical
  Case**           Non-critical      recovery,        resilience   with disaster
                   workloads         critical data                 recovery

                                                                   
  -----------------------------------------------------------------------------------

**Comparison of Blob Types**

  ------------------------------------------------------------------------------
  **Feature**        **Block Blob**    **Append Blob**           **Page Blob**
  ------------------ ----------------- ------------------------- ---------------
  **Optimization**   Large             Append-only operations    Random
                     unstructured data                           read/write
                                                                 access

  **Block/Page       64 KB - 100 MB    64 KB - 100 MB            512-byte pages
  Size**             (default 4 MiB)                             

  **Maximum Size**   Up to 190.7 TiB   Same as block blob        8 TiB

  **Use Case**       Media, backups,   logging data from virtual Virtual disks,
                     documents         machines., telemetry,     legacy VMs
                                       audit trails              

  **Write Behavior** Overwrite         Append-only               Random access
                     supported                                   
  ------------------------------------------------------------------------------

**Key Takeaways**

-   Use **block blobs** for general-purpose storage.

-   Use **append blobs** for log files and sequential writes.

-   Use **page blobs** for scenarios like Azure VM disks requiring
    random read/write access.

**Blob storage tier:**

Hot: Optimized for data that is accessed frequently; it has higher
storage costs but lower access costs.

Cool: Suitable for data that is infrequently accessed and stored for at
least 30 days; it offers lower storage costs and higher access costs
compared to the Hot tier.

Archive: Ideal for data that can tolerate several hours of retrieval
latency and is stored for a minimum of 180 days; it provides the lowest
storage costs with higher access costs.

**Storage Access**

-   **Public vs. Private Access**:

    -   **Public Access**:

        -   All blobs in a public container are accessible anonymously.

        -   Commonly used for public assets like images or videos for
            websites.

    -   **Private Access**:

        -   Ensures that only authorized users or applications can
            access blobs.

        -   Entire storage accounts or individual containers can be
            locked into private access.

-   **Blob URL Pattern**:

    -   Example:
        https://\<storage-account-name\>.blob.core.windows.net/\<folder\>/\<blob-name\>

    -   Folder structure is virtual unless using hierarchical namespaces
        (e.g., Data Lake).
[Explore Azure Blob storage]{.underline}

Azure Blob Storage is Microsoft\'s cloud-based object storage solution,
optimized for handling vast amounts of unstructured data such as text
and binary content. It is designed for various applications, including
serving images or documents directly to browsers, streaming media,
writing log files, and storing data for backup, disaster recovery, and
analysis

**Key Components:**

-   **Storage Account**: The top-level container that provides a unique
    namespace for your Azure Storage data, accessible globally over HTTP
    or HTTPS.

-   **Containers**: Within a storage account, containers organize blobs,
    similar to directories in a file system.

-   **Blobs**: The individual pieces of data stored, which can be block
    blobs, append blobs, or page blobs, each optimized for different
    storage scenarios.

**Types of Storage Accounts:**

-   **Standard General-Purpose v2**: Supports Blob Storage, Queue
    Storage, Table Storage, and Azure Files with various redundancy
    options like LRS, GRS, ZRS, and GZRS.

-   **Premium**: Offers higher performance using solid-state drives
    (SSDs) and includes account types for block blobs, page blobs, or
    file shares, suitable for scenarios requiring low latency and high
    transaction rates.

**1. Locally Redundant Storage (LRS)**

-   **Description**:\
    LRS replicates data **three times** within a single data center in a
    region.

-   **Key Features**:

    -   Copies exist in different fault domains and update domains
        within the same data center.

    -   Cost-effective redundancy option.

    -   Suitable for non-critical workloads or scenarios where regional
        outages are acceptable.

-   **Durability**:\
    Offers **99.999999999% (11 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated outside the physical boundaries of the
        data center.

    -   No protection against data center failures.

**2. Geo-Redundant Storage (GRS)**

-   **Description**:\
    GRS replicates data across two geographic regions: the primary
    region (LRS replication) and a secondary region for disaster
    recovery.

-   **Key Features**:

    -   Six copies of data: **three copies in the primary region** (via
        LRS) and **three copies in a paired secondary region**.

    -   Secondary data is read-only unless failover occurs.

    -   Default replication for higher durability.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Limitations**:

    -   Higher latency for read access if secondary replication is
        required.

**3. Zone-Redundant Storage (ZRS)**

-   **Description**:\
    ZRS replicates data across multiple availability zones in the same
    Azure region.

-   **Key Features**:

    -   Protects against zone-level failures within the region.

    -   Each availability zone has an independent power source, cooling,
        and network.

    -   Offers **low-latency** access to data since it remains in the
        same region.

-   **Durability**:\
    Offers **99.9999999999% (12 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated to a geographically distant region.

**4. Geo-Zone Redundant Storage (GZRS)**

-   **Description**:\
    GZRS combines the benefits of ZRS and GRS. Data is replicated across
    multiple zones in the primary region and is then replicated to a
    geographically distant secondary region.

-   **Key Features**:

    -   Combines zone-level redundancy (ZRS) and regional redundancy
        (GRS).

    -   Offers protection from zone failures, regional failures, or
        both.

    -   Six copies of data: three in different zones in the primary
        region, and three in a secondary paired region.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Advantages**:

    -   Best choice for mission-critical workloads requiring both
        regional and zone redundancy.

**Comparison Table**

  -----------------------------------------------------------------------------------
  **Feature**      **LRS**           **GRS**          **ZRS**      **GZRS**
  ---------------- ----------------- ---------------- ------------ ------------------
  **Replication    Single Data       Primary +        Across Zones Across Zones +
  Scope**          Center            Secondary Region (Same        Secondary Region
                                                      Region)      

  **Number of      3                 6 (3 Primary, 3  3            6 (3 Primary, 3
  Copies**                           Secondary)                    Secondary)

  **Durability**   11 nines          16 nines         12 nines     16 nines

  **Read Access**  Single Region     Primary Only     Single       Primary Only
                                     (Secondary       Region       (Secondary
                                     Readable with                 Readable with
                                     RA-GRS)                       RA-GZRS)

  **Cost**         Least Expensive   More Expensive   Moderate     Most Expensive

  **Best Use       Cost-sensitive,   Disaster         Zone failure Mission-critical
  Case**           Non-critical      recovery,        resilience   with disaster
                   workloads         critical data                 recovery

                                                                   
  -----------------------------------------------------------------------------------

**Comparison of Blob Types**

  ------------------------------------------------------------------------------
  **Feature**        **Block Blob**    **Append Blob**           **Page Blob**
  ------------------ ----------------- ------------------------- ---------------
  **Optimization**   Large             Append-only operations    Random
                     unstructured data                           read/write
                                                                 access

  **Block/Page       64 KB - 100 MB    64 KB - 100 MB            512-byte pages
  Size**             (default 4 MiB)                             

  **Maximum Size**   Up to 190.7 TiB   Same as block blob        8 TiB

  **Use Case**       Media, backups,   logging data from virtual Virtual disks,
                     documents         machines., telemetry,     legacy VMs
                                       audit trails              

  **Write Behavior** Overwrite         Append-only               Random access
                     supported                                   
  ------------------------------------------------------------------------------

**Key Takeaways**

-   Use **block blobs** for general-purpose storage.

-   Use **append blobs** for log files and sequential writes.

-   Use **page blobs** for scenarios like Azure VM disks requiring
    random read/write access.

**Blob storage tier:**

Hot: Optimized for data that is accessed frequently; it has higher
storage costs but lower access costs.

Cool: Suitable for data that is infrequently accessed and stored for at
least 30 days; it offers lower storage costs and higher access costs
compared to the Hot tier.

Archive: Ideal for data that can tolerate several hours of retrieval
latency and is stored for a minimum of 180 days; it provides the lowest
storage costs with higher access costs.

**Storage Access**

-   **Public vs. Private Access**:

    -   **Public Access**:

        -   All blobs in a public container are accessible anonymously.

        -   Commonly used for public assets like images or videos for
            websites.

    -   **Private Access**:

        -   Ensures that only authorized users or applications can
            access blobs.

        -   Entire storage accounts or individual containers can be
            locked into private access.

-   **Blob URL Pattern**:

    -   Example:
        https://\<storage-account-name\>.blob.core.windows.net/\<folder\>/\<blob-name\>

    -   Folder structure is virtual unless using hierarchical namespaces
        (e.g., Data Lake).
[Explore Azure Blob storage]{.underline}

Azure Blob Storage is Microsoft\'s cloud-based object storage solution,
optimized for handling vast amounts of unstructured data such as text
and binary content. It is designed for various applications, including
serving images or documents directly to browsers, streaming media,
writing log files, and storing data for backup, disaster recovery, and
analysis

**Key Components:**

-   **Storage Account**: The top-level container that provides a unique
    namespace for your Azure Storage data, accessible globally over HTTP
    or HTTPS.

-   **Containers**: Within a storage account, containers organize blobs,
    similar to directories in a file system.

-   **Blobs**: The individual pieces of data stored, which can be block
    blobs, append blobs, or page blobs, each optimized for different
    storage scenarios.

**Types of Storage Accounts:**

-   **Standard General-Purpose v2**: Supports Blob Storage, Queue
    Storage, Table Storage, and Azure Files with various redundancy
    options like LRS, GRS, ZRS, and GZRS.

-   **Premium**: Offers higher performance using solid-state drives
    (SSDs) and includes account types for block blobs, page blobs, or
    file shares, suitable for scenarios requiring low latency and high
    transaction rates.

**1. Locally Redundant Storage (LRS)**

-   **Description**:\
    LRS replicates data **three times** within a single data center in a
    region.

-   **Key Features**:

    -   Copies exist in different fault domains and update domains
        within the same data center.

    -   Cost-effective redundancy option.

    -   Suitable for non-critical workloads or scenarios where regional
        outages are acceptable.

-   **Durability**:\
    Offers **99.999999999% (11 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated outside the physical boundaries of the
        data center.

    -   No protection against data center failures.

**2. Geo-Redundant Storage (GRS)**

-   **Description**:\
    GRS replicates data across two geographic regions: the primary
    region (LRS replication) and a secondary region for disaster
    recovery.

-   **Key Features**:

    -   Six copies of data: **three copies in the primary region** (via
        LRS) and **three copies in a paired secondary region**.

    -   Secondary data is read-only unless failover occurs.

    -   Default replication for higher durability.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Limitations**:

    -   Higher latency for read access if secondary replication is
        required.

**3. Zone-Redundant Storage (ZRS)**

-   **Description**:\
    ZRS replicates data across multiple availability zones in the same
    Azure region.

-   **Key Features**:

    -   Protects against zone-level failures within the region.

    -   Each availability zone has an independent power source, cooling,
        and network.

    -   Offers **low-latency** access to data since it remains in the
        same region.

-   **Durability**:\
    Offers **99.9999999999% (12 nines)** durability for objects over a
    year.

-   **Limitations**:

    -   Data is not replicated to a geographically distant region.

**4. Geo-Zone Redundant Storage (GZRS)**

-   **Description**:\
    GZRS combines the benefits of ZRS and GRS. Data is replicated across
    multiple zones in the primary region and is then replicated to a
    geographically distant secondary region.

-   **Key Features**:

    -   Combines zone-level redundancy (ZRS) and regional redundancy
        (GRS).

    -   Offers protection from zone failures, regional failures, or
        both.

    -   Six copies of data: three in different zones in the primary
        region, and three in a secondary paired region.

-   **Durability**:\
    Offers **99.99999999999999% (16 nines)** durability for objects over
    a year.

-   **Advantages**:

    -   Best choice for mission-critical workloads requiring both
        regional and zone redundancy.

**Comparison Table**

  -----------------------------------------------------------------------------------
  **Feature**      **LRS**           **GRS**          **ZRS**      **GZRS**
  ---------------- ----------------- ---------------- ------------ ------------------
  **Replication    Single Data       Primary +        Across Zones Across Zones +
  Scope**          Center            Secondary Region (Same        Secondary Region
                                                      Region)      

  **Number of      3                 6 (3 Primary, 3  3            6 (3 Primary, 3
  Copies**                           Secondary)                    Secondary)

  **Durability**   11 nines          16 nines         12 nines     16 nines

  **Read Access**  Single Region     Primary Only     Single       Primary Only
                                     (Secondary       Region       (Secondary
                                     Readable with                 Readable with
                                     RA-GRS)                       RA-GZRS)

  **Cost**         Least Expensive   More Expensive   Moderate     Most Expensive

  **Best Use       Cost-sensitive,   Disaster         Zone failure Mission-critical
  Case**           Non-critical      recovery,        resilience   with disaster
                   workloads         critical data                 recovery

                                                                   
  -----------------------------------------------------------------------------------

**Comparison of Blob Types**

  ------------------------------------------------------------------------------
  **Feature**        **Block Blob**    **Append Blob**           **Page Blob**
  ------------------ ----------------- ------------------------- ---------------
  **Optimization**   Large             Append-only operations    Random
                     unstructured data                           read/write
                                                                 access

  **Block/Page       64 KB - 100 MB    64 KB - 100 MB            512-byte pages
  Size**             (default 4 MiB)                             

  **Maximum Size**   Up to 190.7 TiB   Same as block blob        8 TiB

  **Use Case**       Media, backups,   logging data from virtual Virtual disks,
                     documents         machines., telemetry,     legacy VMs
                                       audit trails              

  **Write Behavior** Overwrite         Append-only               Random access
                     supported                                   
  ------------------------------------------------------------------------------

**Key Takeaways**

-   Use **block blobs** for general-purpose storage.

-   Use **append blobs** for log files and sequential writes.

-   Use **page blobs** for scenarios like Azure VM disks requiring
    random read/write access.

**Blob storage tier:**

Hot: Optimized for data that is accessed frequently; it has higher
storage costs but lower access costs.

Cool: Suitable for data that is infrequently accessed and stored for at
least 30 days; it offers lower storage costs and higher access costs
compared to the Hot tier.

Archive: Ideal for data that can tolerate several hours of retrieval
latency and is stored for a minimum of 180 days; it provides the lowest
storage costs with higher access costs.

**Storage Access**

-   **Public vs. Private Access**:

    -   **Public Access**:

        -   All blobs in a public container are accessible anonymously.

        -   Commonly used for public assets like images or videos for
            websites.

    -   **Private Access**:

        -   Ensures that only authorized users or applications can
            access blobs.

        -   Entire storage accounts or individual containers can be
            locked into private access.

-   **Blob URL Pattern**:

    -   Example:
        https://\<storage-account-name\>.blob.core.windows.net/\<folder\>/\<blob-name\>

    -   Folder structure is virtual unless using hierarchical namespaces
        (e.g., Data Lake).
