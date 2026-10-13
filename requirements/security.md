---
title: Security Cross-Functional Requirements
capability: >
  Security requirements protect the confidentiality, integrity and availability of Building Block services and the data they process. Government systems handle citizen data and deliver essential services, so a security failure has consequences beyond the technical - it undermines institutional trust and can interrupt service delivery. The requirements below cover transport encryption, cryptographic standards, access control, secrets management, input validation, security logging, testing, isolation and operational preparedness. They are ordered from most fundamental to most operational. Every requirement applies to all Building Blocks unless explicitly stated otherwise.
requirements:
  - id:" 1"
    status: PUBLISHED
    level: REQUIRED
    observability: OBSERVABLE
    mutability: IMMUTABLE
    statement: "Transport security is enforced"
    api_operation_id:
    test:
    comment: "previously 5.12"
    documentation: >
      All communication between Building Blocks and between a Building Block and any external client uses HTTPS with TLS 1.3 or higher. Insecure cipher suites are disabled. Plaintext HTTP endpoints are not exposed in any environment other than isolated local development. Without transport encryption, all other security controls can be bypassed through interception.
  - id:" 2"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: IMMUTABLE
    statement: "Only up-to-date and industry-accepted cryptographic algorithms are used for data protection"
    api_operation_id:
    test:
    comment:
    documentation: >
      All cryptographic operations - encryption, hashing, signing, key exchange - use algorithms currently recommended by recognized standards bodies (e.g. NIST, ENISA). Deprecated or broken algorithms such as MD5, SHA-1 for signing or DES must not be used. The implementation allows algorithm configuration to be updated without code changes so that rotation to stronger algorithms is operationally feasible.
  - id:" 3"
    status: PUBLISHED
    level: REQUIRED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Access control and authentication is enforced"
    api_operation_id:
    test:
    comment:
    documentation: >
      Each Building Block enforces a least-privilege access control model so that users and services only access the resources they need. Authentication and authorization is handled through an Identity and Access Management service using open standards. For user-facing flows the Building Block authenticates users and obtain their roles and permissions via OpenID Connect. For machine-to-machine API interactions the Building Block authorizes calls using OAuth 2.0 or JWT-based access tokens. Tokens are short-lived and stored securely with regular rotation. Access decisions are logged to support auditing.
  - id:" 4"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: IMMUTABLE
    statement: "Secure configuration is used"
    api_operation_id:
    test:
    comment: "previously 5.21"
    documentation: >
      All runtime configuration that contains sensitive values - database credentials, API keys, signing secrets, service account tokens - is injected through environment variables or a dedicated secret management system (e.g. HashiCorp Vault, Kubernetes Secrets). Sensitive values are never hard-coded in source files or included in application images. Configuration is separated from code so that secrets can be rotated without redeploying the application.
  - id:" 5"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: IMMUTABLE
    statement: "No sensitive data such as keys, certificates or passwords is stored in code repositories or documentation"
    api_operation_id:
    test:
    comment:
    documentation: >
      Source code repositories, documentation files, CI/CD pipeline definitions and published artifacts do not contain any plaintext secrets, private keys, certificates or passwords. This includes commented-out credentials and example configuration that uses real values.
  - id:" 6"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Input and output sanitization is used"
    api_operation_id:
    test:
    comment: "previously 5.25"
    documentation: >
      All incoming data is validated against the expected format and type before processing. APIs reject or sanitize input that contains unsafe characters or tokens to prevent injection attacks (SQL injection, cross-site scripting, command injection and similar). The same applies to output data - output interfaces encode or escape appropriately for the target context so they do not break or become attack vectors.
  - id:" 7"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Logging and monitoring of security events is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every Building Block has a mechanism for generating logging information that can be captured by the hosting environment. This may be as straightforward as writing to STDOUT (captured via container log drivers such as docker logs) or may use other log sinking technologies. The implementation does not require changes to the hosting platform to capture logs - the Building Block is responsible for producing them in a consumable format.

      Security-relevant events (e.g. failed logins, permission violations) are logged separately from functional logs or clearly tagged so they can be filtered. Security logs include timestamps, trace IDs and user or service context. These logs integrate with centralized observability systems as defined in CFR Observability. Separation of security logs from functional logs allows security teams to review and respond to threats independently from operational log volume.
  - id:" 8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Isolation and containment is ensured"
    api_operation_id:
    test:
    comment:
    documentation: >
      A compromise in one Building Block must not enable escalation or lateral movement to other Building Blocks or shared infrastructure. Containers and services are run with minimal privileges following the principle of least privilege. Network segmentation and namespace isolation is implemented so that each Building Block can only reach the network endpoints it requires.
  - id:" 9"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Secure API gateways are implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Where external APIs are exposed, a gateway layer handles rate limiting, authentication and authorization enforcement, request and response validation and encryption enforcement. The gateway rejects requests that fail authentication or exceed rate limits before they reach the Building Block.
  - id: "10"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Clearly-defined key rotation policies are included"
    api_operation_id:
    test:
    comment: "previously 5.16"
    documentation: >
      Building Blocks that use cryptographic keys, signing certificates or encryption secrets define and document a key rotation policy. The policy specifies rotation frequency, the process for introducing new keys, the grace period during which old keys remain valid for decryption or verification and the procedure for emergency rotation in case of suspected compromise.
  - id: "11"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Continuous vulnerability scanning and patching is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Security testing is integrated into CI/CD pipelines. This includes Static Application Security Testing (SAST) to analyze source code, Dynamic Application Security Testing (DAST) to probe running services and Dependency Vulnerability Scanning (e.g. OWASP Dependency-Check, Trivy) to detect known vulnerabilities in third-party libraries and base images. Critical vulnerabilities are addressed before release.
  - id: "12"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Disaster recovery and incident response plans are implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Each Building Block defines incident response and disaster recovery procedures. Incident response covers alerting and triage steps, root-cause analysis and post-incident review processes and secure rollback or hot-patch mechanisms. These plans are tested periodically - an untested recovery plan does not count as a plan.
  - id: "13"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: IMMUTABLE
    statement: "Compliance and audit readiness is documented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks maintain documentation that demonstrates alignment with recognized security standards including OWASP ASVS ([https://owasp.org/www-project-application-security-verification-standard/](https://owasp.org/www-project-application-security-verification-standard/)), ISO/IEC 27001 ([https://www.iso.org/standard/27001](https://www.iso.org/standard/27001)) and GovStack Security Guide. Periodic third-party security audits are recommended for production-grade deployments.
  - id: "14"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data at rest is encrypted"
    api_operation_id:
    test:
    comment:
    documentation: >
      All persistent data stores - databases, file systems, message queues and backups - encrypt data at rest using industry-accepted algorithms. Encryption keys are managed separately from the data they protect. Where the hosting environment provides storage-level encryption, the Building Block verifies that it is enabled. Where it does not, the Building Block implements application-level encryption for sensitive data.
  - id: "15"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "A Software Bill of Materials is maintained and published"
    api_operation_id:
    test:
    comment:
    documentation: >
      Each Building Block produces and maintains a machine-readable Software Bill of Materials (SBOM) that lists all direct and transitive dependencies, their versions and their licenses. The SBOM follows a recognized format such as CycloneDX or SPDX. The SBOM is updated with each release and made available to deploying organizations so they can assess exposure when new vulnerabilities are disclosed.
  - id: "16"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Sensitive data is not exposed in error responses or log output"
    api_operation_id:
    test:
    comment:
    documentation: >
      Error responses returned to clients do not contain stack traces, internal file paths, database query details or other implementation internals. Log output does not contain passwords, tokens, private keys or personally identifiable information in plaintext. Where such data must be referenced in logs for debugging, it is masked or replaced with identifiers that can only be resolved through a separate secure lookup.
---