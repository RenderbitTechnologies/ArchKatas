# RoadWarrior Sequence Diagrams

## Introduction

We have envisioned some of the common user journeys in the platform and created sequnce diagrams for the same.

Please note that the user journeys listed here are not exhaustive, and are instead meant to be representative of a broad subset across the most commonly expected user journeys on the platform.

## Contents

- [User Registration and Account Management](#user-registration-and-account-management)
  - [Sign up for an account](#sign-up-for-an-account)
  - [Log into the account](#log-into-the-account)
  - [Edit user profile and preferences](#edit-user-profile-and-preferences)
  - [Log out of the account](#log-out-of-the-account)
- [Email Polling and Travel Email Detection](#email-polling-and-travel-email-detection)
  - [Configure the email for polling](#configure-the-email-for-polling)
  - [Poll the email for travel-related emails](#poll-the-email-for-travel-related-emails)
  - [Notify the user for detected travel emails](#notify-the-user-for-detected-travel-emails)
- [Interfacing with Travel Systems for Updates](#interfacing-with-travel-systems-for-updates)
  - [Fetch updated travel details from Sabre](#fetch-updated-travel-details-eg-delays-cancellations-gate-changes-from-sabre)
  - [Fetch updated travel details from Apollo](#fetch-updated-travel-details-eg-delays-cancellations-gate-changes-from-apollo)
  - [Manually sync the travel details](#manually-sync-the-travel-details-on-user-fetch)
- [Manual Reservation Management](#manual-reservation-management)
  - [Add a new reservation](#add-a-new-reservation)
  - [Update an existing reservation](#update-an-existing-reservation)
  - [Delete a reservation](#delete-a-reservation)
- [Grouping and Archiving Reservations](#grouping-and-archiving-reservations)
  - [Group reservations by trip](#group-reservations-by-trip)
  - [Archive completed trips](#archive-completed-trips)
  - [Manually archive a trip](#manually-archive-a-trip)
- [Social Media and Trip Sharing](#social-media-and-trip-sharing)
  - [Share trip on social media](#share-trip-on-social-media)
  - [Share trip with specific contacts](#share-trip-with-specific-contacts)
  - [Generate a public link for a trip](#generate-a-public-link-for-the-trip)
- [Integration with Travel Agency for Support](#integration-with-travel-agency-for-support)
  - [Report an issue with a reservation](#report-an-issue-with-a-reservation)
  - [Request immediate assistance](#request-immediate-assistance)
  - [Check status of a reported issue](#check-status-of-a-reported-issue)
  - [Provide feedback on support](#provide-feedback-on-support)
- [Analytics and Reporting](#analytics-and-reporting)
  - [Generate end-of-year summary reports](#generate-end-of-year-summary-reports)
  - [Fetch travel trends](#fetch-travel-trends)
  - [View hotel and airline preferences report](#view-hotel-and-airline-preferences-report)
  - [View cancellation and update frequency reports](#view-cancellation-and-update-frequency-reports)


## User Registration and Account Management

### Sign up for an account

![Sign up for an account](./diagrams/sequence-diagrams/01-user-registration-and-account-management/01-sign-up-for-an-account.png)
_Figure 1: Sign up for an account_

### Log into the account

![Log into the account](./diagrams/sequence-diagrams/01-user-registration-and-account-management/02-log-into-the-account.png)
_Figure 2: Log into the account_

### Edit user profile and preferences

![Edit user profile and preferences](./diagrams/sequence-diagrams/01-user-registration-and-account-management/03-edit-user-profile-and-preferences.png)
_Figure 3: Edit user profile and preferences_

### Log out of the account

![Log out of the account](./diagrams/sequence-diagrams/01-user-registration-and-account-management/04-log-out-of-the-account.png)
_Figure 4: Log out of the account_

## Email Polling and Travel Email Detection

### Configure the email for polling

![Configuring email for polling](./diagrams/sequence-diagrams/02-email-polling-and-travel-email-detection/01-configuring-email-for-polling.png)
_Figure 5: Configuring email for polling_

### Poll the email for travel-related emails

![Poll the email for travel-related emails](./diagrams/sequence-diagrams/02-email-polling-and-travel-email-detection/02-polling-email-for-travel-related-emails.png)
_Figure 6: Poll the email for travel-related emails_

### Notify the user for detected travel emails

![Notify the user for detected travel emails](./diagrams/sequence-diagrams/02-email-polling-and-travel-email-detection/03-notifying-user-of-detected-travel-emails.png)
_Figure 7: Notify the user for detected travel emails_

## Interfacing with Travel Systems for Updates

### Fetch updated travel details (e.g., delays, cancellations, gate changes) from Sabre

![Fetch updated travel details from Sabre](./diagrams/sequence-diagrams/03-interfacing-with-travel-systems-for-updates/01-fetching-travel-updates-from-sabre.png)
_Figure 8: Fetch updated travel details from Sabre_

### Fetch updated travel details (e.g., delays, cancellations, gate changes) from Apollo

![Fetch updated travel details from Apollo](./diagrams/sequence-diagrams/03-interfacing-with-travel-systems-for-updates/02-fetching-travel-updates-from-apollo.png)
_Figure 9: Fetch updated travel details from Apollo_

### Manually sync the travel details (on user fetch)

![Manually sync the travel details](./diagrams/sequence-diagrams/03-interfacing-with-travel-systems-for-updates/03-manual-travel-system-sync.png)
_Figure 10: Manually sync the travel details_

## Manual Reservation Management

### Add a new reservation

![Add a new reservation](./diagrams/sequence-diagrams/04-manual-reservation-management/01-adding-a-new-reservation.png)
_Figure 11: Add a new reservation_

### Update an existing reservation

![Update an existing reservation](./diagrams/sequence-diagrams/04-manual-reservation-management/02-updating-an-existing-reservation.png)
_Figure 12: Update an existing reservation_

### Delete a reservation

![Delete a reservation](./diagrams/sequence-diagrams/04-manual-reservation-management/03-deleting-a-reservation.png)
_Figure 13: Delete a reservation_

## Grouping and Archiving Reservations

### Group reservations by trip

![Grouping reservations by trip](./diagrams/sequence-diagrams/05-grouping-and-archiving-reservations/01-grouping-reservations-by-trip.png)
_Figure 14: Grouping reservations by trip_

### Archive completed trips

![Archive completed trips](./diagrams/sequence-diagrams/05-grouping-and-archiving-reservations/02-archiving-completed-trips.png)
_Figure 15: Archive completed trips_

### Manually archive a trip

![Manually archive a trip](./diagrams/sequence-diagrams/05-grouping-and-archiving-reservations/03-user-manually-archiving-a-trip.png)
_Figure 16: Manually archive a trip_

## Social Media and Trip Sharing

### Share trip on social media

![Sharing trip on social media](./diagrams/sequence-diagrams/06-social-media-and-trip-sharing/01-sharing-trip-on-social-media.png)
_Figure 17: Sharing trip on social media_

### Share trip with specific contacts

![Sharing trip with specific contacts](./diagrams/sequence-diagrams/06-social-media-and-trip-sharing/02-sharing-trip-with-specific-contacts.png)
_Figure 18: Sharing trip with specific contacts_

### Generate a public link for the trip

![Generating a public link for the trip](./diagrams/sequence-diagrams/06-social-media-and-trip-sharing/03-generating-a-public-link-for-the-trip.png)
_Figure 19: Generating a public link for the trip_

## Integration with Travel Agency for Support

### Report an issue with a reservation

![Reporting an issue with a reservation](./diagrams/sequence-diagrams/08-integration-with-travel-agency-for-support/01-reporting-an-issue-with-a-reservation.png)
_Figure 20: Reporting an issue with a reservation_

### Request immediate assistance

![Requesting immediate assistance](./diagrams/sequence-diagrams/08-integration-with-travel-agency-for-support/02-requesting-immediate-assistance.png)
_Figure 21: Requesting immediate assistance_

### Check status of a reported issue

![Checking status of a reported issue](./diagrams/sequence-diagrams/08-integration-with-travel-agency-for-support/03-checking-status-of-a-reported-issue.png)
_Figure 22: Checking status of a reported issue_

### Provide feedback on support

![Providing feedback on support](./diagrams/sequence-diagrams/08-integration-with-travel-agency-for-support/04-providing-feedback-on-support.png)
_Figure 23: Providing feedback on support_

## Analytics and Reporting

### Generate end-of-year summary reports

![Generating end-of-year summary reports](./diagrams/sequence-diagrams/07-analytics-and-reporting/01-generating-end-of-year-summary.png)
_Figure 24: Generating end-of-year summary reports_

### Fetch travel trends

![Fetching travel trends](./diagrams/sequence-diagrams/07-analytics-and-reporting/02-fetching-travel-trends.png)
_Figure 25: Fetching travel trends_

### View hotel and airline preferences report

![Viewing hotel and airline preferences](./diagrams/sequence-diagrams/07-analytics-and-reporting/03-viewing-hotel-and-airline-preferences.png)
_Figure 26: Viewing hotel and airline preferences_

### View cancellation and update frequency reports

![Viewing cancellation and update frequency](./diagrams/sequence-diagrams/07-analytics-and-reporting/04-accessing-cancellation-and-update-frequency.png)
_Figure 27: Viewing cancellation and update frequency_
