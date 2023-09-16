# ADR-17: CI/CD Strategy

## Status

Adopted

## Context

Implementing an effective CI/CD strategy is crucial for our application's agility, quality, and delivery speed. By automating the stages of application delivery, we can consistently and quickly push features, fixes, and updates. The following CI/CD solutions were considered:

1. **[Jenkins](https://www.jenkins.io/)**:
    - An extensible, open-source automation server used to automate the non-human part of the software development process.

2. **[GitLab CI/CD](https://docs.gitlab.com/ee/ci/)**:
    - Integrated CI/CD part of GitLab that includes the modern developer's entire DevOps lifecycle in a single application.

3. **[AWS CodePipeline](https://aws.amazon.com/codepipeline/)**:
    - A fully managed continuous delivery service that automates the build, test, and deploy phases of the release process.

Given our requirements for ease of integration, scalability, feature set, and costs, our CI/CD tool needed to support our agile practices effectively.

## Decision

We have chosen **GitLab CI/CD** for the following reasons:

1. **Integrated Solution**: GitLab CI/CD is integrated into the GitLab system, which means there is no need for integration with another tool or platform. It provides a seamless experience from code commit to deployment.

2. **Customizable Pipelines**: GitLab's CI/CD pipelines are highly customizable, allowing us to define our workflows.

3. **Auto DevOps**: Provides pre-defined CI/CD configurations which can automatically detect, build, test, deploy, and monitor applications.

4. **Scalability**: With GitLab CI/CD, we can use Kubernetes to dynamically scale our runners, enabling us to handle multiple builds in parallel, reducing the build queue and wait time.

5. **Built-in Security and Compliance**: GitLab CI/CD incorporates security into the DevOps lifecycle. It provides features like Static Application Security Testing (SAST), Dynamic Application Security Testing (DAST), and Dependency Scanning.

## Consequences

**Pros**:

- **Unified Experience**: Reduced context switching as everything is within GitLab.
- **Speed**: Parallel execution of jobs, and with the power of Kubernetes, can handle a surge in build and deploy tasks.
- **Visibility**: Provides a clear view of everything that's happening with the builds, from commits, merges to deploys.

**Cons**:

- **Learning Curve**: For teams unfamiliar with GitLab, there might be an initial learning phase.
- **Overhead**: For smaller teams or projects, the full feature set of GitLab CI/CD might be more than necessary.
