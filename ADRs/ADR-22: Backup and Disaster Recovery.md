## ADR-22: Backup and Disaster Recovery

### Status
Adopted

### Context
For an international travel platform like ours, data is one of the most valuable assets. A robust Backup and Disaster Recovery (BDR) strategy is essential to ensure the availability, resilience, and security of this data. BDR decisions are often around the nature of backup (Snapshot vs. Continuous) and where the backups are stored (Single-region vs. Multi-region), along with concerns about encryption, retention policies, and cost.

**Backup Mechanisms**:
- **Snapshot Backup**: This is a point-in-time backup of the database. Snapshots are usually taken daily and are ideal for applications where data change rate isn't extremely high.
- **Continuous Backup**: This involves continuous data capture and backup of every change. It provides better RPO (Recovery Point Objective) but could be more expensive and complex to manage.

**Backup Storage Location**:
- **Single-region Storage**: Backups are stored in the same region as the primary data center. Faster and often less expensive, but less resilient to region-specific disasters.
- **Multi-region Storage**: Backups are stored across multiple geographic locations to provide higher resilience against disasters that might affect a single region.

### Decision
- **Backup Mechanism**: Opt for a **hybrid strategy** where:
    - Regular **Snapshot Backups** are taken daily to ensure we have consistent, point-in-time data copies.
    - **Continuous Backups** are employed for critical data tables or subsets that have higher rates of change and where data loss would be most impactful.
- **Backup Storage Location**: Adopt a **Multi-region Storage** approach to ensure that, in the event of a regional catastrophe or service disruption, data can be recovered from another unaffected region.
- **Data Security**:
    - All backups will be encrypted using **AES** encryption to ensure the data remains secure.
    - Implement role-based access controls to ensure only authorized personnel can access and restore from backups.
- **Retention Policy**: Retain daily backups for 30 days, weekly backups for 12 weeks, and monthly backups for 12 months to ensure a balance between data recoverability and cost-effectiveness.

### Consequences
**Pros**:
- **High Resilience**: Multi-region storage ensures data recoverability even in the event of large-scale regional disasters.
- **Data Security**: Encryption and strict access controls ensure data remains secure even when stored off-site.
- **Flexibility**: A hybrid backup approach ensures that we get the best of both snapshot and continuous backups.

**Cons**:
- **Increased Cost**: Multi-region storage and continuous backup for certain datasets will lead to higher storage and operational costs. However, the benefits of data resilience and availability justify this expenditure.
