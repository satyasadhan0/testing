# Cloud Services
This section gives pricing for a cloud setup for the company and discusses backup strategies utilising the cloud.

[Pricing](#pricing-for-cloud-services) | [Backup](#backup-strategies) | [Plan](./plan.md) | [Network Design](./network.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

## Pricing for Cloud Services

The organisation plans to move its web server to the cloud, and the cost has been estimated for both AWS and Azure, with identical specifications for comparison. Below are the details:

---

### 1. **AWS (Amazon Web Services)**

**Specifications:**
- **Region:** Asia Pacific (Sydney)
- **Operating System:** Linux
- **Storage:** 100 GB S3 Standard (SSD)
- **Virtual Machine Type:** General Purpose (T3.medium: 2 vCPUs, 4 GB RAM)
- **Bandwidth:** 1 TB/month outbound

**Cost Breakdown:**
- **S3 Standard Storage:**
  - Storage: 100 GB x $0.025/GB = **$2.50/month**
  - PUT, COPY, POST Requests: 100 requests x $0.0000055/request = **$0.0006/month**
  - GET Requests: 100 requests x $0.00000044/request = **$0.00/month**
  - S3 Select Returned Data: 80 GB x $0.0008/GB = **$0.064/month**
  - S3 Select Scanned Data: 80 GB x $0.00225/GB = **$0.18/month**
  - **Total Storage Cost:** **$2.74/month**

- **Data Transfer:**
  - Outbound: 100 GB x $0.08/GB = **$8.00/month**
  - **Total Data Transfer Cost:** **$8.00/month**

- **Lambda Requests:**
  - Monthly Compute Charges: **$0.0005461/month**
  - Object Lambda Charges: **$10.24/month**

**Total Monthly Cost (AWS):** **$10.24 + $8.00 + $2.74 = $21.00 AUD**  
**Annual Cost (AWS):** **$21.00 x 12 = $252.00 AUD**

---

### 2. **Azure**

**Specifications:**
- **Region:** Australia East
- **Operating System:** Linux
- **Storage:** 100 GB SSD
- **Virtual Machine Type:** General Purpose (2 L8as v3: 8 vCPUs, 64 GB RAM)
- **Bandwidth:** 1 TB/month outbound

**Cost Breakdown:**
- **Virtual Machine:**
  - 2 L8as v3 (8 vCPUs, 64 GB RAM): **$970.71/month**

- **Storage:**
  - Managed Disks (E40): Included in VM pricing

- **Bandwidth:**
  - Outbound: 5 GB from Australia East to East Asia included in VM pricing.

**Total Monthly Cost (Azure):** **$970.71 AUD**  
**Annual Cost (Azure):** **$970.71 x 12 = $11,648.52 AUD**

---

### 3. **Recommendation**

Based on the cost comparison, **AWS** is the more cost-effective solution for hosting the organisation’s web server. The total annual cost for AWS is **$252.00 AUD**, significantly lower than Azure’s **$11,648.52 AUD**.

**Reason for Recommendation:**
- **Cost Efficiency:** AWS offers a far more affordable solution for small to medium web hosting.
- **Scalability:** AWS provides auto-scaling options to handle increased web traffic cost-effectively.
- **Performance:** Hosting in the Asia Pacific (Sydney) region ensures low latency for Australian users.
- **Flexibility:** AWS allows easy management and integration with other services.

**Conclusion:** The organisation should move its web server to AWS to minimize operational costs while ensuring reliable performance.


## Backup Strategies

### (a) Adequacy of Current Backup Arrangement

The organisation currently uses a local RAID NAS at the main office to back up important business data and automate regular backups of key computers. Additionally, monthly backups from on-site property management offices are stored on the main office NAS.

**Assessment:**
- **Advantages:**
  - **Redundancy:** RAID provides data redundancy, protecting against single-drive failures.
  - **Centralization:** The main office NAS consolidates data from various offices.

- **Limitations:**
  - **Single Point of Failure:** If the NAS hardware or main office is compromised (e.g., fire, theft, or natural disaster), data may be lost.
  - **Infrequent Backups:** Monthly backups from on-site offices leave data vulnerable to significant loss in case of an incident between backup intervals.
  - **Limited Scalability:** A local NAS may not scale efficiently as data grows.
  - **No Off-Site Redundancy:** Lack of off-site backups increases risk.

**Conclusion:** The current arrangement is insufficient for ensuring data availability, reliability, and disaster recovery.

---

### (b) Cloud Backup Options

Cloud backups provide off-site storage, scalability, and automated management, reducing reliance on physical hardware.

| **Cloud Provider** | **Service**             | **Capacity**      | **Estimated Cost (AUD)**  | **Key Features**                                                                                         |
|--------------------|-------------------------|-------------------|---------------------------|---------------------------------------------------------------------------------------------------------|
| AWS                | S3 Glacier             | 1 TB/month        | $4.80/month              | Low-cost, long-term storage; ideal for archival and infrequent access.                                  |
| Azure              | Blob Storage (Cool)    | 1 TB/month        | $6.20/month              | Suitable for infrequently accessed data; geo-redundant storage options available.                       |
| Google Cloud       | Coldline Storage       | 1 TB/month        | $4.70/month              | Designed for long-term backups; low retrieval costs for occasional access.                              |

**Recommendation:**  
**AWS S3 Glacier** is recommended due to its cost-effectiveness and strong integration with automated backup tools. It also offers robust security, high durability (99.999999999%), and compliance certifications.

---

### (c) Non-Cloud Backup Options

For organisations preferring non-cloud solutions, local or hybrid backup strategies can complement the current NAS setup.

| **Option**                 | **Description**                                                                 | **Cost Estimate**        | **Key Features**                                                                                   |
|----------------------------|---------------------------------------------------------------------------------|---------------------------|---------------------------------------------------------------------------------------------------|
| External Hard Drives       | Use high-capacity drives for periodic backups.                                  | ~$150 per 5 TB           | Portable, one-time cost, but prone to failure without redundancy.                                |
| Off-Site Backup Location   | Maintain a secondary NAS in a geographically distant location.                  | ~$1,200 for hardware     | Protects against local disasters, but requires manual management and higher initial costs.       |
| Tape Backup                | Use tape drives for archival purposes.                                          | ~$800 for tape drive     | Reliable for long-term storage, but slower retrieval times and higher operational overhead.      |

---

### (d) Backup Recommendation for New CQU ICT Students

**Suggested Approach:**  
Students should adopt a hybrid backup strategy that combines local and cloud backups to ensure data safety and easy accessibility.

| **Tool**            | **Type**       | **Purpose**                                           | **Why Recommended**                                                                 |
|---------------------|----------------|-------------------------------------------------------|-------------------------------------------------------------------------------------|
| Google Drive        | Cloud Backup   | Store university documents, assignments, and notes.  | 15 GB free storage; seamless integration with Google Workspace tools (Docs, Sheets). |
| OneDrive            | Cloud Backup   | Backup large files and collaborate on group projects. | Included in CQU student subscription with generous storage limits.                 |
| External SSD        | Local Backup   | Keep an offline copy of all critical coursework.      | Fast data transfer, portable, and reliable for local redundancy.                   |

**Justification:**  
- **Cloud Tools:** Google Drive and OneDrive ensure accessibility and collaboration across devices.  
- **Local Backup:** External SSDs provide offline redundancy and quick access to data in case of internet outages.  

**Backup Schedule:**  
1. Perform weekly incremental backups to the cloud using Google Drive or OneDrive.  
2. Perform monthly full backups to an external SSD.  
3. Regularly verify and test backup integrity.

By combining reliable tools and maintaining a consistent schedule, students can safeguard their university work throughout the course.


