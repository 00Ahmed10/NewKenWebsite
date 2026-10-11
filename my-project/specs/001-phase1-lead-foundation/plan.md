# Implementation Plan: KEN Elevators — Phase 1 Foundation and Critical Lead Prototype

**Branch:** 001-phase1-lead-foundation | **Date:** 2026-10-11 | **Spec:** [spec.md](spec.md)

**Input:** specs/001-phase1-lead-foundation/spec.md; ../docs/PRD.md (PRD-001 v1.0, Draft); .specify/memory/constitution.md v1.0.0.

**Status:** Planning complete; ready for task generation. Implementation, hosted verification, stakeholder acceptance and production authorization are not completed. Source PRD, constitution and clarified spec are preserved.

## Summary

Deliver a protected synthetic-only stakeholder preview: Arabic-first RTL and English LTR shared shell, initial homepage, six service choices, general/quotation Contact prototype, bilingual privacy utility and honest preparation destinations. Static build-time HTML establishes crawlability and responsive accessibility. A minimal Pages Function verifies and durably accepts a lead in D1, creates pending notification evidence atomically, and proves authorized recovery through a labeled hosted notification simulation.

Phase 1 implements foundation slices of P0-F001/F002/F005/F007 plus P0-F003/F006 context/contact safeguards and P0-F004 empty-state honesty. It does not complete the six-page marketing release. Phase 2 supplies full About/Services/Projects/Why Choose Us, genuine gallery and live contact/provider delivery. P1 analytics, FAQs, lightbox and enhanced motion are deferred. No accounts, CMS, dashboard, CRM, payment or instant quoting is added.

## Technical Context

| Item | Decision |
|---|---|
| Language/version | TypeScript 6.0.x strict; React/react-dom 19.3.0; ES2022+, bundler resolution; Node 24 LTS |
| Build/style | Vite 8.3.x, Tailwind CSS and @tailwindcss/vite 4.3.x |
| Routing/rendering | react-router and @react-router/dev 8.4.0 framework mode; explicit SSG, no runtime SSR |
| Validation/phone | Zod 4.x shared schemas; libphonenumber-js/max 1.x with SA national-input default |
| Content | Typed version-controlled bilingual modules; stable IDs, approval metadata, no initial public-content fetch |
| Runtime/storage | Cloudflare Pages + minimal Pages Functions; D1 prepared/batched writes, SQL migrations, no replication; geography/privacy provisional |
| Human verification | Turnstile server Siteverify; explicit widget lifecycle and separate environment keys |
| Notifications | Environment-controlled hosted simulation plus durable attempt history and restricted operator replay; live email provider deferred |
| Quality tooling | Vitest 4.1+, @cloudflare/vitest-plugin 1.x, Testing Library/jsdom, Playwright, axe, Lighthouse CI, Prettier/ESLint |
| Media | Build-time Sharp; approved same-origin AVIF/WebP/JPEG and local licensed WOFF2 fonts |
| Delivery | GitHub Actions, Wrangler 4.x Direct Upload; reviewed SHA-pinned actions; protected preview; production disabled |
| Scope/scale | Low-volume prototype; 12 paired primary destinations (8 preparation states), 2 privacy routes, six service IDs; no inferred traffic/capacity claims |
| Target browsers | Latest two major Chrome/Firefox/Safari/Edge; current iOS Safari/Android Chrome, actual versions recorded at QA |
| Constraints | WCAG 2.1 AA, locale parity, reduced-motion-safe enhancement, synthetic-only unapproved infrastructure, no public leads/secrets/logged personal data |
| Performance | Release p75 LCP ≤2.5s, INP ≤200ms, CLS ≤0.10; synthetic performance ≥90/accessibility ≥95; agreed two-second critical-content objective |

Supported version baselines are researched, not installed/tested. Exact patches, action SHAs, Node/npm and browser tool versions are pinned and compatibility-checked in the first implementation task. [research.md](research.md) records choices/alternatives and official sources. No technical clarification remains; external approvals are gates in [dependencies.md](dependencies.md).

## Constitution Check

**Pre-research check:** PASS for planning. The authorized scope follows prescribed technologies, Phase 1 sequencing and synthetic-only preview; no unjustified exception identified. Business/provider approvals remain future evidence gates.

