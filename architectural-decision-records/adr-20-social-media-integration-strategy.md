# ADR-20: Social Media Integration Strategy

## Status

Adopted

## Context

In order to enhance the user experience on our platform and enable seamless sharing of trip information on various social media platforms, a decision has to be made between direct integration with social media platform APIs or leveraging third-party services like [Zapier](https://zapier.com/).

**Direct API Integration**:

- **Pros**: Greater control over integration, potentially more performant.
- **Cons**: Development-intensive, especially when connecting with multiple platforms, requires maintenance as APIs evolve, handling API rate limits for each platform, handling platform-specific errors.

**Third-party Services (e.g., Zapier)**:

- **Pros**: Faster development and deployment, integration with multiple services through a single point, somewhat insulated from direct API changes.
- **Cons**: Might introduce slight performance lags, reliant on third-party uptime.

## Decision

Considering our platform's need for rapid development, scalability in terms of integrating multiple platforms, and reducing maintenance overhead, we've opted to use **Third-party Services, specifically Zapier**, for our social media integrations. This choice was influenced by:

- **Development Efficiency**: Significantly faster to integrate with multiple platforms.
- **Scalability**: Easily add more platforms in the future.
- **Reduced Maintenance**: While still subject to third-party changes, the direct impact of individual social platform API changes is somewhat mitigated.

## Consequences

**Pros**:

- **Rapid Integration**: Can quickly add support for multiple social media platforms.
- **Flexibility**: Allows for easy addition of more platforms in the future.

**Cons**:

- **Slight Performance Lag**: Introducing an intermediary might add a minimal delay.
- **Dependency**: Reliance on third-party service uptime and potential costs.
