---
title: Foreword
---

Cross-Functional Requirements (CFR) were traditionally called Non-Functional Requirements, but there has been a shift in the recent decade to move away from this due to the implication that it has nothing to do with business function. Instead internationally known software architects such as Martin Fowler and Sam Newman have moved away from the term and suggested the use of cross-functional requirements instead.

**However this shift also means that there should be no technical requirements defined that have nothing to do with business function.** This means that if something can be done one way or another way and neither has any impact on actual business function, then neither of these ways should ever be a requirement. _In simpler terms: a programmers preference, if it does not impact business function, should never be a requirement._

Building Blocks are responsible for meeting all cross-functional requirements or specifying why specific requirements do not apply. Govstack compliance and certification processes will validate these requirements.

_In earlier versions of GovStack specifications these were called cross-cutting requirements._

## "Object-oriented" specifications

Every Building Block specification is an extension of the GovStack cross-functional requirements, much like a class extends a base class in object-oriented programming. The cross-functional requirements define the shared behaviour and constraints that all Building Blocks must satisfy - security, deployment, observability, data handling and so on. A Building Block specification inherits all of these rules and then adds its own functional requirements, API contracts and domain-specific logic on top. It can tighten or elaborate inherited rules where allowed, but it cannot contradict or weaken them.

<figure><img src="/assets/Govstack_object_oriented.png" alt="Image showing how the Cross-Functional Requirements specification is a parent for Building Block specification" width="248"><figcaption></figcaption></figure>

This means that any system that meets a Building Block specification automatically meets the cross-functional baseline as well, and any tool or process built to validate that baseline works across every Building Block without modification.

Building Blocks however should not copy-paste and repeat the already existing core specifications. Instead the core specifications should be taken into account for compliance (including for automatic testing) of software solutions.

### Referring to GovStack core cross-functional requirements

Since Building Block specifications need to refer to these cross-functional requirements, such as for the extension purposes covered above, then GovStack CFR can be universally referred to as:

**govstack:spec:cfr**

Or when referring to a specific version:

**govstack:cfr?version=2.0.0**

_Sub-categories of GovStack CFR (such as govstack:spec:cfr#data) do not have an individual version._

