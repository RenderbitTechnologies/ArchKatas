## ADR-03: Backend Development Framework Selection

### Status
Adopted

### Context
Our application requires a robust backend framework that can handle international traffic, provide quick response times, and facilitate rapid development and deployment. We considered three popular frameworks across different programming languages: Node.js (Express), Java (Spring Boot), and Python (Django/Flask).

**Node.js (Express)**:
- **Pros**:
    - **Performance**: Event-driven, non-blocking I/O makes it suitable for I/O bound tasks and can handle a large number of simultaneous connections with low overhead.
    - **Unified Stack**: Uses JavaScript, allowing for a consistent language between the frontend and backend.
    - **Ecosystem**: Extensive package library (npm) and a vibrant community that contributes to a rich set of middleware and tools.
    - **Development Speed**: Facilitates rapid development due to its minimalist and flexible structure.
- **Cons**:
    - **CPU-Intensive Tasks**: Not ideal for heavy computation tasks, though this isn’t our primary use-case.

**Java (Spring Boot)**:
- **Pros**:
    - **Maturity**: Battle-tested in numerous production environments; trusted for enterprise-level applications.
    - **Performance**: Robust performance, especially for compute-intensive tasks.
    - **Ecosystem**: Mature ecosystem with a wide array of libraries and tools.
- **Cons**:
    - **Development Speed**: Typically requires more boilerplate and configuration than some newer frameworks.
    - **Resource Overhead**: Can be more resource-intensive compared to lightweight frameworks.

**Python (Django/Flask)**:
- **Pros**:
    - **Rapid Development**: Especially with Django, which follows the "batteries-included" philosophy, offering a comprehensive set of features out of the box.
    - **Versatility**: Suitable for both small applications (using Flask) and large applications (using Django).
    - **Readability**: Python’s syntax is clear and concise, leading to easily maintainable code.
- **Cons**:
    - **Performance**: Generally slower than Node.js and Java, especially for I/O bound tasks.
    - **Concurrency**: Python's Global Interpreter Lock (GIL) can be a limitation for CPU-bound tasks, although there are workarounds.

### Decision
Given our priority to maintain a streamlined tech stack and to achieve synergy between the backend and frontend, we have chosen **Node.js with Express**. This decision promotes the use of a single language (JavaScript) across our stack. Node.js with Express offers both performance suitable for our needs and rapid development capabilities.

### Consequences
**Pros**:
- **Unified Development**: Allows developers to leverage their JavaScript expertise across the entire application.
- **Fast Iteration**: Rapid development and deployment cycles can be expected.
- **Scalability**: Built to handle concurrent requests efficiently, making it suitable for our anticipated user growth.

**Cons**:
- **Complex Computation**: For future needs, if heavy computation becomes a requirement, we might need to offload such tasks to dedicated services or consider integrating other languages/frameworks.
