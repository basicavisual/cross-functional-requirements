---
title: Quality Cross-Functional Requirements
capability: >
  Quality cross-functional requirements define what a Building Block must provide so that it can be evaluated, tested and used by people who did not build it. This covers documentation, standards compliance for user-facing components, accessibility, testability and localization. A Building Block that lacks these qualities may work internally but cannot be meaningfully assessed during procurement, verified during compliance testing or operated across different countries and user populations.
requirements:
  - id: "1"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "English documentation is provided"
    api_operation_id:
    test:
    comment: "previously 5.5"
    documentation: >
      The Building Block provides written documentation in English that covers installation, configuration and operational use. Documentation is stored alongside the source code in the same repository. Where applicable, documentation is generated directly from code (for example, inline API annotations or structured comments).

      English serves as the shared working language across GovStack implementations. Without it, no reviewer, integrator or procurement authority can easily evaluate the Building Block and related materials.
  - id: "2"
    status: PUBLISHED
    level: REQUIRED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Web user interfaces comply with HTML5 and CSS3 standards"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every web-based user interface delivered by the Building Block produces valid HTML5 markup and valid CSS3 styling. The interface follows responsive design principles and accessibility best practices. Compliance can be verified through standard HTML and CSS validation tools applied against representative pages of the running application.

      This requirement applies only when the Building Block includes a web UI component.
  - id: "3"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: IMMUTABLE
    statement: "Applications meet the accessibility requirements of WCAG 2.1 at the AA level"
    api_operation_id:
    test:
    comment:
    documentation: >
      All user-facing applications conform to the Web Content Accessibility Guidelines 2.1 at AA level. This means the application is usable by people with disabilities, including those who rely on screen readers, keyboard-only navigation or alternative input devices. WCAG 2.1 AA is a legal baseline in many jurisdictions and a core condition for inclusive government services. Compliance can be verified through automated accessibility scanning tools combined with structured manual testing against the WCAG 2.1 AA success criteria.

      _More:_ [https://www.w3.org/TR/WCAG21/](https://www.w3.org/TR/WCAG21/)
  - id: "4"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "OpenAPI specification is provided"
    api_operation_id:
    test:
    comment: "previously 5.6"
    documentation: >
      The Building Block publishes a machine-readable API definition using the OpenAPI 3.x specification format for every external-facing service endpoint. The specification file validates against the official OpenAPI schema without errors. This specification is the primary contract that other Building Blocks and integrators rely on; without it, integration depends on informal knowledge and point-to-point agreements that break at scale.

      _More:_ [_OpenAPI Standard_](https://spec.openapis.org/oas/latest.html), [_Swagger OpenAPI 3.0 Specification_](https://swagger.io/specification/).
  - id: "5"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Functional scope of the system is defined and documented in clear business use cases and user stories"
    api_operation_id:
    test:
    comment:
    documentation: >
      The Building Block documents its functional scope using business use cases and user stories that describe what the system does, for whom and under what conditions. This documentation establishes the boundary of what the Building Block is responsible for, which directly determines what must be tested and what falls outside scope. A Building Block with undocumented scope cannot be reliably evaluated for compliance or compared against alternatives during procurement.
  - id: "6"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "All end-user functionality is covered by functional tests, including both UI and API interactions"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every feature accessible to end users - whether through a UI or an API - has a corresponding automated test that exercises the expected behavior and verifies the outcome. Test suites include API contract tests, integration tests and UI tests where applicable. Full coverage means that a change to any user-facing behavior triggers at least one test failure if the behavior breaks, which is essential for regression safety across Building Block versions.

      Tests can be run in continuous integration pipelines and produce a pass/fail result per test case.
  - id: "7"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: REPLACEABLE
    statement: "Compliance test mock/example implementation is provided"
    api_operation_id:
    test:
    comment: "previously 5.26"
    documentation: >
      The Building Block provides a working mock or example implementation that demonstrates API endpoints with realistic request and response payloads. This implementation runs independently and responds to API calls as defined in the OpenAPI specification. Its purpose is to enable third-party compliance testing: evaluators and integrators can verify their client code against the mock without access to a full production deployment. See [GovStack BB Template Examples](https://github.com/GovStackWorkingGroup/bb-template/tree/main/examples) for reference.
  - id: "8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Building blocks are localizable"
    api_operation_id:
    test:
    comment: "previously 5.27"
    documentation: >
      Where a Building Block has a user-facing interface, it supports presenting content in the user's local language. The Building Block is designed to support multiple locales without requiring changes to application logic when a new language is added.

      This requirement exists because GovStack operates across countries with different official languages. A Building Block that hard-codes a single language cannot serve its intended international audience (including for countries that internally support multiple languages).
---
