# ADR-05: Cloud Provider Selection

## Status

Adopted

## Context

The trip management dashboard requires a highly available, scalable, and efficient cloud infrastructure. This system needs seamless integration tools, advanced analytics, and robust support. The three dominant players in the cloud service industry are:

- **[AWS (Amazon Web Services)](https://aws.amazon.com/)**: A highly comprehensive and broadly adopted cloud platform with a vast array of services.
- **[Azure](https://azure.microsoft.com/)**: Microsoft's cloud offering, integrated well with Microsoft's software products.
- **[Google Cloud Platform (GCP)](https://cloud.google.com/)**: Known for high-performance computing, machine learning tools, and open source technologies.

## Decision

[AWS (Amazon Web Services)](https://aws.amazon.com/) is chosen as the primary cloud provider for the trip management dashboard due to:

1. Market Leadership: AWS is the market leader with the most mature and feature-rich platform.
2. Extensive Service Catalog: AWS provides a broader range of services compared to its competitors.
3. Strong Developer Tools: AWS offers robust tools that can speed up development and deployment.
4. Global Reach: With 24 geographical regions and 77 availability zones, AWS provides vast coverage.
5. Integration Capabilities: AWS has pre-built integrations for many third-party applications/tools.
6. Security and Compliance: AWS has a broad set of security features and compliance certifications.

## Consequences

**Pros**:

- High Availability: Due to the vast network of data centers.
- Scalability: AWS services are designed to scale with application needs.
- Robust Ecosystem: Rich sets of tools, SDKs, and APIs for developers.
- Strong Community and Documentation: Given its market leader position, AWS has a vast user community and comprehensive documentation.

**Cons**:

- Cost Management: AWS's service richness can sometimes lead to complex pricing.
- Learning Curve: The vast array of services can be overwhelming to new users.
