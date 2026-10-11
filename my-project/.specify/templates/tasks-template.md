---

description: "Task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`

**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Verification**: Include constitution-required critical unit/integration/API/route checks
and bilingual manual acceptance tasks even when the feature request does not repeat them.
Choose meaningful checks proportional to risk; do not add tests that merely mirror implementation.

**Governance**: Read `.specify/memory/constitution.md` and `../docs/PRD.md`. Trace tasks
to feature requirements/PRD IDs. Story P1/P2/P3 ordering is separate from PRD release priorities.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

- **KEN frontend/content**: `src/components/`, `src/pages/`, `src/content/`, `src/lib/`
- **Edge/backend**: `functions/api/v1/`, `migrations/`; no separate Express server
- **Assets/build/verification**: `public/`, `scripts/`, `tests/`
- Confirm exact paths and file extensions against plan.md; these are proposed conventions

<!--
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.

  The /speckit-tasks command MUST replace these with actual tasks based on:
  - User stories from spec.md (with their priorities P1, P2, P3...)
  - Feature requirements from plan.md
  - Entities from data-model.md
  - Endpoints from contracts/

  Tasks MUST be organized by user story so each story can be:
  - Implemented independently
  - Tested independently
  - Delivered as an MVP increment

  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure

- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize React/TypeScript/Vite/Tailwind project per approved plan
- [ ] T003 [P] Configure linting and formatting tools

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

Examples of foundational tasks (adjust based on your project):

- [ ] T004 Define D1 inquiry/notification migrations in migrations/ and privacy approval dependencies
- [ ] T005 [P] Establish Arabic/English route model and direction-aware shell in src/
- [ ] T006 [P] Define inquiry validation, Turnstile, rate limits and idempotency in functions/api/v1/
- [ ] T007 Define typed content/locale models and build validation in src/content/ and scripts/
- [ ] T008 Configure safe error states, correlation logs and notification recovery per plan
- [ ] T009 Configure isolated staging/production bindings, secrets and CI per plan

**Checkpoint**: Foundation ready. The first critical slice MUST prove secure durable inquiry
storage and recovery after notification failure before decorative enhancements begin.

---

## Phase 3: User Story 1 - [Title] (Priority: P1) 🎯 MVP

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Verification for User Story 1 (constitution-required coverage) ⚠️

> Define expected behavior before implementation; critical automated checks and both-locale
> manual acceptance MUST pass before the story is complete.

- [ ] T010 [P] [US1] Contract checks for [endpoint including negative/replay/conflict cases] in tests/contract/[name].test.ts
- [ ] T011 [P] [US1] Bilingual integration checks for [journey including storage/notification failure] in tests/integration/[name].test.ts

### Implementation for User Story 1

- [ ] T012 [P] [US1] Create [public content model] in src/content/[name].ts
- [ ] T013 [P] [US1] Create [validation model] in src/lib/[name].ts
- [ ] T014 [US1] Implement [shared interaction] in src/components/[name].tsx (depends on T012, T013)
- [ ] T015 [US1] Implement [endpoint] in functions/api/v1/[name].ts
- [ ] T016 [US1] Add validation and error handling
- [ ] T017 [US1] Add logging for user story 1 operations

**Checkpoint**: At this point, User Story 1 should be fully functional and testable independently

---

## Phase 4: User Story 2 - [Title] (Priority: P2)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Verification for User Story 2 (constitution-required coverage) ⚠️

- [ ] T018 [P] [US2] Contract/content checks for [capability] in tests/contract/[name].test.ts
- [ ] T019 [P] [US2] Bilingual integration checks for [journey] in tests/integration/[name].test.ts

### Implementation for User Story 2

- [ ] T020 [P] [US2] Create [typed bilingual content] in src/content/[name].ts
- [ ] T021 [US2] Implement [shared component] in src/components/[name].tsx
- [ ] T022 [US2] Implement [page/feature] in src/pages/[name].tsx
- [ ] T023 [US2] Integrate with User Story 1 components (if needed)

**Checkpoint**: At this point, User Stories 1 AND 2 should both work independently

---

