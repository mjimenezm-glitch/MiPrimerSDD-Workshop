# Tasks: Curso-PSWE-07 To-Do List

**Input**: Design documents from `specs/001-todo-list-app/`

**Prerequisites**: `plan.md`, `spec.md`, `research.md`, `data-model.md`, and
`quickstart.md`. No external contracts are defined.

**Tests**: Required by the project constitution. Follow Red-Green-Refactor: write each
unit and acceptance test before the production code it requires, verify it fails, then
implement the minimum behavior and refactor.

**Organization**: Tasks are grouped by user story so each story can be implemented and
validated as an increment.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: The task can run in parallel with other marked tasks because it edits a
  different file and has no unmet dependency.
- **[Story]**: The user story the task implements or tests.
- Every task description names the file to create or update.

## Path Conventions

- Single browser application: `src/` and `tests/` at the repository root.
- Feature planning and validation docs: `specs/001-todo-list-app/`.

## Phase 1: Setup

**Purpose**: Configure the browser app, development server, and automated browser test
runner.

- [ ] T001 Initialize `package.json` with Vite and Playwright development dependencies and `dev`, `build`, `test`, and `test:acceptance` scripts.
- [ ] T002 [P] Configure Vite's development server and build output in `vite.config.js`.
- [ ] T003 [P] Configure Playwright's test directory, Chromium project, and Vite web server in `playwright.config.js`.

## Phase 2: Foundational

**Purpose**: Shared prerequisites that block story work.

No separate production-code foundation is needed: the setup phase supplies the browser
server and test commands. Story tests are written before their corresponding feature
modules, in accordance with the constitution.

**Checkpoint**: Setup is complete; user-story tests and implementation can begin.

## Phase 3: User Story 1 - Create and find tasks (Priority: P1) - MVP

**Goal**: Create tasks, see them in a persistent list, filter by status, and open task
details.

**Independent Test**: With a clean browser profile, create a task with a title and
optional description; verify Pending status, list display, All/Pending/Done filtering,
empty states, and opening its details.

### Tests for User Story 1

- [ ] T004 [P] [US1] Write unit tests for `createTask` title validation, Pending default, task listing, and status filtering in `tests/unit/task-service.test.js`; run them and confirm they fail before implementing the service.
- [ ] T005 [P] [US1] Write unit tests for task creation and listing through an injected storage adapter in `tests/unit/task-repository.test.js`; run them and confirm they fail before implementing the repository.
- [ ] T006 [P] [US1] Write browser acceptance tests for empty and filtered lists, task creation, required-title validation, opening task details, the app title, responsive layout, 44-by-44-pixel targets, and 4.5:1 text contrast in `tests/acceptance/todo-list.spec.js`; run them and confirm they fail before implementing the UI.

### Implementation for User Story 1

- [ ] T007 [P] [US1] Implement `createTask`, `listTasks`, and `getTask` in `src/application/task-service.js`; reject titles without non-whitespace characters and create new tasks with `pending` status.
- [ ] T008 [P] [US1] Implement the local-storage task repository's `list` and `create` operations in `src/persistence/task-repository.js`, allowing a storage adapter to be injected for unit tests.
- [ ] T009 [US1] Create the browser document shell, app mount point, and `Curso-PSWE-07` document title in `index.html`.
- [ ] T010 [US1] Implement the task list, All/Pending/Done filters, empty states, Add task form, validation, and read-only task details in `src/ui/app.js`.
- [ ] T011 [US1] Style the list, form, detail view, completed task rows, and responsive base layout in `src/ui/styles.css`.
- [ ] T012 [US1] Connect the UI to the task service and persistent repository in `src/main.js`; mount the application from `index.html`.

**Checkpoint**: User Story 1 is independently usable; create tasks, filter and open them,
and verify they remain available after reloading the browser app.

## Phase 4: User Story 2 - Review and update a task (Priority: P2)

**Goal**: Show task details and let the user edit task text or toggle completion status.

**Independent Test**: Open an existing task, verify its displayed fields and status, edit
and cancel or save changes, reject a blank title, toggle status in both directions, and
return to the list.

### Tests for User Story 2

- [ ] T013 [P] [US2] Add unit tests for task updates, title validation, and toggling between `pending` and `done` in `tests/unit/task-service.test.js`; run them and confirm they fail before changing the service.
- [ ] T014 [P] [US2] Add browser acceptance tests for task detail labels, edit/save/cancel, blank-title validation, status-toggle labels and behavior, and the back control in `tests/acceptance/todo-list.spec.js`; run them and confirm they fail before changing the UI.
- [ ] T015 [P] [US2] Add repository unit tests proving updates preserve task identity and persist changed title and description in `tests/unit/task-repository.test.js`; run them and confirm they fail before changing the repository.

### Implementation for User Story 2

- [ ] T016 [P] [US2] Implement task update and completion-toggle operations in `src/application/task-service.js`, preserving the existing status during edits and other fields during status changes.
- [ ] T017 [P] [US2] Implement the repository `update` operation in `src/persistence/task-repository.js` so edited task fields persist.
- [ ] T018 [US2] Implement populated edit mode, Save and Cancel behavior, detail status display, dynamic status-toggle labels, and the back control in `src/ui/app.js`.

**Checkpoint**: User Stories 1 and 2 work; saved edits and status changes remain visible
in the list and task detail.

