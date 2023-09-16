# ADR-16: Deployment Strategy

## Status

Adopted

## Context

The efficiency, scalability, and reliability of our deployment process play a crucial role in ensuring that our application remains competitive and meets the expectations of our users. We considered the following deployment strategies:

1. **[Containers (Docker with Kubernetes)](https://www.docker.com/what-docker)**:
    - **Docker**: A platform to develop, ship, and run applications inside containers.
    - **[Kubernetes](https://kubernetes.io/)**: An open-source container orchestration system for automating application deployment, scaling, and management.

2. **[Serverless (AWS Lambda)](https://aws.amazon.com/lambda/)**:
    - Allows you to run code without provisioning or managing servers. You're billed only for the compute time consumed.

3. **Traditional VMs (like AWS EC2)**:
    - Virtual machines allow you to run applications on virtualized hardware, managed by a hypervisor.

Given our application's complexity, growth trajectory, and performance requirements, our deployment strategy needed to balance speed, efficiency, flexibility, and cost.

## Decision

We have chosen **Docker with Kubernetes** for the following reasons:

1. **Scalability**: Kubernetes offers a highly scalable environment where containers can be effortlessly scaled up or down based on the demand.

2. **Consistent Environment**: Docker containers ensure that the application runs in the same environment throughout its lifecycle, from a developer's machine to production deployment.

3. **Resource Efficiency**: Containers are lightweight compared to VMs, as they share the host system's OS, instead of needing their own OS.

4. **Flexibility**: Kubernetes can run anywhere - on-premises, in public or private clouds, making it a versatile choice.

5. **Service Discovery and Load Balancing**: Kubernetes can expose a container using a DNS name or using their IP address. If traffic to a container is high, Kubernetes can load balance and distribute the network traffic to ensure the deployment is stable.

## Consequences

**Pros**:

- **Agility**: Faster deployments and rollbacks.
- **Isolation**: Containers encapsulate the application, minimizing interference and conflicts.
- **Cost-Effective**: Enhanced resource utilization leading to cost savings.
- **Community Support**: Kubernetes, being an industry standard, has a robust community and ecosystem.

**Cons**:

- **Complexity**: Initial setup and maintenance of a Kubernetes cluster can be complex.
- **Overhead**: For very small deployments, the overhead of Kubernetes might be an overkill.
