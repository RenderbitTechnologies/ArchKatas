## ADR-13: Content Delivery Network (CDN)

### Status
Adopted

### Context
In our globally dispersed user base, it's imperative to ensure that content is delivered with minimal latency and high reliability. A Content Delivery Network (CDN) assists in achieving this by serving content from the closest edge location to the user. Three of the top contenders in the CDN space are:

1. **[Amazon CloudFront](https://aws.amazon.com/cloudfront/)**:
    - Integrated with AWS services, which we're leveraging for our infrastructure.
    - Extensive global presence with many edge locations.
    - Pay-as-you-go pricing with integrated AWS billing.

2. **[Akamai](https://www.akamai.com/)**:
    - One of the oldest and most extensive CDN networks.
    - Advanced security features and optimizations.
    - Typically entails contract-based pricing and might be overkill for startup-phase projects.

3. **[Cloudflare](https://www.cloudflare.com/)**:
    - Provides more than just CDN: includes security features, DDoS protection, and more.
    - Global network of data centers.
    - Pricing is based on a tiered model, including a free tier.

Our priorities involve smooth integration, cost efficiency, performance, and reliability.

### Decision
We have chosen **Amazon CloudFront** for the following reasons:

1. **AWS Integration**: Since we've decided on AWS as our primary cloud provider, CloudFront integrates seamlessly with our other AWS resources. This provides operational simplicity and consolidated billing.
2. **Global Reach**: With a vast number of edge locations worldwide, it ensures content is served with low latency, enhancing user experience.
3. **Cost Efficiency**: The pay-as-you-go model avoids upfront commitments and allows us to pay only for the content delivered.
4. **Security & DDoS Protection**: CloudFront, in conjunction with AWS Shield and WAF, provides robust security layers.

### Consequences
**Pros**:
- **Seamless AWS Integration**: Simplifies operations and management.
- **Scalability**: Can handle spikes in traffic without manual intervention.
- **Enhanced Performance**: Improves site loading times, offering a better user experience.

**Cons**:
- **Vendor Lock-in**: Further deepens our dependency on the AWS ecosystem.
- **Complex Pricing**: CloudFront's pricing can be intricate, especially when considering data out costs and regional variations.