## Phase 5: User Story 3 - Delete a task and retain tasks (Priority: P3)

**Goal**: Confirm task deletion and retain all saved task state after the application is
closed and reopened.

**Independent Test**: Confirm and cancel deletion separately; reload the application and
verify created, edited, and completed tasks retain their latest values while deleted
tasks remain absent.

### Tests for User Story 3

- [ ] T019 [P] [US3] Add unit tests for deleting a task and leaving unrelated tasks unchanged in `tests/unit/task-service.test.js`; run them and confirm they fail before changing the service.
- [ ] T020 [P] [US3] Add repository unit tests proving deletion is persisted and deleted tasks do not reappear in `tests/unit/task-repository.test.js`; run them and confirm they fail before changing the repository.
- [ ] T021 [P] [US3] Add browser acceptance tests for warning-colored Delete, confirmation, cancellation, confirmed removal, and task-state persistence after page reload in `tests/acceptance/todo-list.spec.js`; run them and confirm they fail before changing the UI.

### Implementation for User Story 3

- [ ] T022 [P] [US3] Implement task deletion in `src/application/task-service.js`, removing only the selected task.
- [ ] T023 [P] [US3] Implement the repository `delete` operation in `src/persistence/task-repository.js` and persist the resulting task collection.
- [ ] T024 [US3] Implement the warning-colored Delete action, confirmation prompt, cancel behavior, and post-delete navigation in `src/ui/app.js`.

**Checkpoint**: All three stories work independently; confirm persisted task creation,
edits, status changes, and deletion across a browser reload.

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Validate accessibility, responsive behavior, and the documented end-to-end
workflow across the finished stories.

- [ ] T025 [P] Add browser acceptance assertions for mobile and desktop layouts, minimum 44-by-44-pixel interactive targets, and 4.5:1 contrast for all text in `tests/acceptance/todo-list.spec.js`.
- [ ] T026 Update `src/ui/styles.css` until the responsive layouts, target dimensions, and all text/background pairs satisfy FR-014 and FR-015 and the checks in `tests/acceptance/todo-list.spec.js` pass.
- [ ] T027 Run the setup, automated tests, and manual persistence scenarios from `specs/001-todo-list-app/quickstart.md`; update `specs/001-todo-list-app/quickstart.md` only if the runnable validation instructions need correction.

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies; must finish before running app or browser tests.
- **Foundational (Phase 2)**: No extra tasks; complete once Setup is ready.
- **User Stories (Phases 3-5)**: Begin after Setup. Each story's test tasks precede its
  production changes. Stories 2 and 3 use the task and UI modules established by Story 1,
  so deliver them in priority order.
- **Polish (Phase 6)**: Depends on all three user stories.

### User Story Dependencies

- **US1 (P1)**: Starts after Setup; delivers the list, create flow, filtering, detail
  opening, and initial persistent task operations.
- **US2 (P2)**: Depends on US1's task model, repository, and list/detail UI; adds update
  and status-toggle behavior.
- **US3 (P3)**: Depends on US1 and US2 task storage and navigation; adds deletion and
  reload-persistence acceptance coverage.

### Within Each User Story

- Write unit and acceptance tests first; verify they fail before implementing production
  behavior.
- Implement the application logic and persistence operations before wiring their UI.
- Keep each story's tests and implementation limited to its stated requirements.

### Parallel Opportunities

- During Setup, T002 and T003 can proceed in parallel after T001 provides the npm scripts.
- Within each story, separate unit-test files and acceptance-test changes can be prepared
  in parallel before implementation.
- Within each story, application-service and repository implementation tasks can proceed
  in parallel after the tests are written.
- US1 implementation tasks T007 and T008 are independent; UI integration depends on both.
- US2 implementation tasks T016 and T017 are independent; UI integration depends on both.
- US3 implementation tasks T022 and T023 are independent; UI deletion integration depends
  on both.
- US2 and US3 are not parallel because they modify shared UI, service, and repository
  files and have sequential story dependencies.

## Parallel Example: User Story 1

After T001, configure Vite in `vite.config.js` (T002) and Playwright in
`playwright.config.js` (T003) in parallel. After setup, write the unit tests in
`tests/unit/task-service.test.js`, repository tests in
`tests/unit/task-repository.test.js`, and acceptance tests in
`tests/acceptance/todo-list.spec.js` in parallel. Once those tests fail as expected,
implement the service and repository in parallel, then integrate the UI.

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Setup.
2. Write and fail the US1 unit and acceptance tests.
3. Implement task creation, listing, filtering, persistent storage, and read-only task
   details.
4. Run US1 tests and independently validate creation, filters, details, and reload.

### Incremental Delivery

1. Deliver US1 as the usable MVP.
2. Add US2 edit and completion workflows; rerun US1 and US2 tests.
3. Add US3 confirmed deletion and reload persistence checks; rerun all story tests.
4. Complete accessibility and responsive checks, then follow `quickstart.md`.

## Notes

- Every task uses the required checkbox, sequential ID, optional `[P]`, required story
  label for user-story tasks, and a concrete file path.
- Unit and acceptance tests are required by the project constitution, despite being
  optional in the generic task template.
- Feature requirements: US1 covers FR-001–FR-006 and FR-013–FR-017; US2 covers FR-007–
  FR-010; US3 covers FR-011–FR-012 and FR-018; the final polish validates FR-014–FR-015.
