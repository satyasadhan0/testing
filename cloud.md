# Cloud Services
This section gives pricing for a cloud setup for the company and discusses backup strategies utilising the cloud.

[Pricing](#pricing-for-cloud-services) | [Backup](#backup-strategies) | [Plan](./plan.md) | [Network Design](./network.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

## Pricing for Cloud Services
- Average Object Size: 16 MB  
  - Conversion: \( 16 \, \text{MB} \times 0.0009765625 \, \text{GB/MB} = 0.015625 \, \text{GB} \)
- Monthly Storage Volume: 100 GB
  - Number of Objects:  
    \( \frac{100 \, \text{GB}}{0.015625 \, \text{GB per object}} = 6400 \, \text{objects} \)
- S3 Standard Tiered Price:  
  \( 100 \, \text{GB} \times 0.025 \, \text{USD per GB} = 2.50 \, \text{USD} \)

### Request Costs
- PUT Requests:  
  \( 1000 \, \text{requests} \times 0.0000055 \, \text{USD per request} = 0.0055 \, \text{USD} \)
- GET Requests:  
  \( 1000 \, \text{requests} \times 0.00000044 \, \text{USD per request} = 0.0004 \, \text{USD} \)

### S3 Select Costs
- Data Returned: \( 0.0007 \, \text{GB} \times 0.0008 \, \text{USD per GB} = 0.00 \, \text{USD} \)
- Data Scanned: \( 0.0026 \, \text{GB} \times 0.00225 \, \text{USD per GB} = 0.00 \, \text{USD} \)

### Total Monthly Costs
- Storage: $2.50  
- PUT Requests: $0.0055  
- GET Requests: $0.0004  
- Total Monthly Cost: \( 2.50 + 0.0055 + 0.0004 = 2.51 \, \text{USD} \)

### Upfront Costs
- Initial PUT, COPY, POST requests:  
  \( 6400 \, \text{objects} \times 0.0000055 \, \text{USD per request} = 0.0352 \, \text{USD} \)
- Total Upfront Cost: \( 0.04 \, \text{USD} \)

### Data Transfer Costs
#### Inbound Data
- Internet: \( 177 \, \text{GB} \times 0 \, \text{USD per GB} = 0.00 \, \text{USD} \)

#### Outbound Data
- Asia Pacific (Melbourne):  
  \( 134 \, \text{GB} \times 0.08 \, \text{USD per GB} = 10.72 \, \text{USD} \)
- Total Monthly Data Transfer Cost: \( 10.72 \, \text{USD} \)

---

## 2. Google Cloud Storage Cost Breakdown

### Standard Storage
- Monthly Storage Volume: 4949 GB  
  - Region: Australia Southeast 1 (Sydney)  
  - Cost: \( 4949 \, \text{GB} \times \text{standard pricing rate} = 113.827 \, \text{USD} \)

### Network Data Transfer
- Inter-Region Transfer within Asia:  
  \( 2 \, \text{GB} \times 0.08 \, \text{USD per GB} = 0.16 \, \text{USD} \)

### Total Google Cloud Cost
- Storage Cost: 113.827 USD  
- Data Transfer Cost: 0.16 USD  
- Total Monthly Cost: \( 113.987 \, \text{USD} \)

---

## 3. Summary and Recommendations

### Cost Comparison
| Service Provider    | Storage Cost (USD) | Data Transfer Cost (USD) | Total Cost (USD) |
|---------------------|---------------------|--------------------------|------------------|
| AWS S3          | 2.51               | 10.72                    | 13.23           |
| Google Cloud    | 113.827            | 0.16                     | 113.987         |

### Recommendation
AWS S3 is significantly more cost-effective for this scenario:
- AWS provides a lower total cost for both storage and data transfer.
- Google Cloud's cost is higher due to the larger storage volume and higher pricing for standard storage.


## Backup Strategies
## (a) Adequacy of the Current NAS-Based Backup Arrangement
The existing backup arrangement at the main office relies on a local RAID NAS to back up business-critical data, contracts, financial records, and monthly backups from on-site property management offices. While RAID-based NAS systems are reliable for local backups and ensure some fault tolerance, there are notable shortcomings:

- Single Point of Failure: If the NAS fails due to physical damage (fire, flood, theft), all data could be lost.  
- No Offsite Backup: There’s no provision for disaster recovery since backups are stored onsite.  
- Lack of Real-Time Backup: The current system does not back up data in real time, making it susceptible to data loss between backups.  
- Limited Scalability: Expanding NAS capacity requires additional hardware investment.  

Overall, while the current setup provides basic redundancy, it is insufficient to meet modern data security and disaster recovery standards.

---

## (b) Cloud-Based Backup Options

### Comparison of Cloud Backup Services

| Feature                     | AWS Backup                             | Google Cloud Storage              | Azure Backup                     |
|-----------------------------|--------------------------------------------|---------------------------------------|---------------------------------------|
| Backup Type             | Fully automated, centralized backup       | Object storage, lifecycle management  | Centralized, hybrid backup solution  |
| Storage Class           | S3 Glacier Deep Archive                   | Nearline or Coldline                 | Azure Blob Archive                   |
| Cost (Estimated)        | ~ $1/TB/month (S3 Glacier Deep Archive)   | ~ $1.23/TB/month (Coldline)          | ~ $1.20/TB/month (Blob Archive)      |
| Durability              | 99.999999999% (11 9’s durability)         | 99.999999999%                        | 99.999999999%                        |
| Access Time             | 12–48 hours for archival retrieval        | ~3 seconds (Nearline), up to hours   | Hours for archival retrieval         |
| Security                | End-to-end encryption, IAM policies       | Server-side encryption               | Secure transfer, encryption          |
| Scalability             | Highly scalable                           | Highly scalable                      | Highly scalable                      |
| Additional Features     | Lifecycle policies, automated backup jobs | Storage insights                     | Backup scheduling, monitoring        |

Recommended Cloud Service Provider: AWS Backup

- AWS offers the most cost-effective long-term storage for archival data with S3 Glacier Deep Archive (~$1/TB/month).  
- Provides powerful lifecycle management and automation tools.  
- Well-suited for businesses needing high durability and minimal recovery frequency.

---

## (c) Non-Cloud Backup Options

### Comparison of Non-Cloud Backup Solutions

| Feature                    | External Hard Drives                | Tape Backups                       | NAS with Offsite Replication       |
|----------------------------|-----------------------------------------|----------------------------------------|----------------------------------------|
| Cost                   | ~$100–$200/TB one-time cost            | ~$0.02/GB (lower initial cost)         | ~$500–$1,000 for hardware setup        |
| Durability             | Moderate (physical damage possible)    | High if stored properly                | High (with redundancy options)         |
| Capacity               | 2 TB–20 TB                             | Virtually unlimited (via tapes)        | Varies based on NAS model              |
| Ease of Use            | Easy for small data volumes            | Manual handling required               | Automated backup jobs supported        |
| Scalability            | Limited                                | High (add tapes)                       | Moderate                               |
| Portability            | High                                   | High                                   | Limited                                |

Recommended Non-Cloud Option: NAS with Offsite Replication

- Combines the benefits of centralized backup with disaster recovery by replicating data to an offsite NAS.  
- Automated backups eliminate manual intervention.

---

## Issues to Consider for Backup Selection

1. Data Sensitivity: Ensure encryption and compliance with data protection laws (e.g., GDPR).  
2. Recovery Time Objective (RTO): How quickly can data be restored?  
3. Recovery Point Objective (RPO): How much data loss is acceptable?  
4. Cost: Balance between upfront investment and ongoing costs.  
5. Scalability: Choose a solution that accommodates future data growth.  
6. Access Requirements: Evaluate how frequently data will be accessed (archival vs. active storage).  

---

## (d) Backup Recommendations for CQU ICT Students

### Recommended Tools

| Tool                       | Purpose                                  | Justification                                                                 |
|----------------------------|------------------------------------------|-------------------------------------------------------------------------------|
| Google Drive           | Cloud storage and real-time sync         | Free for students with 15 GB; collaborative tools (Docs, Sheets, Slides).     |
| OneDrive (Office 365)  | Cloud backup for Office documents        | Free for CQU students; integrates seamlessly with Microsoft Office Suite.     |
| GitHub                 | Version control for programming work     | Essential for ICT projects; free for private repositories.                    |
| External Hard Drive    | Local backup for critical files          | Cost-effective and quick access to data during internet outages.              |
| Backup Software (e.g., Duplicati) | Automated backups to external drives or cloud | Ensures regular, automated backups without manual intervention.               |


