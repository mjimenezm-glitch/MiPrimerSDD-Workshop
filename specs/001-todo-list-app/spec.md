# Feature Specification: Curso-PSWE-07 To-Do List

**Feature Branch**: `001-todo-list-app`

**Created**: 2026-10-22

**Status**: Draft

**Input**: User description: Build a simple to-do list application named "Curso-PSWE-07" to organize and track daily tasks, with list and detail screens, persistent task storage, and a clean, responsive visual design.

## Clarifications

### Session 2026-10-22

- Q: What minimum text-contrast standard should the application meet? → A: WCAG 2.2 AA, with a minimum contrast ratio of 4.5:1 for all text.

## User Scenarios & Testing

### User Story 1 - Create and find tasks (Priority: P1)

As a user, I want to add tasks and see or filter them in a to-do list so I can keep track of work that is pending or done.

**Why this priority**: Creating and viewing tasks is the essential value of the application.

**Independent Test**: Create tasks with and without descriptions, view them in the list, and switch among All, Pending, and Done filters.

**Acceptance Scenarios**:

1. **Given** the list contains no tasks, **When** the user opens the list, **Then** a friendly empty state is shown.
2. **Given** the user is on the list screen, **When** the user selects Add task, enters a title and optional description, and saves, **Then** the new pending task appears in the list.
3. **Given** the user submits a task without a title, **When** the form validates, **Then** a validation message is shown and no task is created.
4. **Given** the list contains pending and done tasks, **When** the user selects Pending or Done, **Then** only tasks with the selected status are shown and that filter is highlighted.
5. **Given** the active filter has no matching tasks, **When** the list is displayed, **Then** a friendly empty state is shown.
6. **Given** the user sees a task row, **When** the user opens it, **Then** the task detail screen for that task is displayed.

---

### User Story 2 - Review and update a task (Priority: P2)

As a user, I want to inspect, edit, and change a task's completion status so its details and progress stay accurate.

**Why this priority**: Editing task details and completion status keeps the list useful after tasks are created.

**Independent Test**: Open an existing task, verify its details and status, edit it, and toggle its completion state.

**Acceptance Scenarios**:

1. **Given** an existing task, **When** the user opens its detail screen, **Then** the title, description or muted "No description" text, and Done or Pending status are shown.
2. **Given** the task detail screen is open, **When** the user selects Edit, **Then** a form populated with the task's title and description is shown with Save and Cancel actions.
3. **Given** the user edits a task, **When** the user saves a non-empty title and description, **Then** the updated details are shown and retained.
4. **Given** the user edits a task, **When** the user clears the title and saves, **Then** a validation message is shown and the task is not saved with an empty title.
5. **Given** the user edits a task, **When** the user selects Cancel, **Then** the unsaved changes are discarded.
6. **Given** a task is Pending, **When** the user selects Mark as done, **Then** its status changes to Done; when it is Done and the user selects Mark as not done, **Then** its status changes to Pending.
7. **Given** the user is viewing task details, **When** the user selects the back control, **Then** the to-do list is shown.

---

### User Story 3 - Delete a task and retain tasks (Priority: P3)

As a user, I want to delete tasks with confirmation and find my saved tasks after reopening the application so I can maintain a reliable list.

**Why this priority**: Deletion and durable storage support ongoing maintenance and reliable use of the list.

**Independent Test**: Delete an existing task with and without confirming, then close and reopen the application and verify remaining tasks and their states.

**Acceptance Scenarios**:

1. **Given** a task detail screen is open, **When** the user selects Delete, **Then** a confirmation prompt is shown before deletion.
2. **Given** a deletion confirmation is shown, **When** the user cancels, **Then** the task remains unchanged.
3. **Given** a deletion confirmation is shown, **When** the user confirms, **Then** the task is deleted and no longer appears in the list.
4. **Given** tasks have been created, edited, or marked done, **When** the user closes and reopens the application, **Then** those tasks retain their saved titles, descriptions, and completion statuses.

