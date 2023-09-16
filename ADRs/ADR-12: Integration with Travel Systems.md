## ADR-12: Integration with Travel Systems

### Status
Adopted

### Context
Travel systems are intricate, diverse, and, in many cases, built on legacy technologies. Ensuring our new platform interfaces seamlessly with these systems, like SABRE and APOLLO, is of paramount importance. Integrating such systems can be achieved through:

1. **Custom Connectors**:
    - Built from scratch, tailored specifically for the target system.
    - Allows maximum customization and performance tuning.
    - Requires extensive development, testing, and maintenance.

2. **Middleware Platforms**:
    - Platforms like [MuleSoft](https://www.mulesoft.com/) or [WSO2](https://wso2.com/) offer pre-built connectors and integration tools.
    - Provides an abstraction layer, simplifying integrations.
    - Eases maintenance, scalability, and ensures regular updates.
    - Involves costs, either in licensing or operational aspects.

Considering the requirement for speedy development, robustness, and our intention to reduce efforts on non-core development areas, the following assessments were made.

### Decision
We've opted for the **Middleware Platform** approach, specifically using a solution like **MuleSoft** or **WSO2** due to the following reasons:

1. **Quick Integrations**: Middleware platforms come with a range of pre-built connectors, drastically reducing integration times.
2. **Abstraction**: They abstract away the complexities of direct integrations, offering a simplified interface.
3. **Scalability & Maintenance**: Middleware platforms are built with scalability in mind and reduce the maintenance burden due to their vendor's regular updates.
4. **Flexibility**: As new travel systems emerge or we wish to integrate with additional platforms, middleware offers flexibility without starting from scratch.
5. **Error Handling & Monitoring**: Middleware platforms usually come equipped with robust error handling and monitoring capabilities.

### Consequences
**Pros**:
- **Rapid Development**: Speed up the integration process, allowing us to focus on core functionalities.
- **Unified Interface**: Provides a consistent approach to manage and monitor all integrations.
- **Future-proofing**: New connectors can be added as the ecosystem evolves, without overhauling existing integrations.

**Cons**:
- **Cost**: Using a middleware platform introduces licensing or operational costs.
- **Learning Curve**: While middleware abstracts complexity, there is an initial learning curve.
- **Overhead**: Introduces an additional layer, which can sometimes add latency or complicate debugging.
