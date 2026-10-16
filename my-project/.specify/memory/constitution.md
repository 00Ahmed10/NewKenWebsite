<!--
Sync Impact Report — 2026-10-16 staging architecture amendment
Version change: 1.0.0 → 2.0.0 (MAJOR: incompatible redefinition of platform MUSTs).
Authority: explicit user instruction to amend PRD and constitution for staging only.
This records technical documentation authorization, not KEN stakeholder/project-owner
identity verification, legal clearance, deployment or operational acceptance.
Rationale: adopt the user-selected Docker/Railway/secure Node.js/PostgreSQL staging
architecture assessed in specs/001-phase1-lead-foundation/architecture-change-impact.md.
Modified principles:
  I. PRD Scope and Verifiable Content — source revision v1.1; product v1.0 unchanged.
  II. Typed React and Cloudflare Architecture → Typed React and Staging Architecture.
  VI. Secure Boundaries and Minimal Personal Data — environment/roles/privacy boundary.
  VII. Durable Inquiries and Recoverable Notifications — atomic PostgreSQL/outbox,
       concurrent replay/notice rollover and staging authority; same visitor guarantees.
  VIII. Evidence-Based Quality and Operational Readiness — CI enforcement and verified
        Node/Docker/PostgreSQL/monitoring/operations; no threshold reduction.