**Post-design check:** PASS for planning against all eight principles. PASS denotes a compliant design, not an executed test or approval. No principle is waived; later-phase obligations have explicit owners/deadlines.

| Principle | Design evidence | Planned acceptance owner/gate |
|---|---|---|
| I — Scope/content | Spec phase boundaries; approval-aware content; suppressed unverified actions; no fabricated assets; later gallery minimum ≥3 real projects/≥6 images | Product Owner/Content/KEN: visible copy and provisional design by Phase 1 target 2026-10-23; complete genuine content Phase 2 target 2026-11-06; all P0 before launch |
| II — Architecture | Prescribed stack, source content, 14 SSG documents, versioned minimal API, D1/privacy gate | Frontend/Functions: build and actual hosted D1/Turnstile evidence before preview acceptance; complete meaningful 12 primary pages before launch |
| III — Localization | / → /ar/; paired map, correct document direction, safe-context switch, fail-build key/route audits | Content/QA: both native reviews and RTL/LTR manual matrix at Phase 1 gate |
| IV — UX/accessibility | Tokens/components, keyboard focus/states, 44px targets, five widths, static/motion/media fallbacks | Designer/QA/KEN: provisional sign-off and zero critical manual failures at Phase 1 gate; final design later |
| V — SEO/performance | SSG metadata/404, noindex preview, budgets and explicit lab profile | Frontend/SEO/QA: Phase 1 measurements; complete sitemap/domain/schema/field review before release |
| VI — Security/privacy | Independent bounds, rate/Turnstile, parameterized SQL, secret separation, no public reads; real-data gate | Functions/Legal/KEN: synthetic preview review before hosted proof; lawful basis/locations/notice clearance before real intake, PRD target 2026-11-28 |
| VII — Reliability | Atomic inquiry+pending record; 201/200/409; recorded failure/replay; daily reconciliation | Functions/Sales/Operations: designated primary/backup and hosted simulation recovery at Phase 1 gate; live notification finalized Phase 2 and tested prelaunch |
| VIII — Quality/operations | Risk-based tests, CI, isolation, safe alerts, rollout/rollback and lifecycle feasibility | Engineering/QA/Operations: preview evidence by Phase 1 target; approved backup/restore and production smoke before 2026-12-05 proposed launch |

Named individuals/access/approval evidence remain pending. Their gates cannot be marked passed based on this document. See dependencies.md for consequence and role ownership. If a vendor geography is incompatible, stop dependent real-data work and obtain an approved architecture change; do not silently substitute storage.

## Project Structure

### Documentation (this feature)

~~~text
specs/001-phase1-lead-foundation/
├── spec.md                         # Clarified source specification, unchanged
├── plan.md
├── research.md
├── data-model.md
├── quality-strategy.md
├── operations.md
├── dependencies.md
├── quickstart.md
├── contracts/
│   ├── inquiries.openapi.json      # Public submission/health contract
│   └── ui-localization.md          # Routes, query context and interaction contract
└── tasks.md                        # Future speckit-tasks output, not generated here
~~~

### Planned source structure (nothing implemented by this command)

~~~text
src/
├── root.tsx, routes.ts, entry.client.tsx
├── routes/                         # Typed Router modules delegating to page templates
├── pages/                          # Home, Contact, Privacy, Preparation, NotFound
├── components/
│   ├── layout/                     # SiteShell, Navbar, Footer, LanguageSwitcher, MobileMenu
│   ├── ui/                         # Button, Section, FormField, EmptyState, ErrorState
│   └── marketing/                  # PageHero, ServiceCard, CTASection
├── features/inquiries/             # ContactForm, widget, API client, form state
├── content/                        # ar/en dictionaries, pages, services, media, public config
├── lib/                            # Locale/route helpers, safe public utilities
└── styles/                         # Tailwind entry and token definitions
shared/                            # Pure inquiry schema, enums, normalization and safe error codes
server/
├── inquiries/                      # Handler orchestration, idempotency, repository
├── security/                       # Bounded body, rate counter, Turnstile, origin/headers
└── notifications/                  # Persisted state machine and simulation adapter
functions/api/v1/                   # Thin inquiries.ts and health.ts route exports only
migrations/                        # Numbered inquiry/notification/rate-limit SQL
public/                            # Approved media/fonts/licenses and static files only
scripts/
├── validate-content.ts, finalize-static.ts, audit-build.ts
├── optimize-media.ts
└── ops/                            # Restricted reconcile/retrieve/replay/cleanup tools
config/                            # Public deployment/render settings; no credentials
tests/
├── unit/                           # Shared normalization/schema/routing
├── component/                      # Focus, localized errors, menu/form lifecycle
├── contract/                       # OpenAPI and negative transport expectations
├── integration/                    # Cloudflare runtime/D1 races and notification interruption
└── browser/                        # Local and protected hosted critical journeys
.github/workflows/                  # Quality and separately authorized deployments
vite.config.ts, react-router.config.ts, wrangler.jsonc, package.json
~~~

