---
name: simplify-code
description: Reduce the reasoning required to understand and safely change code. Use for code or architecture simplification reviews and maintainability refactoring, excluding prose and formatting-only edits.
---

# Simplify Code

A design is simpler when an engineer can identify what owns a decision, follow
its data, and locate a normal change with fewer facts to coordinate. Prefer
clear names, cohesive responsibilities, direct data flow, and explicit domain
distinctions. Line and file counts do not measure that understanding.

Anchor a proposed change in a concrete source of confusion: competing
authorities, scattered knowledge, unnecessary indirection, or an obsolete
path. Inspect enough of the relevant behavior and callers to understand the
effect of changing it. Treat inherited structures, documentation, and tests
as evidence to evaluate; their existence does not make every implementation
choice a requirement.

Judge deletion, consolidation, extraction, and abstraction by whether they
make behavior easier to explain or a likely change easier to make. Similar
code may have different reasons to change. An abstraction earns its place
when it hides an incidental decision or localizes a responsibility. Making a
hidden rule explicit can improve the design even when it adds code.

Give each rule clear authority. Validation at multiple boundaries can serve
different purposes, such as client feedback, server trust, and database
integrity. Repeated checks do not automatically imply competing ownership.
Preserve boundaries that represent real domain or operational differences.

Respect whether the user requested a review or implementation. Preserve
behavior unless changing it is in scope. Check compatibility before removing
paths, and retain what correctness, security, observability, and necessary
performance require.

Choose the smallest coherent change with a concrete benefit. Leave code alone
when no worthwhile improvement is supported by the evidence. Stop when further
edits offer only cosmetic consistency or speculative flexibility; a review
with no recommended changes is a valid result.

Validate changed behavior with relevant checks proportional to its impact.
Explain what became easier to understand or change, what was verified, and
any material uncertainty. Include size statistics only when they help assess
the result.
