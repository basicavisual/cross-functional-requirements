---
title: Scope
---

## What this specification covers

`govstack-cfr` covers the cross-functional qualities of **software components** that take part in a GovStack ecosystem. Its conformance subject is software: a solution is assessed against it, not a document, an organization or a service.

It applies to:

- **Building Block software**: any implementation of a GovStack Building Block specification, which inherits this baseline through `extends`;
- **adaptors**: components that map an existing product's API onto a GovStack specification. The adaptor must meet this baseline in its own right;
- **software built against `govstack-cfr` alone**: components for which no Building Block specification exists yet, but which are meant to work within a GovStack ecosystem.

Non-Building Block software, such as legacy systems that expose APIs, may also be assessed against this baseline. Doing so does not make it a Building Block.

Within those components, the specification covers six domains:

| Domain | Covers |
|---|---|
| **Development** | Version control, source code and documentation language, licensing, schema migrations, test coverage, code audits, component lifecycle and language choice, public code practices. |
| **Deployment** | Container packaging, backup and restore, deployment documentation and scripts, image integrity, versioning and rollback, multiple environments, CI/CD compatibility, availability and scaling, startup and shutdown behaviour, resource limits, base images. |
| **Architecture** | Autonomy of Building Blocks, API-only communication, API versioning, statelessness, idempotency, REST design guidelines, separation of UI, logic and data, asynchronous design, resilience, correlation IDs, callbacks, observability, time synchronization, API deprecation, tolerant readers, event schemas. |
| **Quality** | Documentation, web standards, accessibility, OpenAPI descriptions, use cases, functional tests, compliance test mocks, localization. |
| **Security** | Transport security, cryptography, access control and authentication, secure configuration, secrets handling, input and output sanitization, security logging, isolation, API gateways, key rotation, vulnerability management, incident response, audit readiness, encryption at rest, software bill of materials, error and log exposure. |
| **Data** | Unicode text, ISO 8601/UTC timestamps, standard data formats, data protection principles, validation, domain data standards, logical deletion, export, lineage, retention, data localization, published data models, sensitivity classification, anonymization. |

The specification also covers how to refer to itself: the `govstack-cfr` identifier, its versioned form and the identifiers of individual requirements.

The architecture requirements apply at two of the three architecture scopes GovStack distinguishes: **system architecture**, meaning the interaction between Building Blocks, service applications and other components, and **component architecture**, meaning the inside of a single component. The scopes are described in [GovStack Architecture](https://specs.govstack.global/architecture/) (`govstack:ra:architecture`).

## What this specification does not cover

The following are outside the scope of `govstack-cfr`. Where another GovStack publication covers the topic, it is named.

- **Functional behaviour of any Building Block.** Service API contracts, endpoints, data structures, key functionalities and functional requirements belong to the Building Block specifications (`govstack-bb-*`). This document never defines what a component does, only the qualities it must have while doing it.
- **Replaceability between implementations.** Swapping one implementation for another without changing consumers requires a shared service API contract, so it is a property of Building Block specifications, not of this baseline.
- **Government services.** Eligibility rules, obligations, service levels, end-to-end service processes and non-digital channels are out of scope. A specification covers the software that automates parts of a service, never the service itself.
- **Government architecture.** Whole-of-government structure, organizational coordination, legal frameworks and semantic alignment across institutions are covered by PAERA and by domain Reference Architectures.
- **Legal and regulatory compliance.** The requirements are written so as not to block compliance with regulations such as GDPR or eIDAS, but they do not establish it. Legal guidance belongs in optional Guides, not in specifications.
- **Semantic interoperability.** Common data models, shared code lists and data-sharing agreements between institutions are outside scope. The data domain requires the use of existing standards, but does not choose which ones a domain adopts.
- **Choice of implementation.** Programming languages, frameworks, products, vendors and hosting providers are not mandated. A preference that has no effect on business function is never a requirement here. Open source is recommended, not required.
- **Sovereignty beyond architecture.** The specification requires components to be configurable for data residency, but the choice of hosting location, legal jurisdiction over infrastructure and operational continuity arrangements are not covered.
- **Operation of a deployment.** The requirements describe what a component must be capable of (backup, rollback, monitoring, incident response plans). How a particular government staffs, runs and governs its deployment is out of scope.
- **Architecture principles and rationale.** The principles the requirements implement, the interoperability maturity model and the architecture patterns GovStack advocates are described in [GovStack Architecture](https://specs.govstack.global/architecture/) (`govstack:ra:architecture`), not here.
- **How specifications are written.** Rules governing the authoring of Building Block specifications, including the rule that they must not copy the baseline into their own text, belong to the GovStack specification framework. Their conformance subject is documents, not software.
- **Compliance procedure.** This document defines what is assessed. How assessments are run, evidenced and recorded, and how GovMarket lists solutions, are defined elsewhere.
