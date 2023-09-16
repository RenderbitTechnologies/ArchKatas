## ADR-26: Content Management System Strategy

### Status
Adopted

### Context
A Content Management System (CMS) is integral to efficiently manage and deliver content for our travel platform. Several factors, such as ease of use, development and operational efficiency, extensibility, and compatibility with the broader technology stack, inform our choice of CMS.

With our platform being oriented towards a JavaScript-centric technology stack, our focus shifted to a CMS that is built on Node.js. This led us to consider **Ghost**, a professional publishing platform using Node.js, and compare it with other major CMS options:

1. **Ghost (Node.js)**:
    - **Pros**:
        - Built on Node.js; aligns with our tech stack.
        - Fast, modern, and uses a decoupled architecture.
        - Simplistic and clean user interface.
        - Secure by default with automatic SSL.
    - **Cons**:
        - Newer to the market; lacks the extensive plugin ecosystem of WordPress.
        - Might require custom integrations for specific functionality.

2. **WordPress (PHP)**:
    - **Pros**:
        - Established and widely used.
        - Extensive plugin ecosystem.
        - Large community and extensive documentation.
    - **Cons**:
        - Built on PHP; misalignment with our JavaScript-centric tech stack.
        - Requires frequent updates for security.

3. **Drupal (PHP)**:
    - **Pros**:
        - Highly customizable.
        - Strong security features.
    - **Cons**:
        - Steeper learning curve.
        - Also built on PHP; doesn't align with our current stack.

Considering our emphasis on a unified technology stack and the benefits of Node.js for backend operations, Ghost emerged as a promising option.

### Decision
Opt for **Ghost** because:

- **Alignment with Tech Stack**: Ghost's Node.js foundation ensures seamless integration with our other platform components.
- **Modern Architecture**: Ghost is designed for modern web architectures, offering faster performance.
- **Usability**: Its minimalist design ensures a clutter-free and efficient content creation experience.

### Consequences
**Pros**:
- **Unified Tech Stack**: Easier maintenance, fewer context switches for developers.
- **Optimized Performance**: Ghost's lightweight nature ensures faster content delivery.
- **Security**: Ghost offers built-in security features such as automatic SSL.

**Cons**:
- **Plugin Ecosystem**: While growing, Ghost's ecosystem isn't as vast as WordPress, potentially demanding custom solutions for unique needs.
- **Community Size**: Being newer, Ghost's community is smaller. While it is active, resources might not be as plentiful as WordPress.

