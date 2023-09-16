## ADR-04: API Strategy Selection

### Status
Adopted

### Context
The trip management dashboard requires a consistent, reliable, and efficient method to fetch and update data between the frontend and backend. The most notable contenders are:
- **[REST](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)**: Representational State Transfer is an architectural style that relies on stateless, cacheable, client-server communication. It uses standard HTTP methods and status codes, URLs, and MIME types.
- **[GraphQL](https://graphql.org/)**: A query language for APIs, and a server-side runtime for executing those queries by using a type system. It enables declarative data fetching where a client can request exactly the data it needs.

### Decision
[REST](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) is chosen as the primary API strategy for the trip management dashboard due to:
1. Maturity and Stability: REST has been around for a long time and has proven stability and effectiveness.
2. Standardized Methods: RESTful methods are widely recognized and understood.
3. Simplicity: For many operations, REST can be more straightforward than GraphQL.
4. Cacheability: RESTful APIs are easily cacheable, which can improve performance.
5. Integration with Existing Systems: Considering that integration with legacy systems (like SABRE, APOLLO) might be easier with REST.
6. Broad Knowledge Base: Given its maturity, there's a vast pool of resources, tools, and talent familiar with RESTful API development.

### Consequences
**Pros**:
- Scalability: RESTful services are stateless; scaling is easier.
- Learning Curve: Developers are generally more familiar with the REST paradigm.
- Versatility: Multiple data formats (not just JSON) can be used.
- Performance: Efficient caching mechanisms can be leveraged to boost performance.

**Cons**:
- Over-fetching/Under-fetching: Might fetch more or less data than required.
- Multiple Endpoints: Requires a different endpoint for different data.
- Versioning: As the system evolves, changes might necessitate API versioning.
