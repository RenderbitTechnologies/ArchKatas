# ADR-09: Email Polling Strategy

## Status

Adopted

## Context

Our platform requires real-time data about users’ travel-related emails to help them manage reservations and updates efficiently. This necessitates an effective email polling strategy. There are various approaches, including:

1. **IMAP (Internet Message Access Protocol)**:
    - Designed for multiple devices, allowing emails to be stored on a mail server.
    - Provides mechanisms for syncing, searching, and flagging emails.
    - Supports better real-time notifications of new emails compared to POP3.
    - However, depending on email server configurations and limits, polling too frequently can lead to IP bans or rate limits.

2. **POP3 (Post Office Protocol version 3)**:
    - Designed to retrieve email from a remote server, and once retrieved, the email is deleted from the server.
    - Does not support multiple devices as seamlessly as IMAP.
    - Might not be a suitable strategy for our case, as it lacks real-time efficiency and continuous sync capabilities.

3. **Third-party Services (e.g., [Context.IO](https://context.io/))**:
    - Provides an abstraction layer on top of standard email protocols.
    - Manages email connections, authentication, and storage considerations.
    - Offers APIs to simplify integration, supporting real-time push notifications when emails arrive.
    - Reduces the effort needed in terms of infrastructure setup and maintenance.

Given our platform's requirements, which include real-time notifications, scalability, and the complexity of managing email connections and configurations, we had to decide on the most effective and efficient approach.

## Decision

We have chosen to employ **Third-party Services (specifically, Context.IO)** for the following reasons:

1. **Simplicity & Rapid Development**: Using services like Context.IO abstracts away the complexities of dealing with different email servers and configurations.
2. **Real-time Updates**: Provides push notifications for immediate information on incoming emails, crucial for the timely update of user reservations.
3. **Scalability**: Designed to handle large volumes of email data without the necessity for our platform to manage storage and server configurations.
4. **Security**: Trusted third-party services often have robust security measures in place, reducing our platform's exposure to vulnerabilities.
5. **Cost-Efficiency**: The reduced development effort and infrastructural requirements can lead to cost savings in the long run.

## Consequences

**Pros**:

- **Rapid Integration**: Allows for quicker time-to-market.
- **Efficient Real-time Processing**: Immediate notification of relevant emails.
- **Reduced Maintenance**: Offloads the need to manage and maintain email servers.

**Cons**:

- **Vendor Dependency**: Reliance on a third-party service introduces the risk of service discontinuations or changes in terms and pricing.
- **Data Privacy Concerns**: Using an external service requires trust that the vendor maintains high data privacy standards, especially when handling sensitive information.
- **Costs**: Though there can be cost savings in terms of development and maintenance, there will be recurring costs associated with using a third-party service.
