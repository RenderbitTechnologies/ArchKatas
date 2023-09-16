# ADR-24: Load Balancing Strategy

## Status

Adopted

## Context

Load balancing is an essential component of any large-scale web application. It is responsible for distributing incoming application traffic across multiple targets, ensuring both availability and fault tolerance. The primary choices to consider in our scenario include:

1. **AWS Elastic Load Balancer (ELB)**:
    - **Pros**:
        - Fully managed and integrated with the AWS ecosystem.
        - Provides automatic scaling based on incoming traffic.
        - Supports both Application Load Balancing (Layer 7) and Network Load Balancing (Layer 4).
        - Comes with integrated AWS metrics, monitoring, and health checks.
    - **Cons**:
        - Might be more costly than self-managed solutions.
        - Less granular control compared to some other tools.

2. **Nginx**:
    - **Pros**:
        - Very popular and widely used for web serving and reverse proxying.
        - Supports both HTTP and TCP load balancing.
        - Offers granular control, SSL termination, and caching capabilities.
    - **Cons**:
        - Requires manual setup, maintenance, and scaling.
        - Not as deeply integrated into the AWS ecosystem.

3. **HAProxy**:
    - **Pros**:
        - A powerful and fast load balancer.
        - Supports TCP and HTTP load balancing.
        - Provides detailed metrics and logging.
    - **Cons**:
        - Has a steeper learning curve.
        - Requires manual management, unlike AWS ELB.

Considering the international launch of our travel platform and the requirement to prioritize North America and Western Europe for latency considerations, a solution that can easily handle varying traffic loads and ensure low latency is essential.

## Decision

Opt for **AWS Elastic Load Balancer (ELB)** for the following reasons:

- **Ease of Management**: ELB provides a fully managed service, reducing operational overhead.
- **Integration with AWS**: ELB is natively integrated with other AWS services, simplifying metrics gathering, monitoring, and auto-scaling.
- **Global Reach**: AWS ELB integrates with the Amazon Route 53 service, ensuring efficient routing of users from different regions to the nearest data centers.
- **Built-in Security**: ELB offers built-in integrations for AWS security features such as AWS Shield, AWS WAF, and SSL/TLS termination.

## Consequences

**Pros**:

- **Automatic Scaling**: ELB handles traffic spikes smoothly without manual intervention.
- **High Availability**: ELB automatically distributes traffic across multiple targets, ensuring that if one fails, traffic is rerouted to healthy ones.
- **Enhanced Monitoring**: Native integration with AWS CloudWatch for monitoring and alerts.

**Cons**:

- **Cost Implications**: ELB might come with a higher cost than self-managed solutions.
- **Less Granular Control**: Some advanced configurations possible in Nginx or HAProxy might be harder or not possible to implement with ELB.