Principles III–V unchanged. Architecture/Release Constraints and documentation-only
Governance scope updated; Amendment History added. No principles/guarantees removed.
Coordinated source: ../docs/PRD.md updated to v1.1; Draft stakeholder status retained.
Consistency propagation — intentionally deferred by the user's two-document boundary:
  ⚠ .specify/templates/plan-template.md — Pages/Functions/D1 stack/paths/checks pending.
  ⚠ .specify/templates/tasks-template.md — backend paths/sample D1 tasks pending.
  ⚠ .specify/templates/spec-template.md — PRD revision and approval-boundary sync pending.
  ⚠ specs/001-phase1-lead-foundation/{spec,plan,tasks,research,data-model}.md pending.
  ⚠ specs/001-phase1-lead-foundation/{dependencies,operations,quality-strategy,quickstart}.md
    and contracts/ pending; design-direction.md only if context needs a dated note.
  ⚠ AGENTS.md managed context reviewed; entry links remain valid, current plan is stale
    for migrated implementation until coordinated update and fresh read-only analysis.
  .specify/templates/commands/*.md, README.md and docs/quickstart.md absent.
  Preserve the assessment and all historical T001/T002 evidence; do not rewrite old hashes.
Pre-amendment SHA-256 (actual bytes; retain historical evidence separately):
  ../docs/PRD.md: 3b5dee7c002d6921f4bce57e59b217d9186511fef4434564c84679ed4f1a4154
  .specify/memory/constitution.md: fd420041c8b92c2902c47e6d84821512b729a76570d597c06d70fbf44d32f386
No package/lock/task/code/install/deploy/commit/push changes authorized in this step.
Hooks: existing repository verified; no initialization performed. Optional commit hook
skipped under the user's no-commit instruction. No hook changed.
External follow-up: stakeholder PRD/architecture acceptance, production architecture/parity,
Saudi privacy/transfers/locations (including metadata), staging access/roles/region,
operations/monitoring/backup/restore, content/contacts, live email and schedule review.
These are pending gates, not approved capabilities. No unexplained placeholders added.
Historical initial-adoption Sync Impact Report follows unchanged.
-->

<!--
Sync Impact Report
Version change: unratified placeholder template → 1.0.0 (initial adoption).
Modified principles: all five unnamed template slots replaced with concrete KEN principles.
Added principles:
  I. PRD Scope and Verifiable Content
  II. Typed React and Cloudflare Architecture
  III. Arabic-First Bilingual Parity
  IV. Premium, Accessible and Progressive UX
  V. Crawlable Content and Measured Performance
  VI. Secure Boundaries and Minimal Personal Data
  VII. Durable Inquiries and Recoverable Notifications
  VIII. Evidence-Based Quality and Operational Readiness
Added sections: Architecture and Release Constraints; Development Workflow and Quality Gates.
Removed sections: generic placeholder examples only; no adopted rules removed.
Consistency propagation:
  ✅ .specify/templates/plan-template.md — stack, layout and explicit Constitution Check gates.
  ✅ .specify/templates/spec-template.md — PRD traceability and mandatory quality/approval criteria.
  ✅ .specify/templates/tasks-template.md — required verification and KEN task categories.
  ✅ AGENTS.md — constitution and PRD references; current plan remains implementation guidance.
  Reviewed .specify/templates/constitution-template.md; generic source template unchanged.
  .specify/templates/commands/*.md absent; no command templates require migration.
  README.md, docs/quickstart.md and feature plans absent; no existing artifacts to migrate.
Deferred placeholders: none.
External follow-up: PRD stakeholder sign-off, brand/content/contact assets, production domain,
email provider/credentials, lead owner, privacy/data-location/retention and backup approvals.
These remain release dependencies, not approval claims made by this constitution.
-->

# KEN Elevators Website Constitution

## Core Principles

### I. PRD Scope and Verifiable Content

Development MUST trace requirements and acceptance evidence to PRD-001 v1.1 in
`../docs/PRD.md`. v1.0 MUST deliver Home, About Us, Services, Projects, Why Choose Us
and Contact Us in both locales, plus bilingual privacy utility content. The Services
page MUST cover the six defined categories: villa, school, administrative, restaurant,
installation and maintenance. Every primary page MUST offer a clear quotation/contact
path. All P0 requirements MUST pass before public release. P1 enhancements MUST preserve
P0 behavior, accessibility and speed. Scope changes MUST record Product Owner approval
and schedule impact. Accounts, CMS/admin dashboards, payments, CRM integration, native
apps, chatbot, maintenance tracking and instant quoting remain outside v1.0.

Claims, contacts, service coverage, project captions and image rights MUST be verified
and approved by KEN. Licensed editorial imagery MUST remain distinguishable from genuine
KEN project evidence. Public launch MUST include at least three approved real projects
and six approved project images with internal permission references. Staging MUST use
explicit empty states or suppress unverified contact actions. Fabricated reviews,
credentials, projects and placeholder contact numbers MUST NOT be published. These rules
protect buyer trust and keep the release focused on credible lead generation.

### II. Typed React and Staging Architecture

The frontend MUST use React, TypeScript, Vite and Tailwind CSS, typed content models,
shared components and documented design tokens. React Router or a compatible equivalent
MUST support stable locale routes. Build-time prerendering/SSG MUST deliver meaningful
HTML for all 12 primary localized URLs and legal content before hydration. Initial public
content MUST NOT require a client-side API fetch.

Version-controlled bilingual modules MUST remain the public content system of record.
The build MUST validate translation keys, stable IDs, image references, route pairings
and metadata. Staging MUST use Docker on Railway with a secure Node.js service serving
the prerendered frontend and same-origin minimal `/api/v1/` API, plus private PostgreSQL.
Explicit SSG MUST preserve meaningful initial HTML, metadata, locale direction and
status-coded localized 404s; disabling runtime SSR MUST NOT reduce delivery to a client-only
SPA. Node delivery MUST enforce redirects, CSP/security headers, compression and safe
cache behavior; inactive Pages directive files cannot satisfy those requirements.
No Express framework, visitor JWT or user table is required. Public GET resources MUST
expose only approved public content/configuration, never inquiries. PostgreSQL MUST store
migration-managed staging inquiries and notification attempts as a transactional outbox.
Turnstile MUST be verified server-side. Production hosting/storage MUST remain a separate
approved decision with staging/production parity assessment and equivalent guarantees.
Architecture changes MUST record rationale and authorization before adoption; selection
of staging technology MUST NOT authorize deployment, real-data intake or unapproved
processing locations. Privacy, access and operational readiness MUST be demonstrated.

### III. Arabic-First Bilingual Parity

`/` MUST resolve to `/ar/`. Arabic MUST use `lang="ar" dir="rtl"`; English MUST use
`lang="en" dir="ltr"` at `/en/`. Geolocation redirects MUST NOT override a deliberate
locale choice. Both locales MUST provide identical capabilities and direct-link refresh.
Language switching MUST preserve the corresponding page when available.

All public copy, navigation, forms, error/success/empty/loading states, image alternatives
and SEO metadata MUST have reviewed Arabic and English variants. Missing translations
MUST fail the build; unexpected runtime absence MUST offer a localized explanation and
safe locale homepage, never raw keys. Shared components MUST handle logical layout,
directional icons, breadcrumbs, focus order and mixed-direction phone/numeric content.
Arabic typography, clipping and keyboard/screen-reader behavior MUST be reviewed
independently from English, with native-speaker editorial approval in both locales.

### IV. Premium, Accessible and Progressive UX

The visual system MUST express dark navy, brushed gold and warm neutrals through consistent
typography, spacing, responsive imagery and reusable navigation, hero, CTA, card, form,
section and modal patterns. Exact colors, licensed Arabic/Latin fonts and brand assets
MUST receive visual sign-off. Luxury styling MUST preserve readability and conversion.

Public experiences MUST meet the WCAG 2.1 AA target: semantic landmarks, labels, text
alternatives, sufficient contrast, visible focus and keyboard access. Gold MUST NOT be
used where text contrast fails. Menus/modals MUST support Escape and focus restoration;
modal viewers MUST trap focus appropriately. Layouts MUST be checked at 360, 390, 768,
1024 and 1440 CSS pixels without horizontal overflow or clipped RTL text. Touch targets
MUST be at least 44 × 44 CSS pixels where practicable; exceptions MUST be documented.

Motion MUST be decorative, restrained, interruptible and progressively enhanced.
Reduced motion MUST suppress parallax, lengthy movement and autoplay-style effects.
Content/CTAs MUST remain available if animations fail or enhancements are disabled.
Scroll hijacking and hover-only actions MUST NOT be introduced. Asynchronous actions
MUST show pending and localized success/error states; recoverable failures MUST preserve
input. Forms MUST focus the first invalid field after attempted submit and confirmation
after success. External app launches MUST require an explicit user action.

### V. Crawlable Content and Measured Performance

Every primary localized URL MUST serve distinct localized titles/descriptions, a matching
canonical and reciprocal `hreflang`. Build/deployment checks MUST validate sitemap,
robots directives, social metadata and properly status-coded localized 404s. Structured
data MUST include only verified company facts; absent facts MUST be omitted.

The PRD release baselines MUST be measured: mobile p75 LCP ≤ 2.5 s, INP ≤ 200 ms and
CLS ≤ 0.10; Lighthouse mobile performance ≥ 90 for each main template in both locales.
Field data MUST be used when sufficient; repeatable throttled mobile synthetic checks
MUST provide prelaunch evidence. Synthetic scores MUST NOT be represented as field
percentiles. The two-second critical-content objective MUST be measured on an agreed
profile, with practicability exceptions recorded. Compressed per-route asset budgets
MUST be defined during foundation planning and enforced in build/release review.

Media MUST use responsive dimensions/srcset, AVIF/WebP with JPEG fallback, reserved layout
space and below-fold lazy loading. Critical hero imagery MUST load promptly; lightweight
posters MUST take precedence over blocking video. Licensed fonts MUST be served locally
and subset/preloaded where feasible. Gallery/lightbox and enhanced motion MUST be split
and deferred. Unnecessary blocking third-party scripts MUST NOT be introduced. Added
enhancements MUST demonstrate that the performance baselines still pass.

### VI. Secure Boundaries and Minimal Personal Data

The inquiry endpoint MUST validate allowlisted fields, types, lengths/enums and total
payload size independently of client validation. It MUST enforce Turnstile, configurable
rate limits, idempotency and parameterized database statements. Delivery MUST use HTTPS.
Secrets MUST exist only in server environment bindings/provider secret stores, never
frontend bundles or public configuration. Errors MUST use safe status codes/correlation
references without raw stack traces or internal details.

Only data needed for lead response MUST be collected, with explicit mandatory privacy
acknowledgement and recorded notice version/timestamp. Real personal-data intake in any
environment MUST await separate authorization, approved bilingual privacy text and Saudi
PDPL legal review of lawful basis, retention, processor/subprocessor locations and
cross-border transfers, including app/database/log/backup and notification processing.
Staging MUST remain protected, noindex and synthetic-only; tester network/access metadata
MUST also receive processing/location review. Platform selection is not legal clearance.
Proposed 12-month retention and daily restricted encrypted backups with 30-day rolling
retention MUST NOT be treated as approved policy. Owners MUST approve periods, locations and feasible provider procedures,
including deletion/export and a restore drill.

Lead access MUST use provider organization roles, least privilege and MFA, with distinct
PostgreSQL application, migration and operational roles; public API credentials MUST NOT
have owner/superuser privileges. Staging access MUST protect every exposed document,
asset and API alias before delivery, with reviewed credential lifecycle and only a
minimal non-sensitive health-probe exception if approved. Public APIs MUST NOT expose lead
listing/read/update operations. Personal fields, raw messages,
secrets and tokens MUST NOT enter URLs, public caches, analytics or application logs.
Optional analytics MUST receive legal/consent approval, use non-sensitive fields and
remain independent of navigation, performance and submission success.

### VII. Durable Inquiries and Recoverable Notifications

General and quotation forms MUST use `POST /api/v1/inquiries`. Service CTAs MUST pass
validated, editable quotation context. Required fields MUST follow the PRD contract:
name 2–100 characters, valid E.164-normalized phone, message 10–2,000 characters, inquiry
type and privacy acknowledgement. Other contact/building fields remain optional as defined
in the contract. Malformed service/query values MUST be ignored safely.

Success MUST mean a durable inquiry write with unique reference ID and timestamp.
For staging, one PostgreSQL transaction on one connection MUST commit the inquiry and
initial pending notification outbox record atomically; failure of either write MUST
roll back both. New acceptance MUST return 201 only after commit; concurrent identical
idempotent replay MUST return 200 with the original reference/timestamp and no duplicate
or new initial attempt. Reusing a retained key for a different payload MUST return 409
without mutation. Retained identity/hash versions MUST remain usable for inquiry retention.
Current privacy-notice rollover MUST serialize with new acceptance: unchanged retained
old-notice replay remains valid after independent request controls, changed retained
content/notice conflicts, and a new stale-notice submission MUST be rejected. Lost commit
responses MUST allow safe same-identity retry with fresh anti-spam verification without
assuming that no commit occurred. Invalid/oversized/spam/rate-limited requests MUST NOT
insert leads. Quota accounting MUST survive later validation/acceptance failure. Storage
failure MUST return a safe failure (503), preserve the draft and offer retry/contact
alternatives. Separately approved production architecture MUST preserve these guarantees.

Notification MUST follow persistence. Every accepted lead MUST have a durable outbox
attempt/status and tested bounded retry/escalation or authorized operational replay.
Recovery MUST preserve attempt history, lease/fencing ownership and unique sequencing;
replay MUST NOT create another inquiry. Phase 1 staging MUST use labeled simulation and
restricted attended drain/replay until live delivery is separately approved; no automatic
worker is implied. Email failure MUST preserve the lead and successful visitor confirmation.
Operators MUST reconcile daily
and make every failed-notification inquiry visible to the designated owner within one
business day. An optional anonymous `lead_submitted` event MUST fire only after durable
acceptance. PostgreSQL records MUST remain authoritative staging lead totals; the separately
approved production inquiry store MUST remain authoritative production totals. Synthetic
counts MUST NOT be represented as live business results. This prevents a polished form
from silently losing customer requests.

### VIII. Evidence-Based Quality and Operational Readiness

Each feature MUST define acceptance evidence proportional to risk. Critical validation,
API contracts, locale/route behavior and persistence/retry flows MUST have meaningful
automated coverage, including invalid, duplicate, conflicting, storage-failure and
notification-failure requests. Both locales MUST receive manual keyboard, screen-reader,
reduced-motion, responsive and editorial review. Scores alone MUST NOT establish
accessibility compliance.

CI/release checks MUST cover formatting, lint, TypeScript, unit/integration tests,
content/route validation, accessibility smoke checks and production build. Required
performance/accessibility thresholds and asset budgets MUST be enforced automatically;
missing/invalid reports or failed thresholds MUST exit nonzero and block CI delivery,
without success masking. Preserve the authorized Lighthouse 13.5.0 security migration.
Docker/Linux reproduction, private PostgreSQL transactions/roles, trusted ingress,
staging access and secret/image boundaries MUST receive meaningful verification. Preview QA
MUST cover the latest two major Chrome, Firefox, Safari and Edge versions, current iOS
Safari and Android Chrome. Production smoke tests MUST verify real contact links, durable
test leads, notification recovery, crawlability and HTTPS. Critical release blockers MUST
close, with rollback and approved backup/restore procedures exercised before launch.

Structured logs MUST include safe correlation IDs, validation categories and notification
status. Monitoring MUST test alerts for > 1% 5xx over 15 minutes or sustained notification
failure. Named owners MUST review availability, errors, speed and lead reliability.
Missing session data MUST be reported as insufficient data. Complete unsampled API status
counts MUST support the existing alert denominator. Bounded environment/schema/database
readiness checks MUST NOT replace continuous monitoring; missing monitoring coverage
MUST trigger escalation, not a healthy claim. Runbooks MUST define restricted private
migration/retrieval/replay/cleanup, secret rotation, approved backup/restore and rollback,
escalation and tested access for at least two authorized staff. Provider features,
regions, roles or backups MUST NOT be presumed approved or operational without evidence.

## Architecture and Release Constraints

The requirements source is [PRD-001 v1.1](../../../docs/PRD.md) in the sibling `docs`
directory; product release scope remains v1.0. It remains Draft pending stakeholder
approval. The user's 2026-10-16 instruction authorizes this staging-only technical
documentation amendment following the
[impact assessment](../../specs/001-phase1-lead-foundation/architecture-change-impact.md).
It does not establish KEN stakeholder/legal sign-off, approve business claims or schedule,
or authorize provisioning, deployment, real-data processing or production launch.
Production hosting/storage MUST receive separate architecture/parity and owner/legal
approval before dependent production work; the former Cloudflare proposal and new Railway
staging selection confer no production approval. Existing feature artifacts/templates
still describe the prior platform and MUST be migrated and reanalyzed before implementation.

| Boundary | Required constraint |
|---|---|
| Content | Typed bilingual source; six page types, 12 primary localized routes and privacy utilities |
| Frontend | React/TypeScript/Vite/Tailwind; shared direction-aware components and build-time HTML |
| Runtime | Staging: Docker/Railway secure Node.js delivery of SSG and same-origin versioned `/api/v1/`; production separately approved |
| Leads | Staging: private PostgreSQL inquiries/transactional outbox, migrations, atomic acceptance and retained idempotency; processing/location clearance; production store separately approved |
| Integrations | Server-verified Turnstile; transactional email provider selected before launch |
| Environments | Separate local, protected synthetic-only preview/staging and production; isolated databases/credentials, Turnstile and recipients; no real intake without separate clearance |
| Deployment | Reviewed CI pipeline; GitHub Actions remains proposed |
| Ownership | KEN Management authorizes launch; Product Owner coordinates acceptance; QA records evidence |

The PRD targets MUST be tracked as current acceptance/operational baselines, with final
stakeholder thresholds recorded before release: Lighthouse accessibility ≥ 95 per
representative template with no critical manual keyboard failures; site/API monthly
availability ≥ 99.9%; durable acceptance ≥ 99.5% of valid non-spam submissions; unexpected
backend errors < 0.1% of API requests. Business targets (20 qualified leads/month, 3% form
conversion and 5% direct-contact intent by day 90) are proposed measurement goals, not
guarantees or current traffic claims. Usability review MUST cover at least ten representative
Arabic/English testers against the PRD completion/trust thresholds.

Approved logo/assets, bilingual copy, gallery rights/evidence, phone/WhatsApp, notification
inbox/provider credentials, domain, lead owner and legal/data-location sign-off MUST be
tracked with responsible owners. The proposed 2026-12-05 launch MUST move if gates remain
unmet. Credentials MUST NOT be written into planning documents. No production personal
data may enter unapproved infrastructure.

## Development Workflow and Quality Gates

1. **Specification:** Trace features to PRD IDs and MoSCoW release priorities; distinguish
   story sequencing from PRD P0/P1/P2/P3. Record locale parity, UX states, quality criteria,
   content/privacy dependencies and measurable acceptance scenarios.
2. **Planning:** Complete the Constitution Check before research and again after design.
   Record evidence or an owner/deadline for each applicable future gate. Define content
   models, routes/SEO outputs, component tokens, API/security boundaries, budgets and tests.
3. **Foundation:** Establish locale shell, visual direction, preview/CI and staging bindings.
   Prove a secure end-to-end inquiry persists and survives notification failure before
   decorative enhancements. Resolve data-location feasibility early.
4. **Core delivery:** Complete six pages, services, genuine gallery, both form modes,
   direct contact, bilingual states, prerendering/SEO and operational recovery. Validate
   all P0 journeys. P1 features follow only after baseline accessibility and speed pass.
5. **Release:** Obtain brand/content, lead-ownership and legal/security clearance; close
   critical defects; record bilingual browser/accessibility/performance evidence, production
   smoke results, backup/restore and rollback drills. KEN Management MUST authorize public
   launch after Product Owner/QA acceptance.
6. **Operations:** Handover runbooks and owners; reconcile notification failures daily;
   review at one week, two weeks and day 30, then assess business impact at day 90.

Every review MUST identify compliance and relevant acceptance evidence. Exceptions MUST
document the rule, rationale, alternatives, owner, expiry and approval. Unapproved
exceptions cannot pass gates. Scope/architecture amendments MUST follow Governance;
they cannot silently weaken release criteria.

## Governance

This constitution governs development decisions and template outputs. The PRD defines
product requirements; approved amendments MUST keep both consistent. Explicit user scope
and authorization govern the current task. Conflicts MUST be surfaced and resolved in
the decision record before dependent work. This amendment covers governing documentation only;
application coding, package changes and deployment require separate authorization.

Amendments MUST state rationale, impact on specs/plans/tasks and migration steps, receive
project-owner approval, update dependent guidance and prepend a Sync Impact Report.
Semantic versioning MUST use MAJOR for incompatible principle/governance removals or
redefinitions, MINOR for new principles/sections or materially expanded obligations,
and PATCH for clarifications without changed obligations. Original ratification MUST
remain fixed; Last Amended MUST reflect the amendment date.

Specifications, plans, tasks and release reviews MUST validate compliance. Plans MUST
repeat the Constitution Check after design; reviewers MUST reject unresolved violations.
`AGENTS.md` provides entry guidance; the current feature plan provides concrete technologies,
structure and commands. Initial 1.0.0 replaces an unratified template and does not claim
earlier governance history or completed stakeholder release approvals.

## Amendment History

| Version | Date | Authority and change |
|---|---|---|
| 2.0.0 | 2026-10-16 | Explicit user-authorized staging documentation amendment: replace the incompatible Pages/Functions/D1 MUSTs with Docker/Railway/Node.js/PostgreSQL; preserve product/security/quality guarantees and separate production/real-data/operations approvals. KEN stakeholder/legal sign-off remains pending; downstream migration is required. |
| 1.0.0 | 2026-10-11 | Initial documentation adoption from the unratified template; original ratification retained; no stakeholder release approval claimed. |

**Version**: 2.0.0 | **Ratified**: 2026-10-11 | **Last Amended**: 2026-10-16
