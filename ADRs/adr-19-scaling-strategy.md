# ADR-19: Scaling Strategy

## Status

Adopted

## Context

With the international launch of our platform, there's an anticipated user growth rate of 30% YoY. Ensuring that our infrastructure scales to accommodate this growth, whilst maintaining performance and uptime, is paramount.

Two prominent scaling strategies are:

1. **Manual Scaling**: This involves pre-emptively provisioning resources based on forecasted demand. This could mean adding more servers during expected peak times.
    - **Pros**: Complete control over resources, potentially more cost-effective if demand is predictable.
    - **Cons**: Less flexible, risk of over-provisioning or under-provisioning, requires constant monitoring.

2. **Auto-scaling**:
    - **[AWS Auto Scaling Groups](https://aws.amazon.com/autoscaling/)**: Allows you to ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application.
        - **Pros**: Dynamically scales with actual demand, improves fault tolerance, and availability. Cost-effective as you only pay for what you use.
        - **Cons**: Slight delay in scaling, potential for unexpected costs if not monitored.

## Decision

Given the unpredictability associated with user growth and the importance of providing a consistent user experience regardless of load, we've decided to adopt the **AWS Auto Scaling Groups** approach for our scaling strategy.

This approach will allow us to:

- Automatically increase the number of instances during demand spikes to maintain performance.
- Decrease capacity during lulls to reduce costs.
- Ensure high availability and fault tolerance by distributing instances across multiple Availability Zones in AWS.

## Consequences

**Pros**:

- **Adaptive Performance**: Our application can adapt in real-time to both spikes and dips in usage.
- **Cost-Effective**: Only pay for the resources we're actively using.
- **Improved Fault Tolerance**: With instances distributed across multiple Availability Zones, our application's uptime is improved.

**Cons**:

- **Monitoring Overhead**: Ensuring optimal configuration and preventing unexpected costs requires consistent monitoring.
- **Startup Latency**: There's a slight delay when booting up new instances, potentially leading to a temporary performance dip before scaling effects take place.
