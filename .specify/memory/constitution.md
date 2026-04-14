<!--
Sync Impact Report
- Version change: unversioned → 0.1.0
- Modified principles: (added) Training-Only Safety; Test-First; Security by Design; Observability & Simplicity; Infrastructure Abstraction
- Added sections: Constraints & Compliance; Development Workflow
- Removed sections: none
- Templates requiring updates: .specify/templates/tasks-template.md ✅ updated
- Templates reviewed (no change required): .specify/templates/plan-template.md ✅, .specify/templates/spec-template.md ✅, .specify/templates/agent-file-template.md ✅
- Follow-up TODOs: RATIFICATION_DATE left as TODO(RATIFICATION_DATE)
-->

# ContosoDashboard Constitution

## Core Principles

### Training-Only Safety (NON-PRODUCTION)
The repository and its artifacts are explicitly intended for training and educational use only. The codebase MUST NOT be used for production systems. Any mock authentication, seeded data, or relaxed security controls are allowed only under this training context and must be documented in associated feature specs.

### Test-First (MANDATORY)
All feature work MUST follow a test-first workflow: write acceptance and unit tests BEFORE implementing behavior; tests MUST fail, implementation is added, then tests MUST pass. Every user story accepted into a spec MUST include verifiable, automated tests or a documented rationale approved by maintainers.

### Security by Design
Security controls that can be applied in this training context (IDOR protection, role-based policies, authorization checks, secure cookie settings) MUST be present and exercised by tests. Any deviation for training reasons MUST be documented in the relevant spec and labeled `training-exception` with a mitigation plan for production hardening.

### Observability & Simplicity
Implementations MUST provide minimal, structured observability (structured logs, meaningful error messages) and prioritize simple, auditable implementations over clever but opaque solutions. Avoid premature optimization; prefer clear contracts and measurable goals.

### Infrastructure Abstraction & Migration Path
The codebase MUST use interface abstractions for infrastructure (storage, authentication, external services) so that training implementations can be swapped for production services (e.g., LocalFileStorage → Azure Blob Storage) without changing business logic. Migration guidance MUST be included in docs for any infrastructure replacement.

## Constraints & Compliance
This project is offline-first for training. It uses mock authentication, LocalDB, and local file storage by design. The repository MUST contain a clear statement in `README.md` that the project is training-only and list any intentional security or reliability limitations. Any contribution that introduces external service dependencies MUST include a configuration toggle to disable those services for offline training.

## Development Workflow
- Branching: Feature branches MUST follow `[###-feature-name]` convention; PRs target `main` or the active release branch.
- Reviews: All PRs require at least two approvals from repository maintainers or approvers listed in `MAINTAINERS.md` and a passing CI gate before merge.
- CI Gates: CI MUST run unit, integration (where applicable), and security linting. The CI definition SHOULD include a `Constitution Check` job that verifies mandatory items (tests present, license header, no dev-only secrets committed).
- Tests: Tests MUST be present for all user stories and acceptance criteria. Tests MUST execute in CI and be used as gating criteria for merges.
- Exceptions: Any approved exception to a core principle MUST be made via a documented PR that includes an explicit mitigation and a target timeline for remediation.

## Governance
Amendments to this constitution follow these rules:

1. Propose an amendment as a pull request updating this file. Include a migration/implementation plan for any operational impacts.
2. The PR MUST include at least two maintainer approvals and a successful CI run.
3. For changes that add or remove principles (semantic governance changes), bump MAJOR version. For additions such as a new principle or materially expanded guidance, bump MINOR. For wording/clarity fixes, bump PATCH.
4. After merge, update the `Last Amended` date and publish the change in project release notes.

**Version**: 0.1.0 | **Ratified**: TODO(RATIFICATION_DATE) | **Last Amended**: 2026-04-14

