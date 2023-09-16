# ADR-25: Caching Mechanism Strategy

## Status

Adopted

## Context

To ensure high performance and reduced latency, it's imperative to adopt a caching mechanism. Caching strategies play a pivotal role in the user experience, especially for a travel platform where timely information retrieval can make or break user decisions. The main contenders in the discussion are:

1. **In-memory Caching (Redis)**:
    - **Pros**:
        - Extremely fast due to in-memory nature, offering sub-millisecond response times.
        - Versatile; can be used as a cache, message broker, and more.
        - Supports various data structures like strings, hashes, sets, and more.
        - Horizontal scaling with partitioning.
    - **Cons**:
        - As an in-memory database, the cost can escalate with the data size.
        - Data can be lost in case of a crash (though persistent options exist).

2. **Content-based Caching (Varnish)**:
    - **Pros**:
        - Specifically designed for HTTP caching.
        - Highly efficient for caching web pages or API responses.
        - Can be placed in front of any HTTP server.
        - Rich feature set for cache invalidation, purging, and hit/miss info.
    - **Cons**:
        - More suitable for static content or whole-page caching.
        - Complexity can increase with custom cache invalidation logic.
        - Doesn't support other caching patterns or data structures like Redis.

For our travel platform, while web page caching is important, caching dynamic data, user sessions, and other elements is equally critical. Moreover, the flexibility to use cache for multiple purposes and patterns holds value.

## Decision

Opt for **Redis** for the following reasons:

- **Flexibility**: Redis's versatile nature allows it to handle diverse caching needs, from session storage to frequently accessed data.
- **Performance**: In-memory nature ensures high speed and low latency.
- **Scalability**: Redis can be easily scaled out with partitioning.
- **Mature Ecosystem**: Availability of client libraries for various programming languages and robust community support.

## Consequences

**Pros**:

- **Improved Latency**: Faster data retrieval for a better user experience.
- **Versatility**: Ability to use Redis for multiple caching patterns and even as a message broker or session store.
- **Scalability**: Can handle large volumes of data and traffic by scaling out.

**Cons**:

- **Cost Consideration**: Being in-memory, Redis can become expensive as the dataset grows. It's essential to monitor usage and costs.
- **Persistence Management**: Depending on configuration, there's potential data loss in crashes. Regular backups and choosing appropriate persistence options become crucial.