### Edge Cases

- A task with an empty or whitespace-only title cannot be saved; the form identifies the title as required.
- A missing or empty description is allowed and is represented on the detail screen as muted "No description" text.
- When filtering yields no tasks, the list shows a friendly empty state rather than an empty unexplained screen.
- Canceling an edit or a deletion confirmation leaves the existing task unchanged.
- The layout remains usable at mobile and desktop viewport sizes, including on screens where content must scroll.

## Requirements

### Functional Requirements

- **FR-001**: The application MUST show a to-do list screen and a detail screen for an individual task.
- **FR-002**: The list screen MUST display each task's title and completion status, and completed task titles MUST appear with strikethrough and muted color.
- **FR-003**: The list screen MUST let users choose All, Pending, or Done; the active choice MUST be visibly highlighted and results MUST match the selected status.
- **FR-004**: Users MUST be able to open a task's detail screen by selecting its list row.
- **FR-005**: Users MUST be able to create a task with a required title, optional description, and initial Pending status.
- **FR-006**: The create and edit forms MUST reject an empty or whitespace-only title with a visible validation message.
- **FR-007**: The detail screen MUST show the task title, its description or muted "No description" text, and a visible Done or Pending status label.
- **FR-008**: Users MUST be able to edit a task's title and description using the same form as task creation, with Save and Cancel actions.
- **FR-009**: Users MUST be able to switch a task between Done and Pending; the corresponding action label MUST change to Mark as done or Mark as not done.
- **FR-010**: Users MUST be able to return from task details to the list using a back control.
- **FR-011**: Deleting a task MUST require confirmation; canceling MUST preserve it and confirming MUST remove it from the list.
- **FR-012**: Created tasks and changes to their title, description, and completion status MUST persist after closing and reopening the application.
- **FR-013**: The list screen header and the application/window title MUST display "Curso-PSWE-07".
- **FR-014**: The application MUST use a clean, minimal visual style with a light background, generous white space, one sans-serif font family, and one accent color for primary actions and the active filter. Titles MUST be larger and bolder than descriptions.
- **FR-015**: Interactive touch and click targets MUST be at least 44 by 44 pixels, text MUST meet WCAG 2.2 AA with a minimum contrast ratio of 4.5:1 against its background, and layouts MUST support mobile and desktop screen sizes.
- **FR-016**: The list MUST show a short, friendly empty state when there are no tasks or the active filter has no matches.
- **FR-017**: The Add task action MUST be clearly visible on the list screen and open the task form.
- **FR-018**: The detail screen MUST provide Edit, status-toggle, and Delete actions; Delete MUST use a distinct warning color.

### Key Entities

- **Task**: A user-created item with a required title, optional description, and completion status of Done or Pending.

## Success Criteria

### Measurable Outcomes

- **SC-001**: In acceptance testing, users can create a task with a title and optional description, and see it in the list in no more than three actions after opening the list.
- **SC-002**: In acceptance testing, each of the All, Pending, and Done filters displays exactly the tasks with the corresponding status.
- **SC-003**: In acceptance testing, all task titles, descriptions, and statuses remain unchanged after closing and reopening the application.
- **SC-004**: Every required task flow in the acceptance scenarios can be completed successfully on both mobile and desktop viewport sizes.
- **SC-005**: All interactive targets measure at least 44 by 44 pixels, and every text/background combination has a contrast ratio of at least 4.5:1.
- **SC-006**: Every specified empty, validation, detail, status, edit, and deletion-confirmation state is visibly represented in acceptance testing.

## Assumptions

- The application is for a single local user; accounts, categories, due dates, priorities, search, and synchronization are excluded.
- A task begins in Pending status when created.
- A title containing only whitespace is treated as empty.
- No maximum title or description length is specified; the application accepts user-entered content within its practical display limits.
- The target devices are mobile and desktop; the application remains usable at both sizes, with no specific browser or operating-system list specified.
