# ADR-27: User Notifications Strategy

## Status

Adopted

## Context

A robust user notification system is vital for a travel platform like ours, ensuring timely updates on booking statuses, promotions, and other relevant information. To deliver a seamless user experience, the choice of notification delivery methods must cater to the diverse preferences of users, providing them with relevant, timely, and actionable information without being obtrusive.

We weighed the following primary channels for user notifications:

1. **SMS (e.g., [Twilio](https://www.twilio.com/))**:
    - **Pros**:
        - Direct and immediate.
        - High open and read rates.
        - No need for internet access.
    - **Cons**:
        - Costs can accumulate rapidly with high usage.
        - Limited character space.
        - Might be seen as intrusive by some users.

2. **Push Notifications (e.g., [Firebase Cloud Messaging (FCM)](https://firebase.google.com/products/cloud-messaging))**:
    - **Pros**:
        - Instant delivery to user devices.
        - Can engage users even if they're not actively using the app.
        - Rich media capabilities (images, sounds).
    - **Cons**:
        - Users might disable them.
        - Overuse can lead to notification fatigue.

3. **Email (e.g., [SendGrid](https://sendgrid.com/))**:
    - **Pros**:
        - Detailed content delivery.
        - Can be personalized and segmented.
        - Archivable; users can reference them later.
    - **Cons**:
        - Slower open rates.
        - Risk of ending up in spam or promotions tab.
        - Relies on users checking their email.

The ideal solution should leverage the strengths of each channel, using them complementarily, based on the content's nature, urgency, and user preferences.

## Decision

Adopt a **hybrid approach** that integrates all three channels:

- Use **SMS** via providers like [Twilio](https://www.twilio.com/) for critical alerts, such as booking confirmations and urgent travel updates, where immediate attention is required.
- Employ **push notifications** via platforms like [Firebase Cloud Messaging (FCM)](https://firebase.google.com/products/cloud-messaging) for timely reminders, app-specific promotions, or in-app activity alerts.
- Rely on **email** platforms like [SendGrid](https://sendgrid.com/) for detailed communications, newsletters, promotional campaigns, and transaction summaries.

Third-party hosted service providers will be employed to ensure scalability, reliability, and feature-rich capabilities without overburdening our development and operational teams.

## Consequences

**Pros**:

- **Diverse Channels**: Cater to various user preferences and notification content types.
- **Scalability**: Using third-party services ensures we can handle volume spikes.
- **Engagement**: Effective use of notifications can lead to increased user engagement and retention.

**Cons**:

- **Management Complexity**: Multiple channels require more intricate management and segmentation strategies.
- **Cost**: Utilizing multiple channels, especially SMS, may have associated costs.
- **User Experience Balance**: Care must be taken not to overwhelm users with notifications, potentially leading to app uninstalls or opt-outs.
