---
title: Data Cross-Functional Requirements
capability: >
  Data requirements define how Building Blocks encode, format, validate, protect and manage data. Government systems exchange data across agencies, jurisdictions and time - often decades. Strict encoding and format rules prevent data from becoming unreadable. Protection and lifecycle rules ensure governments meet legal obligations and maintain citizen trust. Requirements are ordered from foundational encoding rules to deployment-specific concerns.
requirements:
  - id: "1"
    status: PUBLISHED
    level: REQUIRED
    observability: OBSERVABLE
    mutability: IMMUTABLE
    statement: "Use only Unicode for text"
    api_operation_id:
    test:
    comment: "previously 5.18"
    documentation: >
      All text stored, processed or transmitted by a Building Block uses UTF-8 encoding. This applies to API payloads, database text columns, log entries, configuration files and file-based data exchange. No other character encoding is permitted. Implementations reject or convert non-UTF-8 text at the point of entry rather than storing it silently. UTF-8 is the only encoding that supports all languages and scripts without conversion.
  - id: "2"
    status: PUBLISHED
    level: REQUIRED
    observability: OBSERVABLE
    mutability: IMMUTABLE
    statement: "Use ISO 8601/UTC for timestamps"
    api_operation_id:
    test:
    comment: "previously 5.19"
    documentation: >
      All timestamps follow ISO 8601 in UTC (e.g., `2025-11-12T13:30:00Z`). When a local time zone is relevant - for example, displaying a deadline to a citizen - the offset is stated explicitly alongside the UTC value. Internal storage and all API payloads use UTC. This prevents ambiguity in cross-border exchange and errors from daylight saving transitions or missing offsets.
  - id: "3"
    status: PUBLISHED
    level: REQUIRED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Use standardized data formats for inputs and outputs"
    api_operation_id:
    test:
    comment: "previously 5.23"
    documentation: >
      JSON is the default data format for API payloads and service-to-service communication. Where JSON is not possible - for example, legacy systems that require XML - the Building Block uses another recognized standard format. Proprietary or ad-hoc serialization is not permitted. The chosen format must be supported by standard tooling so that producers and consumers can parse and validate payloads without custom parsers.
  - id: "4"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Comply with high quality data protection principles"
    api_operation_id:
    test:
    comment: "previously 5.9"
    documentation: >
      Building Blocks conform to GDPR or GDPR-compatible principles: consent-based collection where no other legal basis applies, right to access and delete personal data, purpose limitation, data minimization and privacy-by-design/default. These principles must be adaptable to national frameworks. Each deployment documents which legal framework applies and how the Building Block satisfies it.
  - id: "5"
    status: PUBLISHED
    level: RECOMMENDED
    observability: OBSERVABLE
    mutability: EXTENSIBLE
    statement: "Data quality and validation is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks validatea data when it is received and when it is updated. Constraints - required fields, value ranges, formats, enumerations - are declared in machine-readable schemas (e.g., JSON Schema, XML Schema) and enforced programmatically. Rejected input returns an error identifying which field failed and why. Data quality metrics such as completeness and format conformance should be monitored through observability mechanisms.
  - id: "6"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Use existing standards for domain data"
    api_operation_id:
    test:
    comment: "previously 5.24"
    documentation: >
      When a recognized domain-specific data standard exists, the Building Block should adopt it. Examples: DICOM, HL7 and FHIR for healthcare, TMForum Open APIs for telecommunications, CRVS standards for civil registration. The specification documents which standards it uses and where it deviates. If no standard exists for the domain, the Building Block still publishes its data model in a machine-readable format.
  - id: "7"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "Deleting records preserves logical records unless hard deletion is mandated by law"
    api_operation_id:
    test:
    comment:
    documentation: >
      Soft delete is the default: records are marked as deleted and excluded from standard queries but retained for audit and recovery. All deletions are timestamped in UTC and record the actor or system that initiated them. Hard deletion is permitted only when required by regulation or a verified data subject request. The deletion method is logged regardless of type.
  - id: "8"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: REPLACEABLE
    statement: "All data is exportable in machine-readable and human-readable formats"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks can export stored data in at least one machine-readable format (JSON, XML or CSV) and at least one human-readable format (PDF, TXT or HTML). APIs expose endpoints for individual and bulk export. Exported files include the export timestamp and source system identifier. This enables data portability and prevents lock-in to a single implementation.
  - id: "9"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data lineage and provenance tracking is supported"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks should track the origin, transformations and usage of each data element. For every record, metadata captures: source system identifier, timestamp of each modification and the service or agent responsible. This metadata must be queryable by authorized audit processes. The purpose is to allow reconstruction of the full chain of custody when a data error or dispute occurs. Implementation mechanism is not prescribed.
  - id: "10"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data retention and archival policy is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks define retention periods per data type. When a period expires, data is archived or destroyed per stated policy. Archived data remains subject to the same protection rules as active data. All retention and destruction events are logged with timestamps and the triggering process. Retention policies are configurable per deployment because legal obligations differ across jurisdictions.
  - id: "11"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data sovereignty and localization is implemented"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks support data residency requirements defined by national regulation. Sensitive data is storable within the deploying country's jurisdiction unless a legal agreement permits cross-border transfer. The Building Block provides configuration that controls where data is physically stored and processed. Compliance depends on infrastructure configuration and legal assessment, not only on code.
  - id: "12"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data model and metadata schema is published"
    api_operation_id:
    test:
    comment:
    documentation: >
      Each Building Block publishes its data model and metadata schema. Publication should follow the GovStack Schema Registry specification where available. Metadata should align with established cataloguing standards such as DCAT-AP, Dublin Core or ISO 11179. The published schema includes resource names, field types, required/optional markers and relationships between resources. A Building Block whose data model is not published cannot be integrated predictably.
  - id: "13"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Data is classified by sensitivity level"
    api_operation_id:
    test:
    comment:
    documentation: >
      Each Building Block classifies stored and processed data into at least three levels: public, internal and confidential. Classification is documented in the data model per data type or field group, not only at the system level. The labels determine which handling rules apply - including who may access the data, how it is transmitted and whether it may leave the jurisdiction. Specific labels may be adapted to national frameworks, but the minimum three-tier structure is maintained.
  - id: "14"
    status: PUBLISHED
    level: RECOMMENDED
    observability: AUDITABLE
    mutability: EXTENSIBLE
    statement: "Anonymization and pseudonymization is supported"
    api_operation_id:
    test:
    comment:
    documentation: >
      Building Blocks that store or process personal data support producing anonymized or pseudonymized copies for secondary use such as analytics, reporting or research. Anonymization makes re-identification practically impossible. Pseudonymization replaces direct identifiers with tokens reversible only through a separate protected mapping. The Building Block documents which technique it supports and when each applies.
---