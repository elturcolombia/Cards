<!--
Sync Impact Report:

- Version change: None -> 1.0.0
- Added sections:
  - Core Principles
  - Technology Stack
  - Development Workflow
  - Governance
- Templates requiring updates:
  - ✅ .specify/templates/plan-template.md
  - ✅ .specify/templates/spec-template.md
  - ✅ .specify/templates/tasks-template.md
  - ❔ .gemini/commands/*.toml (will check)
  - ✅ README.md
- Follow-up TODOs:
  - TODO(RATIFICATION_DATE): Determine original adoption date
-->
# Laravel Cards Constitution
<!-- Constitution for the Laravel Cards project. -->

## Core Principles

### I. Modular Design
Every feature should be developed in a modular way. Modules must be as self-contained as possible, with clear and documented interfaces. This promotes separation of concerns and reusability.

### II. API-First Development
All features should be exposed through a well-defined API. The API should be documented using an OpenAPI specification. This allows for parallel development of frontend and backend, and for easier integration with other services.

### III. Test-Driven Development (NON-NEGOTIABLE)
TDD is mandatory. Tests must be written before the implementation. The Red-Green-Refactor cycle is to be strictly enforced. This ensures that the code is testable and that the tests accurately reflect the requirements.

### IV. Comprehensive Testing
In addition to unit tests, integration tests are required for new features, especially for those that involve interactions between different modules, external services, or database schemas.

### V. Clear Versioning
The project will follow Semantic Versioning (MAJOR.MINOR.PATCH). All breaking changes must be clearly documented and communicated.

## Technology Stack

The project will use the following technology stack:
- Backend: PHP / Laravel
- Frontend: JavaScript / Vue.js (or other modern framework, to be decided)
- Database: MySQL / PostgreSQL
- Infrastructure: Docker

## Development Workflow

- All code changes must be submitted through Pull Requests.
- All PRs must be reviewed by at least one other developer.
- All PRs must pass all tests before being merged.
- All PRs must be up-to-date with the main branch.

## Governance
This Constitution supersedes all other practices. Amendments to this Constitution require a formal proposal, a review period, and approval from the project lead. All pull requests and code reviews must verify compliance with this constitution.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): Determine original adoption date | **Last Amended**: 2025-10-19