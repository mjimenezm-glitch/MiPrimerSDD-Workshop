# Data Model: Curso-PSWE-07 To-Do List

## Task

Represents one item the user tracks.

| Field | Type | Required | Rules |
|-------|------|----------|-------|
| `id` | String | Yes | Stable identifier used to open, update, and delete the task. |
| `title` | String | Yes | Must contain at least one non-whitespace character. |
| `description` | String | No | May be empty; empty descriptions appear as muted "No description" on details. |
| `status` | `pending` or `done` | Yes | New tasks start `pending`; user can toggle between either state. |

### Relationships

- Tasks are independent; there are no categories, users, or related entities in scope.

### Lifecycle and validation

1. Creation requires a non-empty title and sets status to `pending`.
2. Editing may change title and description, but must preserve a valid title and current
   status.
3. Completion changes status between `pending` and `done`; other task fields remain
   unchanged.
4. Confirmed deletion removes the task; canceled deletion leaves it unchanged.

### Persistence boundary

Application logic uses a task repository interface for listing, creating, updating, and
deleting tasks. The browser local-storage adapter implements that interface. UI modules
MUST NOT read or write local storage directly. Unit tests can provide a fake repository.
