# ADR-28: Feedback and Support System Integration Strategy

## Status

Adopted

## Context

For a travel platform, feedback and support systems are essential to gauge user satisfaction, collect feedback, address concerns, and provide timely customer support. The choice between developing an in-house solution or leveraging third-party platforms affects factors like development speed, feature set, scalability, and cost.

Here are the primary considerations for each approach:

1. **In-app Custom Solutions**:
    - **Pros**:
        - Total control over the user experience and feature set.
        - Tight integration with our internal systems.
        - No third-party subscription costs.
    - **Cons**:
        - Significant development and maintenance overhead.
        - Longer time to market.
        - Feature set might not be as extensive as established third-party platforms.

2. **Third-party Platforms (e.g., [Zendesk](https://www.zendesk.com/), [Intercom](https://www.intercom.com/))**:
    - **Pros**:
        - Fast implementation with proven platforms.
        - Robust set of features, with opportunities for customization.
        - Scalability and reliability provided by established providers.
    - **Cons**:
        - Monthly/annual subscription costs.
        - Limited control over data and user experience.
        - Potential difficulties in data migration if switching platforms.

Given our need for rapid deployment, a reliable support system, and a feature-rich experience for users and customer service reps, we evaluated the best third-party options.

## Decision

We decided to adopt [Zendesk](https://www.zendesk.com/) as our feedback and support system integration:

- **Comprehensive Toolset**: Zendesk offers a complete suite for support, including ticketing, chat, knowledge base, and community forums.
- **Integration Capabilities**: With its robust API and integrations, it can be seamlessly incorporated into our platform.
- **Customization & Branding**: It offers capabilities for customization to ensure our brand's consistency across all touchpoints.
- **Scalability**: As a travel platform, there could be spikes in support requests, especially during peak travel seasons. Zendesk is built to handle scale.

## Consequences

**Pros**:

- **Speed**: Rapid deployment without the overhead of development.
- **Reliability**: Leveraging a proven system means fewer bugs and issues.
- **Feature-rich**: Access to an array of features from day one.

**Cons**:

- **Cost**: Recurring costs associated with the subscription.
- **Data Control**: Some level of data will reside in third-party servers, though Zendesk does comply with global data privacy standards.
- **Customization Limitations**: While Zendesk offers a lot of customization, there might be constraints compared to a fully custom solution.
