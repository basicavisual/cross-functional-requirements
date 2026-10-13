---
title: Architecture Cross-Functional Requirements
capability: >
  Architecture cross-functional requirements define the structural constraints that every Building Block must satisfy to participate in a GovStack ecosystem. These requirements enforce autonomy, interface discipline and operational resilience - the properties that make independent Building Blocks composable without creating hidden dependencies between teams, agencies or vendors.
requirements:
  - id: "1"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: IMMUTABLE
    statement: "Building Blocks are autonomous"
    api_operation_id:
    test:
    comment: "previously 5.20"
    documentation: >
      Each Building Block is capable of running independently, without requiring other Building Blocks or external data stores. It owns its data, manages its own lifecycle and does not depend on the availability of any peer to function. No shared databases, no shared file systems and no shared memory between Building Blocks. Autonomy enables independent deployment, independent scaling and independent team ownership.
  - id: "2"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Communicate with other Building Blocks only via API"
    api_operation_id:
    test:
    comment: "previously 5.3"
    documentation: |
      Paraphrased from the Amazon API Mandate: [https://api-university.com/blog/the-api-mandate/](https://api-university.com/blog/the-api-mandate/)

      1. All BBs expose their data and functionality through service interfaces (APIs).
      2. Building Blocks communicate with each other through these interfaces.
      3. There will be no other form of interprocess communication allowed: no direct linking, no direct reads of another team's data store, no shared-memory model, no back-doors whatsoever. The only communication allowed is via service interface calls over the network.
      4. It doesn't matter what technology is used. HTTP, Corba, Pubsub, custom protocols - doesn't matter. Technology choice (HTTP, Pub/Sub, gRPC, etc.) is flexible, but the API contract is immutable.
      5. All service interfaces, without exception, are designed from the ground up to be externalizable. That is to say, the team must plan and design the service so the interface is able to be exposed to developers in the outside world. No exceptions.

      Building blocks do not use shared databases, file systems or memory for data exchange with other building blocks.
  - id: "3"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "APIs are versioned"
    api_operation_id:
    test:
    comment: "previously 5.4"
    documentation: >
      Every API uses semantic versioning (see [https://semver.org/](https://semver.org/)) to document changes. Breaking changes are deployed on a separate versioned endpoint (e.g. `/api/v1` and `/api/v2`), so that existing consumers are not forced to change when a new version is released. The version identifier is present in the endpoint path or header contract.
  - id: "4"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "APIs are stateless"
    api_operation_id:
    test:
    comment: "previously 5.14"
    documentation: >
      Each API call contains all of the data necessary to complete itself successfully. The server does not rely on stored session state from prior requests to process a new request. Any context needed - authentication tokens, resource identifiers, filters - is passed explicitly with every call.
  - id: "5"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "HTTP methods follow idempotency"
    api_operation_id:
    test:
    comment: "previously 5.13"
    documentation: >
      Safe methods (GET, HEAD, OPTIONS, TRACE) do not change server state. Idempotent methods (GET, HEAD, PUT, DELETE, OPTIONS, TRACE) may change state on the first call but repeated identical calls leave the server in the same final state. POST and PATCH are not idempotent unless a specific operation is explicitly designed and documented as such.

      Idempotency is a property of server state, not of response content. A second DELETE returning 404 (or also 204) is still idempotent because the resource no longer exists. What implementations must guarantee is that repeated calls produce no additional side effects - no extra audit records, no further notifications, no outbound messages and no state mutations beyond those of the first call.

      Reference: RFC 9110 Section 9.2 ([https://www.rfc-editor.org/rfc/rfc9110#section-9.2](https://www.rfc-editor.org/rfc/rfc9110#section-9.2)).

      _Reference:_ [_https://restfulapi.net/idempotent-rest_-apis/](https://restfulapi.net/idempotent-rest-apis/)
  - id: "6"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Follows REST API Design Guidelines Part 1"
    api_operation_id:
    test:
    comment: "previously 5.1"
    documentation: |
      APIs follow the core principles of the TM Forum REST API Design Guidelines: no PII or session keys in URLs (use POST or request bodies for sensitive data), support for caching and retries, resource identification via URIs, separation between server-internal representation and client-facing representation, self-descriptive messages that include enough information for the receiver to know how to process them. See: TM Forum REST API Design Guidelines.

      _See:_ [_TM Forum REST API Design Guidelines_](https://www.tmforum.org/resources/specification/tmf630-rest-api-design-guidelines-4-2-0/)

      _Some key principles from these design guidelines are as follows:_

      * _APIs do not include Personally Identifiable Information (PII) or session keys in URLs - use POST or other methods for this_
      * _Support caching/retries_
      * _Resource identification in requests Individual resources are identified in requests, for example using_ [_URIs_ ](https://en.wikipedia.org/wiki/Uniform_resource_identifier)_in RESTful Web services. The resources themselves are conceptually separate from the representations that are returned to the client. For example, the server could send data from its database as_ [_HTML_](https://en.wikipedia.org/wiki/HTML)_,_ [_XML_ ](https://en.wikipedia.org/wiki/XML)_or as_ [_JSON_](https://en.wikipedia.org/wiki/JSON)_—none of which are the server's internal representation._
      * _Resource manipulation through representations. When a client holds a representation of a resource, including any_ [_metadata_ ](https://en.wikipedia.org/wiki/Metadata)_attached, it has enough information to modify or delete the resource's state._
      * _Self-descriptive messages Each message includes enough information to describe how to process the message. For example, which parser to invoke can be specified by a_ [_media type_](https://en.wikipedia.org/wiki/Media_type)_._
  - id: "7"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Follows REST API Design Guidelines Parts 2-7"
    api_operation_id:
    test:
    comment: "previously 5.2"
    documentation: >
      APIs follow the extended TM Forum REST API Design Guidelines (parts 2 through 7) covering resource manipulation through representations, self-descriptive messages, error handling conventions and additional design rules. Deviations from these guidelines is documented and the replacement still provides a consistent API contract. See: TM Forum REST API Design Guidelines.

      _See:_ [_TM Forum REST API Design Guidelines_](https://www.tmforum.org/resources/specification/tmf630-rest-api-design-guidelines-4-2-0/)
  - id: "8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "User interface and service logic is logically separated"
    api_operation_id:
    test:
    comment:
    documentation: >
      UI components and backend services interact strictly via APIs. The presentation layer does not contain business rules or direct data store access. The backend does not generate UI markup. This separation allows frontend and backend to evolve on independent release cycles and supports multiple client types against the same service layer.
  - id: "9"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Databases do not include business logic"
    api_operation_id:
    test:
    comment: "previously 5.17"
    documentation: >
      Triggers, stored procedures and embedded business logic in databases are avoided. All business logic resides in application code or orchestration components where it can be version-controlled, tested and deployed through standard pipelines. Keeping logic out of the database prevents hidden coupling between the data layer and business rules.
  - id: "10"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Domain Driven Design (DDD) and microservices architectural principles guide the design of components"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks follow Domain Driven Design concepts. Each microservice encapsulates a bounded domain of functionality, owns its data and is independently deployable. Service boundaries align with business capabilities, not technical layers. A change to one domain does not require coordinated deployment of another domain.
  - id: "11"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Designed for asynchronous first"
    api_operation_id:
    test:
    comment: "previously 5.22"
    documentation: >
      Designs support occasional connectivity and low bandwidth by defaulting to asynchronous communication patterns. A Publish/Subscribe pattern can be used to propagate changes, allowing loosely-coupled solutions to be assembled without modifying existing APIs. Synchronous request/response is acceptable where latency requirements demand it, but the architecture does not assume that every downstream service is available at the moment a request is made.
  - id: "12"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Application is resilient to external system failures"
    api_operation_id:
    test:
    comment:
    documentation: >
      Failures in one dependency only impact directly related use cases - they do not cascade to the entire application or to unrelated services. Building Blocks implement retry logic, circuit breaker patterns and fallback mechanisms so that a slow or unavailable external system does not bring down the whole Building Block architecture.
  - id: "13"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Include Transaction/Trace/Correlation IDs"
    api_operation_id:
    test:
    comment: "previously 5.15"
    documentation: >
      Every transaction that crosses multiple services carries a correlation ID that is passed with every request and response in the chain. The correlation ID is generated at the entry point and propagated without modification through all downstream calls. This enables end-to-end tracing of a single operation across Building Block boundaries for debugging, performance analysis and audit purposes.
  - id: "14"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: REPLACEABLE
    statement: "Use Web Hooks for callbacks"
    api_operation_id:
    test:
    comment: "previously 5.11"
    documentation: >
      When a Building Block needs to notify another system about an event or completion of an asynchronous operation, it uses webhooks - HTTP callbacks to a URL registered by the subscriber. Direct function calls or internal method invocations across Building Block boundaries are not permitted for callback functionality.
  - id: "15"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Observability and monitoring functionality is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks expose health check endpoints, metrics and logging interfaces that can be consumed by standard monitoring platforms (e.g. Prometheus, Grafana, ELK, OpenTelemetry). Health checks report the operational status of the Building Block and its critical dependencies. Without observability, operators cannot detect degradation, diagnose failures or plan capacity.
  - id: "16"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Use NTP synchronization"
    api_operation_id:
    test:
    comment: "previously 5.28"
    documentation: >
      Where precise timestamps are required, Building Blocks leverage Network Time Protocol (NTP) or an equivalent time synchronization mechanism to align clocks across servers. Accurate time synchronization is necessary for correct ordering of events, reliable log correlation, valid security token expiration and consistent audit trails across distributed services.
  - id: "17"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "APIs follow a published deprecation lifecycle"
    api_operation_id:
    test:
    comment:
    documentation: >
      When an API version or endpoint is scheduled for removal, the Building Block announces a deprecation timeline and communicates it to consumers through machine-readable signals (e.g. IETF RFC 8594 Sunset header or equivalent).

      Deprecated endpoints continue to function for a defined transition period before removal. The deprecation policy and timeline is documented per API version.

      _Reference: IETF RFC 8594 (https://datatracker.ietf.org/doc/html/rfc8594)._
  - id: "18"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Consumers apply the tolerant reader pattern to received payloads"
    api_operation_id:
    test:
    comment:
    documentation: >
      When a Building Block receives a payload (API response, event or message), it ignores fields it does not recognize rather than rejecting the entire payload. This allows producers to add new fields without breaking existing consumers and is a precondition for independent evolution of Building Blocks.

      Implementations do not fail on unknown properties in JSON or XML payloads unless a strict validation mode is explicitly required by a functional requirement.

      _Reference: Postel's Law (RFC 761), Google AIP-203._
  - id: "19"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Asynchronous messages and events follow a published schema"
    api_operation_id:
    test:
    comment:
    documentation: >
      Every event or message exchanged asynchronously between Building Blocks has a defined and versioned schema that describes its structure, required fields and semantics. Schemas are published and accessible to all consumers before integration.

      Changes to event schemas follow the same versioning discipline as synchronous APIs (see architecture requirement #3). Without published schemas, asynchronous channels become undocumented coupling between services.

      _Reference: CNCF CloudEvents (https://cloudevents.io/), AsyncAPI specification (https://www.asyncapi.com/)._
---