**Structure decision:** One repository keeps static frontend and Pages Functions together. shared/ imports must be browser-safe; frontend may never import server/ or operational scripts. Server dependencies do not enter hydration bundles. Functions contain thin handlers, avoiding accidental public routes from helper files. Content approval/permission references live in build-only manifests when internal; publish only safe projections. No generic application framework, ORM, global state library or admin service is required.

## Frontend architecture

Router root provides localized html language/direction and shared shell; route modules select typed page content and metadata. Use framework-supported hydration with stable build-time markup. Query-based service/type preselection happens after hydration without personal values or metadata changes. Initial form defaults and noscript explanation are present in HTML. Include static reading/navigation fallback if scripts are blocked; no apparent working submit without a usable verified submission path.

Content records have stable page/service/media IDs, paired copy, preparation/approved state and reviewed metadata. Build fails on missing keys, mismatched pairs, unknown IDs, broken asset references or unapproved production projections. Initial content is imported from source, not fetched from GET APIs. Public content GET endpoints in the full PRD are deferred to the later feature that needs them; no public lead read/list/update route will exist.

Choose a nonmodal mobile disclosure menu to minimize focus complexity: announced expanded state, hidden links excluded from tab order, Escape closes and restores trigger focus. If design changes it to a modal, add tested focus containment/background inertness before acceptance. Components use semantic elements and logical CSS properties; numeric/reference/phone fragments use bidi isolation and LTR presentation. Form UI stores drafts in component memory only and uses localized inline/summary feedback. No persistent personal drafts are assumed across reload or locale changes.

### Provisional design tokens

| Token | Proposed value/use |
|---|---|
| Navy/background | #0B1526 |
| Navy/surface | #15243A |
| Metallic gold | #C7A568 for decorative trim and CTA surface; navy CTA text |
| Warm neutral | #F5F1E8; light readable text or section background |
| Ink | #172335 on warm neutral |
| Error | #B42318 on light surfaces; dedicated light-error pairing on navy, contrast tested |
| Spacing/radius | 4px base; 8/12/16/24/32/48/64px steps; 8px controls, 16px cards |
| Typography | Noto Sans Arabic Arabic body/headings; Inter English body; optional Cormorant Garamond English display, all provisional |
| Motion | 120–180ms opacity/color transitions; no parallax, autoplay/video or reveal-dependent visibility |

Exact tokens/fonts/rights require visual/native approval. Enforce 4.5:1 normal text, 3:1 large text/control contrast with automated token checks and rendered review; gold body copy is not assumed safe on light backgrounds. Use 44×44px targets where practicable, visible two-tone focus, flexible line height, no Arabic letter spacing and font-display:swap. Local licensed font subsets preserve shaping. Approved hero uses responsive picture/srcset, eager fetch priority and dimensions; below-fold images are lazy. Without supplied assets, use an honest CSS surface and localized preparation state, not a fabricated elevator/project image.

## Backend architecture and acceptance sequence

