# ArchKatas

## O'Reilly Architecture Katas Summer 2023

This is a team submission for [O'Reilly Architecture Katas Summer 2023](https://learning.oreilly.com/featured/architectural-katas/).

### Team Members

- Soham Banerjee
- Shreya Pramanik
- Aditya Vikram Jajodia

## Contents

- [Introduction](#introduction)
- [Business Case](#business-case)
  - [Requirements](#requirements)
  - [Technical Constraints](#technical-constraints)
  - [Business Constraints](#business-constraints)
  - [Assumptions](#assumptions)
  - [High-Level Components](#high-level-components)
  - [Architectural Considerations](#architectural-considerations)
- [Architecture Characteristics](#architecture-characteristics)
  - [Driving Characteristics](#driving-characteristics)
  - [Implicit Characteristics](#implicit-characteristics)
  - [Others Considered](#others-considered)
- [Architecture Approach](#architecture-approach)
  - [Architecture Goals](#architecture-goals)
- [Context](#context)
  - [Actors](#actors)
  - [Use Cases](#use-cases)
  - [Event Storming](#event-storming)
- [Containers](#containers)
  - [Modular Monolith](#modular-monolith)
  - [Service Containers](#service-containers)
  - [API Layer](#api-layer)
- [Components](#components)
  - [Identity and Access Manager](#identity-and-access-manager)
  - [Profile Manager](#profile-manager)
  - [Connections Manager](#connections-manager)
  - [Rewards Manager](#rewards-manager)
  - [ETL Manager](#etl-manager)
  - [Reporting and Analytics Manager](#reporting-and-analytics-manager)
  - [Social Media API Manager](#social-media-api-manager)
- [Deployment](#deployment)
- [Cost Analysis](#cost-analysis)
- [Evaluation, Risks and Architecture Fitness](#evaluation-risks-and-architecture-fitness)
- [ADRs](#adrs)
- [References](#references)

## Introduction

A new startup wants to build the next generation online trip management dashboard to allow travelers to see all of their existing reservations organized by trip either online (web) or through their mobile device.

## Business Case

### Requirements

The provided requirements document is available [here](./requirements-specification.md).

### Technical Constraints

1. **Integration with Legacy Systems**: The solution must integrate with the existing travel systems like SABRE and APOLLO, which may have proprietary interfaces or limitations in terms of data access and response times.

2. **Response Times**: The web interface must respond within 800ms, and the mobile interface must have a first contentful paint under 1.4 seconds.

3. **Real-time Updates**: Updates from travel agencies and other systems need to be presented within the application within 5 minutes of generation.

4. **Uptime**: The system must guarantee 99.9833% uptime, which translates to not more than 5 minutes of unplanned downtime per month.

5. **Cross-Platform Interface**: A consistent and rich user interface must be provided across all deployment platforms, which may restrict technology choices and require additional development and testing.

6. **International Availability**: The system must function across different geographical regions, accounting for potential regional restrictions and data sovereignty issues.

7. **Email Polling**: The solution must interface with varied email systems to poll and extract travel-related information.

8. **Data Analytics**: The system must be capable of gathering and processing large amounts of analytical data from user trips.

### Business Constraints

1. **Privacy Concerns**: Sharing trip information on social media or with specific individuals can lead to potential privacy concerns, thus requiring robust data protection and privacy measures.

2. **Data Validity**: The system relies on the validity of external data from airline, hotel, and car rental systems, as well as data parsed from emails, which may not always be accurate or up-to-date.

3. **User Adoption**: With 15 million accounts, ensuring smooth user adoption and minimal disruption during transitions or updates is crucial.

4. **Regulatory and Compliance Issues**: Operating internationally brings along various regulatory and compliance requirements related to data storage, user privacy, and more.

5. **Monetization**: The startup nature of the project implies a need to eventually find revenue streams, which may not be initially clear, especially when prioritizing user adoption and experience.

6. **Preferred Travel Agency Integration**: While the system integrates with a preferred travel agency for quick problem resolution, any limitations or delays from this agency directly impact the service quality.

7. **Competitive Advantage**: The requirement to have better real-time updates than competitors places an ongoing need for monitoring, benchmarking, and improving system performance.

### Assumptions

1. **Data Access**: Assumption that existing systems like SABRE and APOLLO will provide necessary access to data and interfaces required for real-time integration.

2. **User Behavior**: Assumption that users will be proactive in providing access to their emails for polling and will actively use the system for manual updates and trip management.

3. **Uniformity of Data**: Assumption that travel-related emails follow certain patterns or templates that can be reliably identified and parsed.

4. **Network Reliability**: Assumption that there will be consistent and reliable internet connectivity for real-time updates.

5. **Data Analytics Readiness**: Assumption that the data gathered will be readily usable for analytics, trend predictions, and reporting without significant data cleansing or transformation.

6. **Security Protocols**: Assumption that integrating with third-party systems (like travel agencies and social media platforms) will not pose significant security risks or vulnerabilities.

7. **User Base Growth**: Assuming a gradual growth in the active user base, which will allow the system to scale appropriately without sudden, unplannable spikes in demand.

### High-Level Components

- **Web Frontend:** A responsive web application built with modern frameworks like React or Angular.
- **Mobile App:** Native or cross-platform apps (like Flutter) to ensure optimal performance and UX.
- **Backend API:** RESTful/GraphQL APIs built with technologies such as Node.js or Spring Boot to serve both the web and mobile clients.
- **Database:** A distributed database system like Cassandra for scalability, combined with a relational DB like PostgreSQL for structured data.
- **Email Poller Service:** A separate service dedicated to pulling emails, filtering them, and feeding travel-related emails into the main system.
- **Travel Interface Connector:** To connect with systems like SABRE, APOLLO. This will regularly fetch and push updates.
- **Social Media Integrator:** For sharing trip details on social media platforms.
- **Data Analytics Service:** For processing, analyzing, and reporting user trip data.

### Architectural Considerations

- **Scalability and Cloud Platform:** Given the projected growth rate, we'll require a cloud platform that offers the ability to scale resources up and down with ease. AWS, Google Cloud, and Azure are all great options. Given the international nature of the app, we might choose AWS due to its more extensive global data center presence.
- **Latency and Data Centers:** We'd leverage AWS data centers in North America (US West and US East) and Western Europe (Frankfurt, London, or Paris) to reduce latency for primary markets. This might involve setting up multi-region deployments.
- **Content Delivery Network (CDN):** To further reduce latency and provide quick static content delivery to users worldwide, we'll use a CDN like Amazon CloudFront.

## Architecture Characteristics

The following section highlights the salient architecure characteristics we consider crucial to a successful implementation of the system.

### Driving Characteristics

| Characteristics | Rationale                                                                                     | Whether Top 3? |
|-----------------|-----------------------------------------------------------------------------------------------|----------------|
| **Scalability** | With 15 million user accounts and 2 million active users/week, the system needs to handle high traffic and user data. | Yes            |
| Portability     | As an international system, it must operate across different regions and networks.            | No             |
| Upgradeability  | To remain competitive and relevant, the system should be able to incorporate new features or updates easily.  | No             |
| **Extensibility** | Given integrations with various travel systems and potential future platforms, the architecture must be extensible. | Yes            |
| **Performance** | Fast response times are needed for both web and mobile, ensuring user satisfaction.          | Yes            |
| Availability    | With a max of 5 minutes of unplanned downtime per month, the system requires high availability.  | No             |

### Implicit Characteristics

#### Security

We are transmitting and maintaining user's personal data such as their emails, phone numbers and locations over the web. The data needs to be secured in transit and at rest using appropriate encryption mechanisms. Also, there is need for data de-identification mechanisms and zero-trust verification policies when data needs to be accessed by the development team, admistrative users or other business stakeholders.

#### Usability

The system is meant to accessed via mobile apps primarily by non-technical users. The need for it to be intuitive and usable is implicit.

#### Cost

The system needs to be cost-effective as it needs to support millions of users with a high throughput and concurrent user load.

### Others Considered

#### Reliability

As the system is mission critical, and cost of downtime is high, it needs to be highly reliable to serve it's existing user base and onboard new ones without service interruptions.

#### Recoverability

In case of service downtime, the system needs to be able to recover in a consistent state.

## Architecture Approach

1. **Decoupled Microservices Architecture**

    Given the requirement for scalability, especially with a potential of 2 million active users a week and the need to process real-time updates from various external systems, a microservices architecture offers decoupled services that can individually scale based on demand. For instance, the service handling email polling might be scaled differently from the service managing travel updates.

2. **Event-Driven Design**

    Considering the need for real-time updates and interactions between multiple components, adopting an event-driven design allows the system to react to changes and updates efficiently. It aids in ensuring updates are presented in the app within the desired 5-minute timeframe.

3. **Cloud-Native Deployment**

    To ensure high availability and meet the technical requirements of max 5 minutes unplanned downtime per month, a cloud-native deployment approach on platforms like AWS, Azure, or GCP would be pursued. These platforms provide the necessary tooling and infrastructure to ensure high availability, backups, and disaster recovery.

4. **Integration Gateways**

    Given the need to integrate with various external systems like SABRE, APOLLO, and social media platforms, dedicated integration gateways would be set up. These gateways would handle the specifics of communicating with each external system, offering a consistent interface to the internal components.

5. **Data Lakes for Analytics**

    Considering the analytical requirements and trend analysis, a data lake approach would be used to store raw data from various sources. This allows for efficient big data processing and ensures that analytical processes don't impact the operational efficiency of the system.

6. **Global Content Delivery & Data Localization**

    Given the international user base, a CDN (Content Delivery Network) approach would ensure that static content is delivered fast across the globe. Simultaneously, data localization strategies would be employed to ensure compliance with international data laws.

### Architecture Goals

1. **Scalability**: The architecture should support the platform's growth in terms of user numbers, data volume, and processing demands. It should effectively handle the demands of 2 million active users/week and beyond.

2. **Resilience & Availability**: With a technical requirement of max 5 minutes unplanned downtime per month, the system should be designed with redundancy, failovers, and quick recovery mechanisms.

3. **Integration Flexibility**: With many external systems to integrate with, the architecture should provide a flexible and maintainable approach to integrations. This ensures long-term viability even when external systems evolve or change.

4. **Data Security & Privacy**: Given the sensitive nature of travel data and the need to poll users' emails, the system should prioritize data security and user privacy, aligning with GDPR and other global data protection standards.

5. **Operational Efficiency**: To ensure updates within 5 minutes and web response times within 800ms, the system's operational efficiency is paramount. Efficient data pipelines, optimized databases, and streamlined processing are essential.

6. **Extensibility**: As user needs evolve and new features or integrations are required, the architecture should support easy extensibility without major overhauls. This includes the potential for future monetization strategies or new analytical insights.

7. **User Experience Focus**: With a requirement for a rich user interface across all platforms, the architecture should support seamless user experiences, fast load times, and intuitive interactions.

### A discussion regarding architecture characteristics and microservices

Figure 1 shows how our top 3 architecture characteristics score against formal system architecture styles.

![characteristics](/Diagrams/characteristics.png)
*Figure 1 Architecture Characteristics*

- It is incidental that the architectural styles we have chosen have scored the highest number of stars against the top 3 chosen characteristics.
- Even though Microservices score low on performance, which is one of our top 3 characteristics, we still primarily use Microservices as part of our proposed system architecture. The reason for that is, this performance penalty is applicable to the entire system comprising of independent Microservices, because of the inherent latency introduced by network IO and transaction management in a distributed system. The performance penalty however does not apply to individual microservices, in cases where one service has much higher performance requirements than others. In such cases it makes sense to isolate the performance critical functionality into a micro service that might serve a much higher number of requests compared to the rest of the system. This is the approach we take to mitigate this overall performance penalty.
- Microservices are inclusive of the other event driven and serverless architecture styles for the following reasons

1. Event driven architecture is really about message based asynchronous communication between components of the system. Nothing about Microservices prohibits us from using both synchronous and asynchronous components and communication mechanisms for the same service.
2. Serverless architectures are really about stateless microservices. Microservices can be deployed on a serverless platform with the caveat that the services themselves be containerised & stateless applications.

## Context

We start modelling the architecture of the system by envisioning the entire system as a black box. The Context model identifies all external actors and their interactions with the system.

### Actors and Use Cases

The users of the application fall into 2 categories. The public users will interact with the system using a mobile app, while the administrative and organisational use cases are more back end related, like data upload and ETL, reporting etc. Admin/Org users will interact with the system through a web based dashboard.

![blackBox](/Diagrams/blackbox.png)
*Figure 2 Use Cases*

### Event Storming

The next step is zooming into the black box. The prerequisite to our goal of modelling the system as a set of independent microservices is to start with domain partitioning. To accomplish this we used the event storming process.
Event-storming begins with initially identifying "Domain Events". A Domain event is something that happens within the system. It is described by a ubiquitous language entity followed by a verb or action on that entity. Each use case in Figure 2 maps to one or more domain events shown here. As per the process, we identify as many domain events as we can and put each one on an orange sticky note on a virtual whiteboard.

![Ad-Hoc Domain Events](/Diagrams/domainEvents.png)
*Figure 3 Domain Events*

Subsequently we identify the commands that trigger these domain events. While a domain event is something that happens within the system, the command is the action that triggers a series of domain events. Commands invoked by external actors are explicitly identified. Certain commands do not have an associated actor, which implies that it was invoked internally within the system. We organise the related sets of commands  and domain events together into sets of related aggregates.
![adding commands](/Diagrams/commandsAndActors.png)
*Figure 4 Commands, Actors and Aggregates*

Next we determine the automation policies for the commands that do not have an associated external actor and are triggered when a certain domain event completes. The automation policies indicate asynchronous communication coupling between the bounded contexts. Grouping the semantically related aggregates together gives us the bounded contexts and the blueprint for individual microservices.
![bounded contexts](/Diagrams/automationPolicies.png)
*Figure 5 Automation Policies and Bounded Contexts*

The above diagram gives us the boundaries of our bounded contexts and the event driven connections between them

## Containers

### Modular Monolith

The event storming process described in the previous section allowed us to identify the bounded contexts of our system and the aggregates (components) within them. We now map each bounded context to be a module of our overall system. The resulting modular monolith is depicted in the following diagram.
![Modular Monolith](/Diagrams/modmono.png)
*Figure 6 Modular Monolith*

### Service Containers

The previous section described a single container, comprising of multiple modules. It did not give us any information about how the modules are coupled. The next step therefore is to segregate the container along the boundaries of our bounded contexts. The following diagram illustrates the the interactions between the various microservices and the external actors.

**Note**
Synchronous communication coupling between the services is omitted from this diagram for clarity, but it is shown in figure 9 and discussed in the related section

![Service Containers](/Diagrams/containers.png)
*Figure 7 Service Containers*

### API Layer

Next, we add an API layer to extract the publically accessible interface of the system. Instead of external users directly connecting to the individual services via a GUI, all external requests will be routed through the API layer. Also see [ADR04-API-layer](/ADRs/ADR04-API-Layer.md)

![API Layer](/Diagrams/apiLayer.png)
*Figure 8 API Layer*

**Note**
In the above diagram, the API layer only serves requests from public mobile-app based clients. This is on purpose, the administrative/organizational users will make up a small fraction of the total user base of the system. Their use cases are also different from reqular users, thus it makes sense for them to have separate APIs for accessing relevant services. Identity, access control and authentication mechanisms for administrative users are also significantly different from those of public users who do not have access to internal infrastructure, data and services.

### Coupling and Architecture Quanta

Finally we close out the service containers section with a discussing of coupling between the services and architecure quanta.

The previous diagram showed 8 distinct containers including the API layer.
Since the API layer is simply a proxy, it does not include any domain specific functionality or perform any workflow orchestration, we can omit it from this section.

The following diagram illustrates how the remaining services are coupled, that databases they own or share, and the domain entities in those databases.

![quanta](/Diagrams/quanta.png)
*Figure 9 Coupling and Quanta*

**Static Coupling**

- The ETL service and the Rewards Manager microservice are statically coupled through a shared database. We could make a case for separating transactions from master data into two separate databases, where ETL only writes to the master database and Rewards manager only reads from it as shown in the diagram. This however does not do much to reduce the contract coupling introduced by shared data they have to work with. The diagram shows to separate databases for clarity and semantic reasons

**Dynamic Coupling**

- The Profile service synchronously requests data from IAM service
- The Rewards and Connections services synchronously requests data from the Profile service
- The Profile service asynchronously ingests messages/events from Rewards and Connections services
- The Reporting and analytics service asynchronously ingests messages/events from the Profile service

The Social Media API does not depend upon any other services, it is invoked directly from admin dashboards. It is in a sort of middle ground, where it’s trivial enough not warrant it’s own Microservice, but semantically it does not make sense to make it part of other services we have defined.

Given the shared database between the ETL and Rewards service, the system architecure has a quanta of 6, illustrated by the dashed lines in the above diagram.

## Components

The following section describes the internal components of each microservice identified the previous section

### Identity and Access Manager

The **Identity and Access Manager (IAM)** plays a critical role in managing and securing access to resources within a system architecture. IAM is a crucial component of cybersecurity and ensures that only authorized users and entities can access the system's resources while maintaining the principle of least privilege. Here are the key responsibilities and functions of an Identity and Access Manager within a system architecture:

**User Identity Management:**

- Create and manage user accounts: IAM administrators create, update, and deactivate user accounts as needed.
- Maintain user profiles: IAM ensures that user profiles are accurate and up-to-date, reflecting each user's role and permissions.

**Authentication:**

- Implement authentication mechanisms: IAM manages the authentication process, which verifies the identity of users and entities trying to access the system. Common methods include passwords, multi-factor authentication (MFA), and biometrics.
- Secure authentication tokens: IAM ensures that authentication tokens (e.g., session cookies) are secure to prevent unauthorized access.

**Authorization:**

- Define access control policies: IAM administrators create and enforce access control policies that determine who can access what resources and under what conditions.
- Role-based access control (RBAC): IAM often implements RBAC, where users are assigned roles with specific permissions based on their job functions.
- Fine-grained access control: IAM may also support more granular access control policies, allowing for precise control over resource access.

**Access Provisioning and Deprovisioning:**

- Automate user provisioning: IAM can automate the process of granting access to new users, ensuring they have the necessary permissions from the start.
- Deactivation and deprovisioning: When users leave the organization or no longer require access, IAM ensures that their accounts and permissions are promptly revoked.

**Audit and Compliance:**

- Logging and monitoring: IAM logs user activities and access attempts for auditing purposes, helping organizations maintain compliance with security regulations.
- Compliance enforcement: IAM can enforce compliance policies and ensure that access control measures align with regulatory requirements.

**Single Sign-On (SSO):**

- Provide SSO capabilities: IAM can enable SSO solutions, allowing users to access multiple applications with a single set of credentials, enhancing user convenience and security.

**Password Management:**

- Password policies: IAM enforces password policies, such as complexity requirements and password rotation, to enhance security.
- Password reset and recovery: IAM often provides self-service mechanisms for users to reset or recover their passwords securely.

**Access Reviews:**

- Periodic access reviews: IAM may facilitate periodic reviews of user access rights to identify and address any unauthorized or unnecessary permissions.

**Security Integration:**

- Integration with security tools: IAM systems often integrate with other security solutions, such as intrusion detection systems and SIEM (Security Information and Event Management) platforms, to enhance overall security posture.

![IAM](/Diagrams/IAM.png)
*Figure 10 Identity & Access Manager*

### Profile Manager

The profile manager is responsible for creating and maintaining the public profile for all users. Once an account is provisioned and the user logs in, a default profile automatically created and the user is directed to update it.
The service encapsulates a query based CRUD component to make the profile changes requested by the user.
Besides this, we also apply profile updates that happen due to various events triggered within the system as a result of user actions. See [ADR05-CQRS-EventSourcing](/ADRs/ADR05-CQRS-EventSourcing.md)

![Profile Manager](/Diagrams/profile.png)
*Figure 11 Profile Manager*

### Connections Manager

The connection manager is the most intricate part of the system. The need for it to be horizantally scalable is crucial given the amount of real time connections and requests it will handle at scale from all over the United States.
In our proposed architecture, each instance of the Connections manager service will serve requests from multiple zip codes.
The service itself comprises of an Orchestrator component and a message processor. The Orchestrator keeps track of free and busy websocket connections by getting notifications from the Message Processor.

![Connections Manager](/Diagrams/connection.png)
*Figure 12 Connections Manager*

The following sections describes the overall workflow, the differences between how the server and app handle citizen and officer requests should be noted

**Location Tracking**

- Officer turns on location services and makes themselves available for connection within a 15 minute window via the client app
- App makes a GET request recieved by the orchestrator component on behalf of the officer. The request must include officer's current geolocation (Lat,Long),zipcode and sufficent information to uniquely identify the account and profile (AccountID, ProfileID). If the zipcode is not included in the request, the server will be responsible for mapping the geolocation to a zip code
- Orchestrator determines the request is coming from an officer (separate endpoints for officer and citizen is one way of achieving this)
- Orchestrator responds with the url of a free connection websocket connection
- Orchestrator creates a record of a busy connection in it's local database of a tuple comprising the websocket url and the Officer's profile ID
- App on the Officer's device establishes a websocket connection to the url provided in the previous step.
- App sends the officer's location over the websocket connection whenever it detects a location change from the location services
- Message processor stores and updates the the location of the officer in a geolocation clustered, in-memory graph database [ADR06](/ADRs/ADR06-InMemory-Graph-Store-For-location-lookup.md)
- App on citizen device makes a GET request recieved by the orchestrator component when it detects a location change. The request must include citizen's current geolocation (Lat,Long),zipcode and sufficent information to uniquely identify the account and profile (AccountID, ProfileID). If the zipcode is not included in the request, the server will be responsible for mapping the geolocation to a zip code
- Orchestrator determines the request is coming from an citizen (separate endpoints for officer and citizen is one way of achieving this)
- Orchestrator responds with the url of a free connection websocket connection
- Orchestrator creates a record of a busy connection in it's local database of a tuple comprising the websocket url and the Citizen's profile ID
- App on the Citizen's device establishes a websocket connection to the url provided in the previous step.
- App sends location updates to the server over the websocket connection, message processor looks up the location of the closest police officer from the in-memory graph store and sends it over the same connection, along with other relevant profile data.
- The message processor is responsible for removing the officer's location from the in-memory cache once the app notifies with a message. Once the 15 minute window expires the websocket connection is closed and the orchestrator is notified. Orchestrator removes the tuple it added earlier from it's local db.

The workflow described above is illustrated in the following sequence diagram

![connectionWorkflow](/Diagrams/connectionSeq.png)
*Figure 13 Connection Workfkow*

**Proximity Detection**
Proximity detection can happen in of two ways

1. Bluetooth based proximity detection, similar to how Covid Tracking apps work
2. Calculating proximity on the server

Bluetooth based proximity detection does not require a constantly sending and recieving location updates from the web server. APIs for background services exist on both Android and iOS, that can run even when the app is closed and send notifications to the user (See the next section about handling notifications). Such services can be programmed to periodically check for nearby bluetooth devices and obtain their bluetooth UUID. This UUID can then be sent to the server to determine if the device has the app installed and request the profile of the associated user. This will also require the user profiles or accounts on the server to be mapped to the UUIDs, and keep them updated, since UUIDs can be randomly generated.

The other method is to calculate proximity on the server and then allow the citizen to request a connection when they are within the threshold. There are a couple of benefits to this latter approach

1. User's bluetooth need not be on at all times
2. Since both officer and citizen geolocations are being tracked, they can be rendered on a map, enhancing usability. The will not be possible with device detected proximity

As mentioned earlier, we proposed using graph data structures to store and lookup officer locations on the server. Using graphs makes proximity calculation faster when compared to a table based lookup at the expense of lower performance when adding or removing locations from the graph.

![latlonggraph](/Diagrams/latlongGraph.png)
*Figure 14 Geolocation Graph*

**Handling Notifications**
Our architecture recommends using device triggered notifications along with server pushed notifications (See  [ADR07-Device trigerred notifications](/ADRs/ADR07-Device-triggered-notifications.md)).
The relevant classes for background services are subclasses of UNNotificationTrigger (swift) on iOS and the Service (java) class on Android.

**Establishing Connection**
Once a citizen is notified they are close to an officer accepting connections, they can request a connection via the App UI, which triggers another Http request to the orchestrator. The orchestrator sends a notification to the officer's device either through a cloud based messaging service, or through the open websocket channel. If the officer accepts, the app requests the Orchestrator to register a successful connection and put an event on the "Established connections" topic.

### Rewards Manager

The Rewards manager is responsible handling point redemptions and donations by Citizens and Officers respectively.
The service intially serves the data for the views where the users can make these transactions. The Storefront offers, municipal schemes and Charity views are made available to users on the app, the users can then choose how they may use the points they have accrued by making connections.
Whenever a points transaction is recorded, a representation of the event is put into the outbound channel to be consumed by the profile manager to update the relevant user profiles. The event itself may include data about the nature of the transaction along with discounts or schemes that were availed, coupons or vouchers generated as part of the transaction.
![Rewards Manager](/Diagrams/rewards.png)
*Figure 15 Rewards Manager*

### ETL Manager

The ETL manager is a relatively straightforward part of the system, it is only meant to be used by administrative users to upload the organizational data related to Retailers (storefronts,discounts), Municipalites (municipal points related schemes) and Charities. Another possible use case for ETL could be bulk loading Officer accounts and profile data from precinct IT departments, so individual officers don't need to do it themselves.
As such the ETL manager encapsulates connectors for incoming data sources, and rules for data sanitization and validation

![ETL Components](/Diagrams/etl.png)
*Figure 16 ETL Manager*

### Reporting and Analytics Manager

The purpose of reporting and analytics is to maintain a data warehouse on which it may perform dimension based (temporal, geographical) analytics and report generation. It therefore contains OLAP querying components as well as jobs to run aggregation and report generation tasks.
Our architecture includes an event stream from the profile manager to be consumed be Reporting and Analytics that allows it to have the latest conections and rewards related data, along with profile attributes of related users available for analysis and reporting . See [ADR05-CQRS-EventSourcing](/ADRs/ADR05-CQRS-EventSourcing.md)

![Reporting and Analytics](/Diagrams/reporting.png)
*Figure 17 Reporting and Analytics*

### Social Media API Manager

Most social media platforms allow posting data through REST based APIs. The social media API manager encapsulates the client libraries for the APIs of the platforms where Hey Blue! does it promotion. Third party tools such as Zapier provide social media workflow integration out of the box, in which case the service would encapsulate the the relevant third party client libraries instead

![Social Media API](/Diagrams/social.png)
*Figure 18 Social Media API Manager*

## Deployment

The next diagram models a sample deployment of the Hey Blue! system on the Google Cloud Platform. A brief overview of the involved GCP services follows, along with other major cloud alternatives

![gcp](/Diagrams/gcp.png)
*Figure 19 GCP Deployment Architecture*

Cloud Run is GCP’s default server less product. It is meant for deploying containerized applications with support for horizontal scaling, load balancing and maintenance of minimum active instances in a fully cloud managed Kubernetes Cluster. In the model, cloud run is used for deploying the Connections, Profile and Rewards microservices along with the administrative dashboard application.

- Microsoft Cloud Alternative: Azure Container instances
- Amazon Cloud Alternative: AWS Lambda

The API gateway allows registration of endpoints for services deployed on GCP (such as Cloud Run) and allows authentication, routing, monitoring, alerting, logging, and tracing of calls to registered services. The API gateway can authenticate requests via the Firebase authentication service, which can completely stand in for the IAM service described in our architecture.

- Microsoft Cloud Alternative: Azure Application Gateway
- Amazon Cloud Alternative: AWS API Gateway

The Pub/Sub service allows asynchronous, low latency message based communication between deployed services. We can use Pub/Sub to implement event queues and topics for async inter-service communication

- Microsoft Cloud Alternative: Azure Service Bus and related products
- Amazon Cloud Alternative: Amazon SQS

BigQuery is GCPs big data analytics and machine learning platform. It allows ingesting event streams directly from Pub/Sub.

- Microsoft Cloud Alternative: Azure Synapse analytics, HDInsight
- Amazon Cloud Alternative: AWS Redshift

Cloud Data Fusion is GCPs most basic ETL service that provides support for pre-built as well as custom transformations and connectors that should suffice for most ETL use cases.

- Microsoft Cloud Alternative: Azure Data Factory
- Amazon Cloud Alternative: AWS ETLeap, AWS Glue

## Cost Analysis

Actual cost of cloud services depends on implementation specific details such as network ingress/egress, CPU and memory usage etc, it can only be determined after building and staging the services on the clould platform.

An estimated Google Cloud cost analysis per month for 50000 Monthly active Users follows, obtained by pricing calculators for individual services

API gateway - 3000 calls per month per user
$3 per million calls *((50000*3000)/1000000) = $450

Cloud Run
~$50 * 20 Instances  - ~$1000 per month

Cloud SQL
.035/GB/Hr *24 hrs* 30 days * 50 GB -   $1260

Pub/Sub Lite
(Throughput 1MBPS min/5 MBPS Max) with 1 day of storage  - ~$70 per month

Total Estimated Cost per month 450 + 1000 + 1260 = $2780

## Evaluation, Risks and Architecture Fitness

This final section is a discussion of how the proposed architecture adheres to the initially chosen driving characteristics, the associated trade-offs and risks. It highlights the areas that must be continuosly be tested and evaluated against benchmarks through fitness functions, ideally as part of the CI/CD pipeline.

*Evaluating the architecture against driving caharacteristics*

- Scalability - Domain functionality with high scalability requirements are isolated into stateless microservices. The Connections service is meant to be the most compute intensive, serving higher traffic than others, it is therefore designed to be stateless with no associated persistent data store. Fitness tests for scalability will involve running tests against staging clusters with simulated web traffic
- Performance - We mitigate network latency related performace issues with effective domain partitioning of data and services and avoiding distributed transactions. Individual services can be tested and benchmarked for perfomance
- Extensibility - The combination of Microservices, event driven communication and serverless depolyment lends itself well to an extensible architecture, allowing new components and services to be introduced to serve additional requirements and use cases. However, it is difficult to test a system for extensibilty, strict adherence to loose coupling and high cohesion between components is needed.

*Risks*

- Databases could be a bottleneck to horizontal scalability. Serverless database services/tools, sharding and replication services/tools are possible mitigation strategies
- Testability of event driven workflows involving multiple services. Tests for individual microservices will also need to include comprehensive cases for distributed workflows

## ADRs

[ADR-01: Frontend Framework Selection](/ADRs/ADR-01%3A%20Frontend%20Framework%20Selection.md)
[ADR-02: Mobile Development Strategy](/ADRs/ADR-02%3A%20Mobile%20Development%20Strategy.md)
[ADR-03: Backend Development Framework Selection](/ADRs/ADR-03%3A%20Backend%20Development%20Framework%20Selection.md)
[ADR-04: API Strategy Selection](/ADRs/ADR-04%3A%20API%20Strategy%20Selection.md)
[ADR-05: Cloud Provider Selection](/ADRs/ADR-05%3A%20Cloud%20Provider%20Selection.md)
[ADR-06: Multi-Region Deployment Strategy](/ADRs/ADR-06%3A%20Multi-Region%20Deployment%20Strategy.md)
[ADR-07: Database Selection Strategy](/ADRs/ADR-07%3A%20Database%20Selection%20Strategy.md)
[ADR-08: Database Replication Strategy](/ADRs/ADR-08%3A%20Database%20Replication%20Strategy.md)
[ADR-09: Email Polling Strategy](/ADRs/ADR-09%3A%20Email%20Polling%20Strategy.md)
[ADR-10: Message Broker & Event System Strategy](/ADRs/ADR-10%3A%20Message%20Broker%20%26%20Event%20System%20Strategy.md)
[ADR-11: Data Analytics Strategy](/ADRs/ADR-11%3A%20Data%20Analytics%20Strategy.md)
[ADR-12: Integration with Travel Systems](/ADRs/ADR-12%3A%20Integration%20with%20Travel%20Systems.md)
[ADR-13: Content Delivery Network (CDN)](/ADRs/ADR-13%3A%20Content%20Delivery%20Network%20(CDN).md)
[ADR-14: Authentication Strategy](/ADRs/ADR-14%3A%20Authentication%20Strategy.md)
[ADR-15: Monitoring & Logging Strategy](/ADRs/ADR-15%3A%20Monitoring%20%26%20Logging%20Strategy.md)
[ADR-16: Deployment Strategy](/ADRs/ADR-16%3A%20Deployment%20Strategy.md)
[ADR-17: CI CD Strategy](/ADRs/ADR-17%3A%20CI%20CD%20Strategy.md)
[ADR-18: Testing Strategy](/ADRs/ADR-18%3A%20Testing%20Strategy.md)
[ADR-19: Scaling Strategy](/ADRs/ADR-19%3A%20Scaling%20Strategy.md)
[ADR-20: Social Media Integration Strategy](/ADRs/ADR-20%3A%20Social%20Media%20Integration%20Strategy.md)
[ADR-21: User Data Security and Compliance](/ADRs/ADR-21%3A%20User%20Data%20Security%20and%20Compliance.md)
[ADR-22: Backup and Disaster Recovery](/ADRs/ADR-22%3A%20Backup%20and%20Disaster%20Recovery.md)
[ADR-23: Cost Management Strategy](/ADRs/ADR-23%3A%20Cost%20Management%20Strategy.md)
[ADR-24: Load Balancing](/ADRs/ADR-24%3A%20Load%20Balancing.md)
[ADR-25: Caching Mechanism](/ADRs/ADR-25%3A%20Caching%20Mechanism.md)
[ADR-26: Content Management System](/ADRs/ADR-26%3A%20Content%20Management%20System.md)
[ADR-27: User Notification System](/ADRs/ADR-27%3A%20User%20Notification%20System.md)
[ADR-28: Feedback and Support System Integration](/ADRs/ADR-28%3A%20Feedback%20and%20Support%20System%20Integration.md)
