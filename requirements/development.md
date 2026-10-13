---
title: Development Cross-Functional Requirements
capability: >
  Development practices prioritize long-term sustainability, collaborative contribution and operational transparency - because building blocks are expected to be maintained across teams, organizations and sometimes national boundaries over extended periods. The requirements below establish the baseline for how software and its source code is written, managed, tested and kept healthy over time.
requirements:
  - id: "1"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "All application source code uses version control"
    api_operation_id:
    test:
    comment:
    documentation: >
      All source code, configuration and infrastructure definitions are managed in Git or an equivalent distributed version control system. Every change is traceable to a commit with a meaningful message, an author and a timestamp. Repositories retain full history - no force-pushes or history rewrites on shared branches. Branching and merging strategy should be documented in the repository.
  - id: "2"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "All application source code and comments are clear, maintainable and written in English"
    api_operation_id:
    test:
    comment:
    documentation: >
      All source code, inline comments, commit messages and configuration files are written in English. Code follows a consistent and documented style guide covering naming conventions, folder structure and formatting. Names should be descriptive enough to convey purpose without extra comments. Where comments exist, they explain reasoning - not what the code already says.
  - id: "3"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "All software is published with a clear open-source license"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every repository includes a recognized open-source license file (OSI-approved) at the root. Third-party dependency licenses must be compatible with the project license - verified manually or through automated tooling. Governments need legal certainty before deploying software as unclear licensing blocks adoption.

      Apache 2.0 License can be used for this purpose, it is used by default in GovStack. More: [https://www.apache.org/licenses/LICENSE-2.0](https://www.apache.org/licenses/LICENSE-2.0)
  - id: "4"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Database schema changes are managed with migration scripts"
    api_operation_id:
    test:
    comment:
    documentation: >
      All schema changes - table creation, column modifications, index changes, data transformations - are expressed as versioned migration scripts committed alongside application code. Migrations run sequentially from empty to current state. Each script should be idempotent or guarded against re-execution. Rollback scripts are recommended for production deployments.
  - id: "5"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Include unit and integration test coverage"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building blocks include automated unit tests (fast, isolated, deterministic) and integration tests (validating interactions with databases, APIs and external dependencies). Tests run without manual intervention and produce clear pass/fail results. Coverage should prioritize critical business logic and public API surfaces. A minimum coverage threshold should be defined and enforced through CI tooling.
  - id: "6"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Regular security and code quality audits"
    api_operation_id:
    test:
    comment:
    documentation: >
      Automated security and quality analysis runs across source code and third-party dependencies using tools such as SonarQube, Snyk or OWASP Dependency-Check. This applies to source code, SaaS building blocks and independently deployable software. Scans cover static analysis, dependency CVEs and code quality metrics. Findings above a defined severity threshold block merges or releases. Audit results and remediation history are retained for compliance review.

      All source code undergoes peer code review with explicit attention to security implications before merging. Sensitive code segments (e.g. cryptographic operations, identity management) are reviewed by team members with demonstrated security expertise.
  - id: "7"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Used components End-of-Life is at least 5 years"
    api_operation_id:
    test:
    comment:
    documentation: >
      No language runtime, framework, library or infrastructure dependency should be adopted where that component has a known or projected EOL of less than 5 years. Teams verify EOL timelines against official support policies and document them. Where no formal EOL is published, assess community activity, release cadence and commercial backing as proxy indicators.
  - id: "8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Preference for the top 25 languages listed in either the TIOBE Index or any of the three IEEE Spectrum rankings"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building blocks should use languages ranking in the top 25 of the TIOBE Index ([https://www.tiobe.com/tiobe-index/](https://www.tiobe.com/tiobe-index/)) or IEEE Spectrum rankings ([https://spectrum.ieee.org/top-programming-languages](https://spectrum.ieee.org/top-programming-languages)). This maximizes the available developer pool for maintenance, extension and audit - especially in low-resource settings. Less common languages may be used for specific purposes (shell scripting, configuration DSLs) provided core application logic uses a widely supported language.
  - id: "9"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Best practices for Public Code are followed"
    api_operation_id:
    test:
    comment:
    documentation: >
      Development follows the Standard for Public Code ([https://standard.publiccode.net/](https://standard.publiccode.net/)): code in the open, bundle policy with source, create reusable and portable code, welcome contributions, require peer review, document objectives and code, use plain English, adopt open standards, use continuous integration, publish under an open license, follow a coherent style and track codebase maturity. Teams should periodically self-assess against the checklist and address gaps.
---