1. Create server correlation UUID; enforce method, HTTPS at hosting edge, allowed origin, application/json and bounded UTF-8 body ≤32 KiB. Do not trust declared Content-Length alone; cap stream reading.
2. Parse bounded JSON. Read rate identity only from Cloudflare-trusted network metadata; ignore caller-supplied forwarded IPs. Missing trusted identity fails safely on hosted requests; local tests supply a deliberate adapter.
3. Atomically claim both per-network rate windows, then validate the allowlisted schema/normalized fields/current privacy acknowledgement. Limits: 10 requests/10 minutes and 50/day, including parsed submissions later rejected by schema/verification and accepted replays. Rate refusal is 429 with Retry-After; storage/control outage is 503. Edge-level body/invalid-JSON flood protection supplements counters. Fixed windows allow boundary bursts and shared-IP interference; report this tradeoff and tune from safe aggregate evidence.
4. Verify Turnstile with secret, token, expected action=inquiry and configured hostname allowlist; timeout fails closed. Use one token-scoped Siteverify UUID for bounded network retry; application retries refresh tokens. Never expose or persist challenge tokens.
5. Compute environment-scoped SHA-256 key hash and keyed canonical payload hash. Unique D1 key plus batch handles simultaneous acceptance. Insert candidate inquiry on conflict do nothing; insert sequence-one pending notification only for the newly inserted candidate; select authoritative key row in the batch. Existing matching canonical payload returns 200/original reference; changed content returns 409/no insert; new candidate returns 201. SQL failure rolls back and returns 503. Concurrent winners need no in-memory lock.
6. Return only referenceId, received status and safe correlation/timestamp metadata, with no-store. After commit, best-effort waitUntil invokes the notification adapter. Visitor success is unaffected by notification result. Pending records and restricted reconciliation recover interruptions independently of the request lifetime.

[data-model.md](data-model.md) defines fields/hashes/state/migrations; [OpenAPI](contracts/inquiries.openapi.json) defines exact transport/status/error codes. No method handler exposes inquiry data. Unsupported public methods return 405 with Allow, unknown inquiry child routes return generic 404. Health exposes only ok/unavailable and correlation, no counts/configuration.

### Security and privacy boundaries

Only public Turnstile site key, locale/config and approved business facts reach frontend output. D1 binding, verification secret, hash secrets, Cloudflare deploy/access tokens and later notification credentials belong to server/provider secret stores. Preview and production have independent identifiers/secrets/bindings; real-data intake is disabled until approval. A synthetic-only marker is not a security control: protected preview restricts testers and visibly prohibits real personal data; review tester/provider network metadata processing with the privacy owner.

Use parameterized queries, no HTML interpretation of inquiry text, no values in errors/logs/URLs, no public record caches, no wildcard CORS and no analytics collection in Phase 1. Same-origin Origin validation supplements Turnstile; there is no visitor JWT/session to introduce. Generate static CSP with final-script hashes, minimal Turnstile origins and no unsafe-inline scripts, plus nosniff/referrer/frame protections. Functions set their own headers because static _headers does not cover them. Record only correlation ID, safe validation category, durations and notification category, never raw requests, IPs/digests, personal fields, token or provider body. Provider/platform logging and backup geography remain approval gates.

## Localization and SEO strategy

The manifest contains homes /ar/ and /en/, matching /about, /services, /projects, /why-ken, /contact, plus /privacy. Four deferred marketing page pairs show explicit preparation text and a contact path in preview. Every route has paired reviewed title/description, lang/dir and semantic H1. / redirects 302 to /ar/ in preview; production redirect permanence is a later domain decision, without geographic overrides.

Use Router explicit SSG and initial route discovery. Finalize leaf documents as locale/slug.html to preserve extensionless PRD URLs; leave home index and route .data outputs intact. Generate root/ar/en static 404 documents to prevent Pages SPA-200 fallback. Check direct unknown/unsupported-locale requests for true 404 and localized HTML. Client not-found UI offers the same safe home links.

