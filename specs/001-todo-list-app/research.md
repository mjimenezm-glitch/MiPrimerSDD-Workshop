# Research: Curso-PSWE-07 To-Do List

## Decision: Build a client-side browser application with plain web standards

- **Decision**: Use semantic HTML, CSS, and JavaScript ES modules, served during development
  by Vite.
- **Rationale**: The specification requires responsive mobile and desktop screens and an
  application/window title. A browser application satisfies those requirements with the
  fewest runtime parts and without introducing an unrequested UI framework.
- **Alternatives considered**:
  - A component framework: rejected because the two-screen feature does not require its
    extra runtime or abstractions.
  - A native desktop or mobile application: rejected because no single native platform
    is specified and a responsive browser UI matches the target sizes.

## Decision: Store the single user's tasks in browser local storage

- **Decision**: Store task records in local storage for the current browser profile and
  application origin, accessed through a small task-repository interface.
- **Rationale**: The feature is local to one user, has a small data model, and requires
  persistence across application restarts but not synchronization or server access.
  Keeping storage behind an interface preserves testability and replaceability.
- **Alternatives considered**:
  - A remote database or synchronization service: rejected because accounts, network
    storage, and synchronization are out of scope.
  - An in-memory collection: rejected because it would not meet the persistence
    requirement.
  - IndexedDB: rejected because the specified small task records do not require its
    additional asynchronous storage capabilities.

## Decision: Use built-in unit testing and focused browser acceptance testing

- **Decision**: Use Node.js's built-in test runner for task-service unit tests and
  Playwright for end-to-end browser acceptance tests.
- **Rationale**: Built-in unit testing avoids an extra unit-test framework; browser
  automation verifies the required responsive UI flows, form validation, and persistence.
  These tests implement the constitution's Red-Green-Refactor and user-story acceptance
  test requirements.
- **Alternatives considered**:
  - Manual-only acceptance checks: rejected because they are not repeatable automated
    acceptance coverage.
  - A custom browser harness: rejected because it duplicates functionality provided by
    a focused test tool.

## Decision: Do not add an external contract directory

- **Decision**: Define no public API or external service contract.
- **Rationale**: The feature is a self-contained browser application with no integration
  or interface exposed to other systems. The internal persistence boundary is documented
  in the data model.
