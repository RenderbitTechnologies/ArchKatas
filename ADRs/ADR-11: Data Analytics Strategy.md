## ADR-11: Data Analytics Strategy

### Status
Adopted

### Context
Given the nature of our platform, analyzing user travel trends, preferences, cancellations, updates, and more, is essential. This data can drive decisions and enhance user experiences. The challenge lies in managing and analyzing vast amounts of data efficiently. Our contenders are:

1. **[Apache Spark](https://spark.apache.org/)**:
    - An open-source distributed computing system.
    - Known for its fast data processing capabilities for large datasets.
    - Can run on various platforms, including Hadoop, Mesos, Kubernetes, and standalone clusters.
    - Supports multiple programming languages, including Java, Scala, Python, and R.
    - Offers libraries for data analysis, machine learning, graph analysis, and streaming.

2. **[Google BigQuery](https://cloud.google.com/bigquery)**:
    - A serverless, highly scalable, and cost-effective multi-cloud data warehouse.
    - Fully managed, with automatic backup, replication, and patching.
    - Integrates with Google Cloud's AI and ML tools.
    - Pricing is based on the amount of data processed, not storage or compute capacity.
    - Requires data to be stored in the Google Cloud environment, potentially causing vendor lock-in.

3. **[AWS Redshift](https://aws.amazon.com/redshift/)**:
    - A fully managed data warehouse service in the cloud.
    - Designed for online analytic processing (OLAP) and business intelligence tools.
    - Integrates with AWS's ecosystem.
    - Pricing is a combination of storage and the nodes provisioned.
    - Like BigQuery, it has the potential for vendor lock-in.

Given our focus on ensuring high flexibility, scalability, and avoiding vendor lock-in, we evaluated the technologies based on these critical aspects.

### Decision
We've chosen to go with **Apache Spark** for these reasons:

1. **Flexibility and Scalability**: Spark's distributed nature allows it to process large datasets efficiently, scaling horizontally as needed.
2. **Platform Agnostic**: Spark can run on various platforms, ensuring we're not tied to a specific vendor's infrastructure.
3. **Rich Ecosystem**: With libraries like Spark SQL, MLlib, and GraphX, we can harness various analytics tools under one umbrella.
4. **Language Support**: Being able to use Java, Scala, Python, and R provides flexibility in analytics tasks and potential integrations.
5. **Cost Efficiency**: Being open-source, we're only limited by the infrastructure costs, avoiding per-query costs that solutions like BigQuery impose.

### Consequences
**Pros**:
- **Versatility**: Spark is versatile and can handle batch processing, real-time data processing, machine learning, and more.
- **Community Support**: With a strong open-source community, getting support and updates is more assured.
- **Integration**: Easy to integrate with our chosen data storage and other systems.

**Cons**:
- **Operational Complexity**: Managing a Spark cluster may introduce operational overhead and complexity.
- **Resource Intensive**: Spark is resource-hungry, especially memory, which can affect costs if not managed well.