## Phase 5: User Story 3 - [Title] (Priority: P3)

**Goal**: [Brief description of what this story delivers]

**Independent Test**: [How to verify this story works on its own]

### Verification for User Story 3 (constitution-required coverage) ⚠️

- [ ] T024 [P] [US3] Contract/content checks for [capability] in tests/contract/[name].test.ts
- [ ] T025 [P] [US3] Bilingual integration checks for [journey] in tests/integration/[name].test.ts

### Implementation for User Story 3

- [ ] T026 [P] [US3] Create [typed bilingual content] in src/content/[name].ts
- [ ] T027 [US3] Implement [shared component] in src/components/[name].tsx
- [ ] T028 [US3] Implement [page/feature] in src/pages/[name].tsx

**Checkpoint**: All user stories should now be independently functional

---

[Add more user story phases as needed, following the same pattern]

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect multiple user stories

- [ ] TXXX [P] Documentation updates in docs/
- [ ] TXXX Code cleanup and refactoring
- [ ] TXXX Performance optimization across all stories
- [ ] TXXX [P] Critical unit checks for validation/locale behavior in tests/unit/
- [ ] TXXX Security hardening
- [ ] TXXX Run quickstart.md validation
- [ ] TXXX [P] Review approved Arabic/English copy, claims, image rights and gallery minimum
- [ ] TXXX [P] Verify RTL/LTR layouts, keyboard/screen-reader/focus and reduced motion at required widths
- [ ] TXXX [P] Audit 12 prerendered primary routes, privacy pages, canonical/hreflang, sitemap and 404s
- [ ] TXXX Measure per-route budgets and mobile Lighthouse/Web Vitals against PRD baselines
- [ ] TXXX Verify validation/Turnstile/rate limits/idempotency and no public lead/secret/PII exposure
- [ ] TXXX Exercise notification recovery, daily reconciliation, safe alerts and operator retrieval
- [ ] TXXX Obtain privacy/vendor/data-location/retention and approved backup/deletion/export decisions
- [ ] TXXX Verify production contacts, test lead persistence, backup restore, rollback and handover
- [ ] TXXX Record all P0 acceptance evidence and KEN Management launch authorization

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Final Phase)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) - May integrate with US1 but should be independently testable
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) - May integrate with US1/US2 but should be independently testable

### Within Each User Story

- Define acceptance behavior before implementation; required checks MUST pass before completion
- Models before services
- Services before endpoints
- Core implementation before integration
- Story complete before moving to next priority

### Parallel Opportunities

- All Setup tasks marked [P] can run in parallel
- All Foundational tasks marked [P] can run in parallel (within Phase 2)
- Once Foundational phase completes, all user stories can start in parallel (if team capacity allows)
- All tests for a user story marked [P] can run in parallel
- Models within a story marked [P] can run in parallel
- Different user stories can be worked on in parallel by different team members

---

## Parallel Example: User Story 1

```bash
# Independent verification tasks for User Story 1:
Task: "Contract checks for [endpoint] in tests/contract/[name].test.ts"
Task: "Integration checks for [user journey] in tests/integration/[name].test.ts"

# Launch all models for User Story 1 together:
Task: "Create [content model] in src/content/[name].ts"
Task: "Create [validation model] in src/lib/[name].ts"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL - blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: Test User Story 1 independently
5. Preview/demo if ready; public launch requires all P0 and constitution release gates

### Incremental Delivery

1. Complete Setup + Foundational → Foundation ready
2. Add User Story 1 → Test independently → Deploy/Demo (MVP!)
3. Add User Story 2 → Test independently → Deploy/Demo
4. Add User Story 3 → Test independently → Deploy/Demo
5. Each story adds value without breaking previous stories; public launch still requires all P0 gates

### Parallel Team Strategy

With multiple developers:

1. Team completes Setup + Foundational together
2. Once Foundational is done:
   - Developer A: User Story 1
   - Developer B: User Story 2
   - Developer C: User Story 3
3. Stories complete and integrate independently

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- Define expected behavior first and retain automated/manual acceptance evidence
- Commit after each task or logical group
- Stop at any checkpoint to validate story independently
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence
