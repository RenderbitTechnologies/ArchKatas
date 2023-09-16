# ADR-14: Authentication Strategy

## Status

Adopted

## Context

Providing a secure and user-friendly authentication system is of utmost importance for our platform. Users should have a seamless experience whether they're accessing our platform for the first time or returning. We considered the following primary authentication mechanisms:

1. **[OAuth2.0/OpenID](https://openid.net/connect/)**:
    - **OAuth2.0** is an authorization framework that allows third-party applications to obtain limited access to user accounts on an HTTP service.
    - **OpenID Connect** (OIDC) is an identity layer on top of the OAuth 2.0 protocol, providing authentication.

2. **[JWT (JSON Web Tokens)](https://jwt.io/)**:
    - It's a compact, URL-safe means of representing claims to be transferred between two parties.
    - Used in authentication and authorization protocols, including OAuth 2.0 and OIDC.

3. **SSO (Single Sign-On) Solutions**:
    - Allows users to log in once to provide access to multiple applications and services.
    - Crucial for corporate users or integrated platforms to provide a seamless authentication experience.

For our application, balancing security, user experience, and integration capabilities is essential.

## Decision

We have opted for a combination of **OAuth2.0/OpenID** and **SSO** for the following reasons:

1. **Broad Acceptance & Flexibility**: OAuth2.0/OpenID is widely adopted and provides flexibility in terms of user authentication. It's not only secure but also provides a familiar login experience for users, as they might already be using OAuth2.0/OpenID in other platforms.

2. **Enhanced Security with JWT**: While JWT was a consideration, using it in tandem with OAuth2.0/OpenID means we can use JWTs as our access tokens post-authentication. This provides a secure, stateless, and scalable means of maintaining user sessions.

3. **Corporate Integration with SSO**: As we expand and integrate with corporations or other large entities, providing SSO capabilities ensures employees or members of these entities can access our platform without going through repeated authentication processes. It's not just about convenience; it's about enhancing user experience and speeding up the onboarding process.

## Consequences

**Pros**:

- **Seamless User Experience**: With SSO, users experience fewer disruptions.
- **Flexible Integrations**: OAuth2.0/OpenID allows for easy integration with third-party platforms and services.
- **Enhanced Security**: Leveraging the combination ensures both secure authentication (via OAuth2.0/OpenID) and secure session management (via JWT).

**Cons**:

- **Complex Implementation**: Combining multiple strategies requires careful implementation to avoid vulnerabilities.
- **Dependency**: Relying on external identity providers (in case of some OAuth2.0/OpenID scenarios) can sometimes result in outages or issues if the external service faces downtime.
