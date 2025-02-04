# Cloud Services
This section gives pricing for a cloud setup for the company and discusses backup strategies utilising the cloud.

[Pricing](#pricing-for-cloud-services) | [Backup](#backup-strategies) | [Plan](./plan.md) | [Network Design](./network.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

## Pricing for Cloud Services

### Cloud Service Provider Comparison

| Cloud Provider | Region | Storage Type | Data Transfer | Estimated Monthly Cost (USD) | Estimated Annual Cost (USD) |
|---------------|--------|--------------|--------------|----------------------|----------------------|
| AWS          | Asia Pacific (Sydney) | S3 Standard (100 GB) | 177 GB In / 134 GB Out | $13.23 | $158.80 |
| Google Cloud | Australia Southeast 1 | Standard Storage (4949 GB) | Inter-Region Transfer | $9.50 + $4.48 | $113.99 |

**AWS Estimate Details:**
- **Storage:** S3 Standard, 100 GB per month
- **Data Transfer:** 177 GB inbound, 134 GB outbound
- **Requests:** PUT, COPY, POST, LIST (1000), GET, SELECT (1000)
- **Total Monthly Cost:** $13.23 USD
- **Total Annual Cost:** $158.80 USD

**Google Cloud Estimate Details:**
- **Storage:** Standard Storage, 4949 GB in Sydney
- **Data Transfer:** Inter-region transfer within Asia
- **Total Monthly Cost:** $9.50 + $4.48 USD
- **Total Annual Cost:** $113.99 USD

**Recommendation:**
Based on cost and performance considerations, **Google Cloud** is recommended for hosting the organisation's web server due to its lower overall annual cost ($113.99) compared to AWS ($158.80), while still providing reliable cloud storage and data transfer capabilities.

---

## Backup Strategies

### Evaluation of Current Backup Arrangement
- **Local RAID NAS**: Currently, backups are stored in an on-premises NAS with monthly backups from remote offices.
- **Issues:**
  - **Limited redundancy**: No off-site backup increases risk from local disasters.
  - **Long backup intervals**: Monthly backups may result in significant data loss.
  - **Scalability concerns**: Future growth may outpace NAS capacity.

### Cloud vs. Non-Cloud Backup Options

| Backup Type  | Provider | Storage Capacity | Estimated Cost (USD) | Advantages | Disadvantages |
|-------------|----------|------------------|----------------------|------------|---------------|
| **Cloud**   | AWS S3 Glacier | 500 GB | ~$3/month | High availability, secure, scalable | Ongoing cost, requires internet |
| **Cloud**   | Google Coldline | 500 GB | ~$2/month | Low cost, offsite, Google integration | Retrieval fees, latency |
| **Non-Cloud** | External HDD | 1 TB | $100 (one-time) | Low upfront cost, portable | Risk of failure, theft, physical damage |
| **Non-Cloud** | Tape Backup | 1 TB | $150 (one-time) | Long-term storage, durable | Slower access, higher maintenance |

**Recommendation:**
- A hybrid approach using **Google Cloud Coldline** for cost-efficient off-site backups alongside a **local RAID NAS** for fast recovery is recommended.

### Backup Strategy for CQU ICT Students

| Tool | Type | Features | Justification |
|------|------|----------|--------------|
| Google Drive | Cloud | 15 GB free, version control | Easy access from any device, CQU integration |
| OneDrive | Cloud | 5 GB free, Office 365 support | Suitable for Windows users, automatic backup |
| External HDD | Physical | 1 TB storage, offline access | Protects against cloud failures, cheap long-term solution |
| GitHub | Cloud | Free private repositories | Ideal for coding and collaborative projects |

**Recommended Approach:**
- **Primary:** Google Drive for documents, GitHub for coding projects.
- **Secondary:** OneDrive as an additional cloud option.
- **Offline Backup:** External HDD updated weekly for redundancy.

**Additional Considerations:**
- **Data Security:** Ensure encryption for sensitive data stored in the cloud.
- **Backup Frequency:** Set automated daily backups for critical data.
- **Redundancy:** Maintain at least two backup copies, one offline and one cloud-based.

