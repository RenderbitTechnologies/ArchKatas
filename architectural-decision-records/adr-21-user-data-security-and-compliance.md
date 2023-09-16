# ADR-21: User Data Security and Compliance

## Status

Adopted

## Context

With the global reach of our application and the sensitive nature of travel-related data, ensuring user data security is paramount. Moreover, entering European markets necessitates strict adherence to the General Data Protection Regulation (GDPR). Key decisions must revolve around encryption mechanisms for data at rest and in transit, as well as measures to ensure GDPR compliance.

**Encryption Mechanisms**:

- **Data in Transit**:
  - **TLS (Transport Layer Security)**: A widely adopted cryptographic protocol designed to provide secure communication across a computer network. Replaces the older SSL.
- **Data at Rest**:
  - **AES (Advanced Encryption Standard)**: A symmetric encryption algorithm widely regarded as secure and adopted by the U.S. government and other organizations globally.
  - **TDE (Transparent Data Encryption)**: Typically provided by database vendors, it ensures that data, such as entire files or databases, is encrypted and decrypted transparently.

**GDPR Compliance Measures**:

- **Data Minimization**: Only collecting and processing data absolutely necessary for the service.
- **Right to Access & Right to Erasure**: Building systems that allow users to access their data and request deletion.
- **Data Portability**: Providing means for users to obtain and reuse their personal data.
- **Privacy by Design**: Ensuring that data protection is included from the onset of designing systems, not an afterthought.
- **Data Breach Notification**: Establishing mechanisms to notify users and relevant authorities within 72 hours of detecting a data breach.

## Decision

- **Encryption**:
  - Adopt **TLS** for data in transit to ensure that any data exchanged between users and our systems remains confidential and tamper-proof.
  - Use **AES** for data at rest to ensure that stored data remains secure, even in the case of physical breaches.
- **GDPR Compliance**:
  - Implement **Data Minimization** principles across all data collection points.
  - Ensure system architecture supports the **Right to Access & Right to Erasure** by providing self-serve portal capabilities to users.
  - Adopt **Data Portability** measures, allowing users to export their data in a machine-readable format.
  - Ingrain **Privacy by Design** principles in the development lifecycle.
  - Develop protocols and systems for **Data Breach Notification** to ensure timely communication in the event of breaches.

## Consequences

**Pros**:

- **Enhanced Trust**: Users can trust our platform with their data, knowing it's secure and compliant.
- **Regulatory Adherence**: Avoidance of GDPR penalties and a smoother entry into European markets.
- **Business Reputation**: Maintaining a strong reputation as a secure and compliant service.

**Cons**:

- **Development Overhead**: Additional time and resources might be needed to implement and maintain the outlined measures, but this is seen as a necessary investment.
