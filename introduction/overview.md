---
title: Overview
---

## What this document is for

GovStack Cross-Functional Requirements (`govstack-cfr`) is the baseline every GovStack Building Block specification builds on. It sets out the operational qualities a software component needs before it can take part in a GovStack ecosystem: how it is developed, how it is deployed, how it is structured, what quality evidence it provides, how it is secured and how it handles data.

Without a shared baseline, two systems can each work well and still fail to exchange data, because they disagree on transport security, encodings, timestamps, API conventions or authentication patterns. Every integration then needs its own bilateral agreement on these basics. `govstack-cfr` settles those basics once, for every component, so that integration effort goes into what the systems actually do.

## What it does

The document does three things.

1. **It states testable requirements.** Each requirement has a stable identifier and three classifiers: a requirement level (REQUIRED or RECOMMENDED), an observability level (OBSERVABLE or AUDITABLE) and a mutability level (IMMUTABLE, EXTENSIBLE or REPLACEABLE). The classifiers are normative. They determine what a compliance assessment checks and how.
2. **It acts as the base for every Building Block specification.** A Building Block specification extends `govstack-cfr` in the way a class extends a base class. It inherits every requirement and adds its own functional requirements, API contracts and data structures. It may tighten an inherited requirement where the mutability classifier allows it, and it must record a rationale for any requirement it declares not applicable. It never restates the baseline, and it cannot weaken it. A solution that meets a Building Block specification therefore also meets `govstack-cfr`.
3. **It brings systems to protocol interoperability.** Components that meet the baseline share transport, formats, encoding, versioning and authentication conventions, and can exchange data without custom adaptors. This is the first of the three interoperability maturity states GovStack describes.

`govstack-cfr` is a single publication with one version. Its six domains (development, deployment, architecture, quality, security and data) are chapters of that publication, not separately versioned documents. A reference to `govstack-cfr-2.0.0` therefore names one complete set of requirements.

## Who uses it and how

| Reader | How they use it |
|---|---|
| **Governments** | Adopt it as the mandatory technical baseline for software procurement, or reference it from a national interoperability framework. |
| **Donors** | Write its REQUIRED requirements into terms of reference and funding conditions, and evaluate deliverables against them. |
| **Software providers** | Build new software against it, update existing software to meet it, or wrap software they cannot modify in an adaptor that meets it. Where no Building Block specification exists for their domain, they can still build against `govstack-cfr` alone. |
| **GovMarket** | Requires 100% compliance with its REQUIRED requirements, together with those of the relevant Building Block specification, before a solution is listed. RECOMMENDED requirements are scored and shown to buyers as a compliance percentage. |
| **Specification authors** | Declare `extends govstack-cfr-<version>` in their Building Block specification and build their functional requirements on top of the inherited baseline. |
| **Software architects** | Use it as a ready-made checklist of operational qualities instead of deriving one per project. |
| **AI-assisted development** | Uses the identified, classified requirements as context for generating, testing and reviewing code. |

Readers do not need to read the six domains in order. Each domain chapter stands on its own, and each requirement can be cited individually by its identifier.

## What limits it

- **It reaches protocol interoperability and stops there.** Meeting `govstack-cfr` does not make one implementation replaceable by another; that takes a shared service API contract, which only a Building Block specification provides. It also does not make data semantically consistent across institutions, which takes legal, organizational and semantic agreements outside any technical specification.
- **It specifies software components, not government services.** It says nothing about how a ministry runs a service, its eligibility rules, service levels or non-digital channels.
- **It does not confer legal compliance.** It is written so as not to block compliance with regulations such as GDPR or eIDAS, but meeting it does not make a deployment compliant with them. Legal compliance also depends on process and organizational practice.
- **It constrains interfaces and observable qualities, not implementations.** Where a choice has no effect on business function, it is not a requirement. A programming language, framework or vendor preference is never mandated.
- **It covers only the architectural side of digital sovereignty.** It requires components that can be configured for data residency, but the choice of hosting location, legal jurisdiction and operational continuity sit outside its requirements.

## Where to read further

`govstack-cfr` is a requirements specification. The architectural reasoning behind it lives in the [GovStack Architecture](https://specs.govstack.global/architecture/) Reference Architecture (`govstack:ra:architecture`). Go there for:

- the common terminology all GovStack specifications share, including the terms used in this document;
- the nine architecture principles the requirements put into practice;
- the three maturity states of technical interoperability, and where `govstack-cfr` sits among them;
- the Building Block approach, the Information Mediator and the architecture patterns GovStack advocates;
- the architecture scopes (government, system and component) and where this document applies within them;
- the ways governments, donors, providers and GovMarket use GovStack specifications, in more detail than above.
