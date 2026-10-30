<!--
Sync Impact Report
Version change: unratified scaffold → 1.0.0
Modified principles: template placeholders → SIMPLICITY FIRST (YAGNI);
  SIMPLE, CLEAR DESIGN; STRUCTURED ARCHITECTURE;
  TEST-DRIVEN DEVELOPMENT (NON-NEGOTIABLE); SPEC IS THE SOURCE OF TRUTH
Added sections: none
Removed sections: none
Follow-up TODOs: none
-->
# Curso-PSWE-07 Constitution

## Core Principles

### I. SIMPLICITY FIRST (YAGNI)
Implement only what the spec requires; choose the simplest working solution and MUST NOT
add unjustified features, abstractions, configuration options, or dependencies. Any added
complexity MUST be justified in writing in the plan. Rationale: unnecessary complexity
increases cost without serving a requirement.

### II. SIMPLE, CLEAR DESIGN
Functions and modules MUST be small and single-purpose, with clear, intention-revealing names;
duplication MUST be abstracted only when it is real, and single-use abstractions and premature
optimization MUST be avoided. Rationale: straightforward design is easier to understand and
change.

### III. STRUCTURED ARCHITECTURE
Code MUST separate UI, application logic, and persistence, with dependencies flowing UI →
logic → persistence; UI MUST NOT access storage directly, and persistence MUST be hidden
behind a small replaceable interface. Rationale: clear boundaries make behavior testable
and storage replaceable.

### IV. TEST-DRIVEN DEVELOPMENT (NON-NEGOTIABLE)
Production code MUST follow Red-Green-Refactor: write a failing test, make it pass with
minimum code, then refactor; no production code may be added without a test requiring it.
Business logic MUST have unit tests, each user story MUST have an acceptance test mirroring
its acceptance scenarios, and tests MUST be fast and independent. Rationale: tests provide
continuous, reproducible evidence that required behavior works.

### V. SPEC IS THE SOURCE OF TRUTH
Every implementation task MUST trace to a spec requirement, and anything not specified
MUST remain out of scope; ambiguous requirements MUST be clarified before implementation.
Rationale: traceability prevents unintended behavior and scope growth.

## Additional Constraints

Implementation plans and task lists MUST identify the spec requirements they fulfill.
Any complexity beyond the simplest solution MUST have a written justification in the plan.

## Development Workflow

Every change MUST satisfy the applicable principles and tests before it is considered
complete. Reviews MUST verify requirement traceability, architecture boundaries, and the
required test coverage.

## Governance

This constitution governs project planning, implementation, and review. Amendments MUST be
documented here and approved by the project owner; each amendment MUST update the version
and last-amended date. Versioning follows semantic versioning: MAJOR for backward-incompatible
governance changes, MINOR for new or materially expanded principles, and PATCH for
non-semantic clarifications. Plans, implementation reviews, and completion checks MUST
verify compliance; exceptions MUST be documented and approved by the project owner.

**Version**: 1.0.0 | **Ratified**: 2026-10-22 | **Last Amended**: 2026-10-22
