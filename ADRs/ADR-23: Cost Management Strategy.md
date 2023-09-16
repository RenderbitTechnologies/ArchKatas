## ADR-23: Cost Management Strategy

### Status
Adopted

### Context
In a cloud environment, especially on platforms like AWS, effective cost management is vital. The nature of AWS's pricing model provides multiple ways to procure and consume resources, each with its own cost and operational implications. The major choices to consider include:

**Instance Types**:
- **On-demand Instances**: These are standard instances that you pay for by the second, with no long-term commitments or upfront payments. They are ideal for short-term, spiky, or unpredictable workloads.

- **Reserved Instances (RIs)**: These offer significant discounts (up to 75%) compared to On-demand pricing, in exchange for committing to one or three years of usage. They are best for predictable workloads where you can forecast the required capacity.

- **Spot Instances**: Spot Instances allow you to bid on spare Amazon EC2 computing capacity for up to 90% off the On-demand price. While cost-effective, they are ephemeral and can be terminated if the spot price exceeds your bid.

Considering our travel platform's requirements, there's a need to balance the benefits of cost savings against the necessity for stable and reliable operations.

### Decision
- **Primary Workloads (like database servers, main application servers)**: Use **Reserved Instances** for core components of our platform. Since these components are always running and their load can be predicted to some extent, RIs offer a great way to save costs over the long term.

- **Development, Testing, and Staging Environments**: Use **On-demand Instances**. Given the sporadic and unpredictable nature of development and testing workloads, on-demand provides the flexibility to spin up and down resources as needed.

- **Stateless, Ephemeral, or Batch Processing Tasks**: Use **Spot Instances**. For tasks that can tolerate interruptions, or for non-critical batch processing jobs that run during off-peak hours, spot instances offer massive cost savings.

In addition to instance selection:
- Implement monitoring and alerting using AWS Cost Explorer and AWS Budgets to track and forecast expenditures.
- Regularly review and clean up unused resources.
- Utilize AWS Savings Plans where applicable to further optimize costs.

### Consequences
**Pros**:
- **Cost Savings**: By aligning the instance strategy with workload characteristics, there's a significant potential for cost savings.
- **Flexibility**: The chosen strategy provides the flexibility to cater to both predictable and unpredictable workloads.

**Cons**:
- **Management Overhead**: It requires regular monitoring and reviews to ensure that the strategy is optimized for current and future workloads.
- **Spot Instance Interruptions**: Relying on Spot Instances for certain tasks means those tasks might be interrupted. It's crucial to ensure tasks on Spot Instances can tolerate such interruptions or can be quickly resumed.
