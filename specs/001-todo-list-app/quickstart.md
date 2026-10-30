# Quickstart: Curso-PSWE-07 To-Do List

This guide describes how to run the application and validate its specified behavior after
implementation.

## Prerequisites

- Node.js 22 LTS and npm
- A current desktop or mobile browser

## Install and run

From the repository root:

```powershell
npm install
npx playwright install chromium
npm run dev
```

Open the local URL printed by Vite. The list should display the `Curso-PSWE-07` heading
and an empty state.

## Automated validation

In a separate terminal at the repository root:

```powershell
npm test
npm run test:acceptance
```

Expected results:

- Unit tests pass for required-title validation, creation defaults, status changes, and
  task operations through the repository interface.
- Browser acceptance tests pass for all three user stories: create/filter/open tasks;
  inspect/edit/toggle status; confirm/cancel deletion and persistence after reopening.

## Manual persistence check

1. Add a task with a title and description.
2. Mark it Done and verify the Done filter includes it.
3. Close and reopen the same app in the same browser profile.
4. Verify the task details and Done state remain saved.

The model and status rules are described in [data-model.md](./data-model.md).