Generate canonical and reciprocal hreflang from a validated build origin, excluding query context; paired preview metadata uses actual preview origin, not an invented production domain. All preview pages carry noindex, robots disallow and X-Robots-Tag; Access protects unpublished material. Generate/validate sitemap structure, but preview sitemap contains no indexable draft URLs. Production manifest later contains all 12 completed primary documents plus legal utilities and approved origin/social assets. Omit unverified Organization/LocalBusiness facts/schema. Full Search Console/production SEO remains a release gate. [Router SSG](https://reactrouter.com/how-to/pre-rendering), [Pages serving rules](https://developers.cloudflare.com/pages/configuration/serving-pages/).

## Testing and CI/CD strategy

[quality-strategy.md](quality-strategy.md) specifies exact suites, bilingual matrix, budgets/profile and acceptance evidence. Critical tests cover both modes/locales, every field boundary, rejected/spam/oversized/rate requests, simultaneous duplicate/conflict, unknown storage outcome, durable pending notification, interruption/lease expiry/replay and public confidentiality. Automation complements manual keyboard/screen-reader/native editorial review and actual supported-browser/device checks.

GitHub Actions becomes the selected planning CI/CD choice under this explicit user instruction; organization review remains DEP-05. Quality jobs have read-only repository access and no deploy secrets. Use separate staging and later production Pages projects. Trusted staging deployment follows successful checks through an environment-scoped Direct Upload job with explicit project/branch/commit and serialized reviewed migrations. Untrusted fork code cannot run with privileged secrets. Hosted smoke evidence checks D1/Turnstile/recovery and every exposed preview alias. Production jobs remain gated/disabled until all later approvals; deployment existence is insufficient for ready status.

## Local development and deployment

[quickstart.md](quickstart.md) defines proposed commands, configuration, migration/deploy order and synthetic preview exercise; [operations.md](operations.md) defines authorized retrieval/replay, safe alerts, cleanup, backup feasibility and rollback. Commands are future interfaces to implement, not existing successful runs. No application installation, migrations, deployment or personal-data processing occurs during planning.

## Phase 1 implementation sequence

| Step | Work and dependency | Exit evidence |
|---|---|---|
| 1 | Confirm owners/access, wireframes/route/content model, provisional tokens; privacy/vendor feasibility; pin supported tools and establish scripts | Approval register and exact dependency lock; unresolved access stays blocked |
| 2 | Implement typed source models, locale route manifest, SSG shell, navigation, preparation/privacy templates and CI quality baseline | Initial HTML/404 and key/route tests both locales; provisional preview |
| 3 | Establish isolated protected Pages preview, staging D1/Turnstile/secrets and reviewed migrations | No-index/access/binding evidence; no real customer intake |
| 4 | Implement schema/phone, payload cap, rate control, Turnstile and atomic idempotent inquiry/pending record | API positive/negative/boundary/race/storage tests |
| 5 | Wire general/quotation Contact, editable service context, focus/error/pending/retry/confirmation | Both locales/modes stored once; failure draft retained |
| 6 | Hosted simulation, restricted retrieval/replay/reconciliation, interruption/alert/rollback proof | Durable lead survives failure, authorized recovery creates no lead duplicate |
| 7 | Complete initial homepage/components, approved media or honest fallback, tokens and budgets; modest motion only after persistence proof | Five widths, keyboard/screen-reader/reduced-motion and performance reports |
| 8 | Hosted critical walkthrough, native reviews and ≥10 usability tests; close Phase 1 approval gates; document later blockers | Revision/URL/evidence pack; SC-001–010 review with no fabricated pass claims |

Steps 1–3 establish the usable shell before API integration; detailed decorative homepage work follows secure persistence. Research/designer reviews may proceed concurrently, but implementation must honor dependencies. Phase 1 target is 2026-10-23, conditional on dependencies; dates move when gates cannot close. speckit-tasks will expand these steps into dependency-ordered work and verification tasks.

## Complexity Tracking

No constitutional violation or approved exception. Restricted replay avoids an extra service, dashboard or scheduler. Minimal D1 rate storage is deliberate security infrastructure, not a user/account system. Future storage geography changes or added notification automation require a documented approved decision.

## Planning validation record

On 2026-10-11: all nine generated artifacts are present; OpenAPI JSON parses and all internal schema references resolve; local Markdown links resolve; no unfinished template markers or whitespace/fence errors were found. Source PRD, constitution and clarified spec SHA-256 hashes are unchanged. AGENTS.md points to this plan and retains governing-document/no-implementation guidance. The required agent-context script ran successfully. Git diff verification was unavailable because the shell process could not start; filesystem validation completed independently. No application tests, build, remote migration or deployment were run because this command creates planning documents only. These checks establish artifact integrity, not hosted acceptance.
