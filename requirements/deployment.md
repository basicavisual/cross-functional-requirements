---
title: Deployment Cross-Functional Requirements
capability: >
  Deployment requirements define how building blocks are packaged, delivered and operated in production environments. A building block that works in a developer's local setup but cannot be reliably deployed, secured, restored or scaled in a government data center fails the people it is meant to serve. These requirements establish the minimum operational contract between building block providers and the teams responsible for running public infrastructure - covering containerization, security posture, data protection, documentation, environment management and automation.
requirements:
  - id: "1"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Building blocks are deployable as a container"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every building block is packaged and deliverable as an independent container image. The image is self-contained: all runtime dependencies are included and no host-level libraries are assumed beyond the container runtime.

      Build instructions (Dockerfile or equivalent) are included in the repository so that any party can reproduce the image. Deployment may use Docker Compose, Kubernetes or compatible orchestration tools. Each image is versioned and tagged according to semantic versioning. A container image that cannot be built reproducibly from the repository is non-compliant.
  - id: "2"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Backup and restore-capable"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every building block provides a documented procedure for backing up and restoring all persistent data it manages - databases, file stores, configuration state and encryption keys. Backups are testable: a restore from backup to a clean environment must produce a working instance with data intact. The procedure specifies backup frequency guidance, storage location expectations and estimated recovery time. A building block that cannot be restored from its own backup is non-compliant.
  - id: "3"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Include deployment documentation"
    api_operation_id:
    test:
    comment:
    documentation: >
      Deliver written deployment instructions in the building block repository. Documentation covers: prerequisites (OS, runtime, network), all environment variables and their purpose, configuration file locations and formats, expected outputs on successful startup and a verification checklist. Include rollback instructions.

      If any step requires manual action, state it explicitly - do not assume operator knowledge of the building block internals. Documentation that is missing or out of date with the current release is not acceptable.
  - id: "4"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Verify container image integrity before deployment"
    api_operation_id:
    test:
    comment:
    documentation: >
      Container images are signed and their integrity verified before deployment to any environment. Only images from trusted registries with verified signatures are permitted in staging and production. The signing and verification method is documented in the deployment instructions.
  - id: "5"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Versioning and rollback-capable"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every deployed release is versioned and stored so that operators can identify exactly which version is running and revert to a previous version when a deployment fails. The repository retains at least the two most recent release artifacts (images, manifests, migration scripts).

      Include a documented rollback procedure that covers both the application layer and any database or schema changes introduced by the release. Maintain backward compatibility in APIs and data formats wherever possible.
  - id: "6"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Multi-environment support"
    api_operation_id:
    test:
    comment:
    documentation: >
      Deployment artifacts support at least three environments: development, test and production. Staging is recommended as a fourth. All environment-specific values (endpoints, credentials, feature flags, resource limits) are externalized into configuration - not baked into the image or code. Switching between environments must require only a configuration change, not a rebuild. Feature toggling per environment is supported so that incomplete or experimental capabilities can be disabled in production without a separate code branch.
  - id: "7"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Include all deployment scripts"
    api_operation_id:
    test:
    comment:
    documentation: >
      When a building block requires orchestration tools such as Kubernetes or Ansible, all configuration and deployment scripts are included in the building block repository - not maintained separately. Provide automation scripts for each supported environment (dev, test, production at minimum).

      Scripts are idempotent: running them twice against the same environment produces the same result without errors. Prefer declarative deployment definitions (Kubernetes manifests, Helm charts, Terraform modules) over imperative scripts. Scaling and rollback commands are part of the same deployment scripts.
  - id: "8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Continuous integration and continuous deployment compatibility"
    api_operation_id:
    test:
    comment:
    documentation: >
      Deployment artifacts and scripts work within standard CI/CD pipelines without manual intervention. The repository includes or references pipeline definitions that cover automated build, automated test execution, build verification and promotion between environments. Support rollback triggers so that a failed deployment can be reverted automatically or with a single operator action. Where risk allows, support canary or blue-green deployments for safer rollouts.
  - id: "9"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "High availability and scalability"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks are scriptable to deploy and recover, consist of independent instances and support automated scaling and high availability. Deployment is driven by configuration and automation, each instance is disposable and replaceable and recovery from failure is automated. Make sure that no specific cloud provider is required - the architecture must simply not prevent automated, repeatable and scalable operations.

      Building blocks are designed so that horizontal scaling (running multiple replicas behind a load balancer) is possible where the workload justifies it. The building block tolerates the loss of a single replica without service interruption.

      Document any components that cannot be scaled horizontally (for example a single-writer database) and specify the recommended approach for making them resilient to failure.
  - id: "10"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Containers support graceful shutdown and fast startup"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every container handles SIGTERM by completing in-flight requests, releasing held resources (database connections, file locks, message consumers) and exiting within a configurable timeout - (30 seconds recommended by default).

      No request accepted before the shutdown signal may be silently dropped. On startup, the container reaches a ready state fast enough for the orchestrator's readiness probe to pass without extending deployment windows beyond operational tolerance.

      _This is a prerequisite for zero-downtime deployments, rolling updates and horizontal scaling. Reference: 12-Factor App (Factor IX - Disposability), CNCF container best practices._
  - id: "11"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Resource limits are declared in deployment artifacts"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every container deployment manifest declares CPU and memory requests and limits. If a building block does not declare its resource limits, it can use up all available capacity on a shared server and cause other services running alongside it to fail.

      Declared limits reflect tested behavior under expected load - not arbitrary defaults. If a building block requires GPU or other specialized resources, those are declared as well.

      _Reference: NIST SP 800-190 (Application Container Security Guide), CIS Kubernetes Benchmark._
  - id: "12"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Container images use minimal base images"
    api_operation_id:
    test:
    comment:
    documentation: >
      Container images are built from minimal base images that contain only the runtime dependencies needed to operate. Images do not include package managers, shells, compilers or development tools unless the building block requires them at runtime - and if so, the justification is documented. Smaller images reduce the number of components that can be exploited and speed up image pull times across environments.

      _Reference: NIST SP 800-190, CIS Docker Benchmark._
---