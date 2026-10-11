# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]

**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: Filled by `/speckit-plan`; follow `.agents/skills/speckit-plan/SKILL.md`.
Read `.specify/memory/constitution.md` and `../docs/PRD.md` before planning.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: TypeScript + React [record exact supported versions in research]

**Primary Dependencies**: Vite, Tailwind CSS, React Router or compatible equivalent,
build-time prerendering/SSG, Cloudflare Pages Functions and Turnstile

**Storage**: Typed bilingual source modules for public content; migration-managed D1
inquiries/notification attempts, provisional pending privacy/data-location approval

**Testing**: [select TypeScript unit/integration, API, route/content, accessibility and
browser tools; include bilingual manual QA, Lighthouse and failure-recovery evidence]

**Target Platform**: Cloudflare Pages + Pages Functions; latest two major desktop
Chrome/Firefox/Safari/Edge versions, current iOS Safari and Android Chrome

**Project Type**: Prerendered bilingual corporate marketing and lead-generation website

**Performance Goals**: Mobile p75 LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.10;
Lighthouse mobile performance ≥ 90 and accessibility ≥ 95; distinguish field/synthetic evidence

**Constraints**: Arabic default RTL/English LTR parity, WCAG 2.1 AA target, nonblocking
reduced-motion-safe premium UX, approved content, secure durable leads, separate environments

**Scale/Scope**: Six primary page types × two locales, bilingual privacy utilities,
six service categories; no visitor accounts, CMS/admin dashboard, payments or instant quoting

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

Record PASS, approved exception, or NOT APPLICABLE with rationale for every principle.
Planned release evidence MUST identify owner/deadline; it does not establish a completed gate.

- **I — Scope/content:** Trace PRD IDs and MoSCoW priority; exclude v1.0 non-goals;
  identify verification/rights owners and gallery launch minimum (three projects/six images).
- **II — Architecture:** Use the prescribed stack, typed source content, all localized
  build-time HTML and minimal `/api/v1/` Functions; identify D1/privacy dependencies.
- **III — Localization:** Define `/` → `/ar/`, paired routes, lang/dir, context-preserving
  switch, missing-key build validation and separate RTL/LTR review.
- **IV — UX/accessibility:** Document tokens/component patterns, WCAG checks, focus/states,
  reduced motion, progressive fallbacks and the 360/390/768/1024/1440 viewport matrix.
- **V — SEO/performance:** Define metadata/canonical/hreflang/404 artifacts, per-route
  compressed budgets, media/font strategy and reproducible performance measurements.
- **VI — Security/privacy:** Define validation, Turnstile, rate limits, parameterized SQL,
  secret boundaries, restricted lead access, consent and legal/vendor/data-lifecycle approvals.
- **VII — Reliability:** Contract durable acceptance, idempotent replay/conflict, persistence
  before notification, failure recovery, daily reconciliation and accountable lead ownership.
- **VIII — Verification/operations:** Plan critical automated/manual coverage, CI, isolated
  staging, production smoke checks, safe logs/alerts, backup/restore, rollback and launch approval.

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Confirm and expand the proposed KEN layout for this feature.
  These paths describe a future plan, not existing implementation directories.
  Keep static frontend and edge Functions in the same project; justify deviations.
-->

```text
src/
├── components/          # Shared direction-aware UI and design system
├── pages/               # Six primary page templates plus utility/error pages
├── content/             # Typed, reviewed Arabic/English public records
├── lib/                 # Locale, validation and interaction helpers
└── styles/              # Tailwind and documented visual tokens

functions/api/v1/        # Pages Functions; public content/health and protected inquiry POST
migrations/             # D1 inquiry/notification SQL migrations
public/                 # Approved fonts/media and hosting artifacts
scripts/                # Build-time rendering, content/route/media validation

tests/
├── contract/
├── integration/
├── unit/
└── browser/             # Locales, keyboard, responsive and critical journeys
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
