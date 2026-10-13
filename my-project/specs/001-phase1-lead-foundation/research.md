# Research — Phase 1 Foundation and Critical Lead Prototype

Date: 2026-10-11. Sources: PRD-001 v1.0, clarified spec, constitution 1.0.0 and primary documentation below. Three research agents investigated frontend/rendering, Cloudflare reliability/privacy, and quality/deployment as required by speckit-plan. Decisions are planning outputs; no dependencies were installed and no hosting or approval is asserted.

## R1 — Supported frontend baseline

**Decision:** React/react-dom 19.3.0, TypeScript 6.0.x, React Router and @react-router/dev 8.4.0, Vite 8.3.x, Tailwind CSS and @tailwindcss/vite 4.3.x. Use Node 24 LTS, satisfying the Router minimum of 22.22.0, and npm with a committed lockfile. These are supported version baselines; implementation must resolve actual patches, verify peer/engine requirements and security advisories, and record exact versions before generating a lockfile. Do not invent unverified patch numbers. A newer major requires a compatibility decision, not a floating latest install.

**Rationale:** Typed reusable components and current maintained tooling satisfy the prescribed stack. Router framework mode provides a Vite-based supported prerender pipeline and typed route modules.

**Alternatives considered:** A custom Vite SSR renderer adds hydration/manifest ownership; an extra third-party SSG plugin adds maintenance risk. A pure SPA cannot meet meaningful initial HTML requirements. Runtime SSR is unnecessary for static source content.

**Evidence:** [React versions](https://react.dev/versions), [TypeScript 6.0](https://devblogs.microsoft.com/typescript/announcing-typescript-6-0/), [Router changelog](https://reactrouter.com/start/start/changelog), [Vite releases](https://vite.dev/releases), [Vite setup](https://vite.dev/guide/), [Node releases](https://nodejs.org/en/about/previous-releases), [Tailwind release history](https://github.com/tailwindlabs/tailwindcss/releases). Observed Router 8.4.0 supersedes stale search results reporting 8.3.1.

## R2 — Static rendering and route delivery

**Decision:** Router framework mode, ssr:false, an explicit paired prerender list, and initial route discovery. Publish build/client only, retaining generated navigation data. Build postprocessing emits home directory indexes, extensionless leaf-page HTML, static locale 404 documents and hosting metadata. Disable generic SPA rewrites.

**Rationale:** One route model drives HTML, navigation, metadata and locale pairing. Pages nearest-directory 404 handling can preserve language while returning HTTP 404. Verify actual Pages status and canonical normalization.

**Alternatives considered:** Runtime SSR/Express; blanket 200 rewrites; a client-only not-found component. None is needed for this boundary.

**Evidence:** [Router prerendering](https://reactrouter.com/how-to/pre-rendering), [initial route discovery](https://reactrouter.com/api/framework-conventions/react-router.config.ts), [Pages document and 404 serving](https://developers.cloudflare.com/pages/configuration/serving-pages/).

## R3 — Styling, typography and public content

**Decision (design update 2026-10-13):** Tailwind Vite plugin, CSS custom-property tokens, native CSS transitions and logical properties. The user-requested [design-direction.md](design-direction.md) supersedes the earlier provisional Noto/Inter/Cormorant proposal with Alexandria Arabic headings, IBM Plex Sans Arabic body and Manrope English. Source OFL licensing is checked below; exact binaries/subsets, shaping, local delivery bytes and designer/KEN approval remain pending. No motion library or advanced 3D dependency initially. Typed bilingual source modules and approval manifests drive all public records.

**Rationale:** Local fonts reduce external requests, consistent logical layout supports RTL/LTR, and explicit approval status prevents fixture facts escaping into production. Arabic shaping must survive subsetting; do not remove glyphs merely to meet budgets.

**Alternatives considered:** Remote font CDN, a general i18n backend and animation library. These add requests or complexity without a Phase 1 need.

**Evidence:** [Tailwind Vite integration](https://tailwindcss.com/docs/installation/using-vite), [Alexandria OFL](https://github.com/google/fonts/blob/main/ofl/alexandria/OFL.txt), [IBM Plex license](https://github.com/IBM/plex/blob/master/LICENSE.txt), [IBM Plex Sans Arabic metadata](https://raw.githubusercontent.com/google/fonts/main/ofl/ibmplexsansarabic/METADATA.pb), [Manrope OFL](https://github.com/google/fonts/blob/main/ofl/manrope/OFL.txt). Source licenses/metadata reviewed 2026-10-13; preserve notices and reserved-name obligations, notably Plex. No font binary downloaded or installed. Compare needed static WOFF2 subsets against restricted variable files, preserve Arabic shaping/diacritics, and measure the existing ≤120 KiB selected-locale budget including Latin fragments. No size/accessibility pass is claimed; use reviewed system/provisional fallback if approval or budget proof is unavailable.

## R4 — Validation and phone handling

**Decision:** Shared pure schemas using Zod 4.x and libphonenumber-js/max 1.x; server remains authoritative. Normalize supported Arabic digits, parse national phone input with SA default, retain valid explicit international numbers, and store E.164 only. Code-point text lengths and canonicalization are defined in data-model.md.

**Rationale:** A handwritten phone regex validates format without numbering-plan validity. The max metadata supports meaningful validation. Schemas generate types and drive safe field-error codes without leaking values.

**Alternatives considered:** Regex-only phone checks; separate browser/server definitions; accepting unknown object properties. Rejected for validation drift or weak boundaries.

**Evidence:** [Zod](https://zod.dev/), [libphonenumber-js documentation](https://github.com/catamphetamine/libphonenumber-js).

## R5 — Transactional persistence and notification record

**Decision:** D1 prepared statements in a single batch create inquiry and sequence-one pending notification, then read the authoritative acceptance record. A unique key hash arbitrates races. After independent controls, an authoritative retained-row lookup classifies identical replay (including accepted notice A after current B) versus changed-payload 409 before new-only current-notice equality. The lookup grants no new-write permission; a current-notice miss still uses the unique atomic batch, and a stale miss resolves a concurrent winner or rejects without insertion (data-model.md). UUID v4 inputs canonicalize to lowercase before hashing. Do not enable read replication in Phase 1. Notifications run only after commit; interrupted work is discoverable in reconciliation.

**Rationale:** Batch rollback prevents a committed inquiry without its normal pending recovery record; defensive left-join reconciliation still handles legacy/anomalous missing records. No read-then-write idempotency race or overwritten payload is allowed.

**Alternatives considered:** Notification before storage, in-memory idempotency or a separate nontransactional outbox insertion. They permit loss or duplicate leads.

**Evidence:** [D1 database API and transactional batch](https://developers.cloudflare.com/d1/worker-api/d1-database/), [prepared statements](https://developers.cloudflare.com/d1/worker-api/prepared-statements/).

## R6 — Rate controls and Turnstile retries

**Decision:** Use D1 atomic capped counters with short-lived keyed network digests and two fixed windows, claimed once before body reading/JSON parsing after transport/identity guards so malformed/oversized eligible POST floods also consume quota. This is the selected pre-parse alternative to a promised unverified edge feature; optional platform abuse controls require actual capability review. Every request, including accepted replay, passes rate and server-side Turnstile validation. Each application retry obtains a fresh token without changing lead identity; a bounded Siteverify network retry uses its own token-scoped verification UUID.

**Rationale:** Tokens expire after five minutes and are single use. Pages documented bindings do not establish native rate-limiter availability; Workers limiter semantics are not a strict global quota. D1 is sufficient at prototype volume. Fail closed on unavailable controls.

**Alternatives considered:** Instance-memory counters, KV read/write counters, trusting a browser success callback or bypassing verification on replay. They violate the security/retry contract or concurrency requirements.

**Evidence:** [Pages bindings](https://developers.cloudflare.com/pages/functions/bindings/), [Workers rate-limit semantics](https://developers.cloudflare.com/workers/runtime-apis/bindings/rate-limit/), [Turnstile Siteverify](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/), [Turnstile test keys](https://developers.cloudflare.com/turnstile/troubleshooting/testing/).

## R7 — Recoverable hosted simulation

**Decision:** An environment-controlled simulation adapter records success/failure/timeout explicitly as simulated. Restricted operator tooling claims pending work, records attempts and reconciles daily; no public recovery endpoint, new scheduler Worker, admin UI or live provider is required in Phase 1.

**Rationale:** Durable work survives waitUntil interruption, and authorized operational replay supports the planned equivalent recovery path, subject to operator authorization/evidence. Pages Functions do not supply a cron trigger to assume here. Simulation changes come from restricted deployment configuration, never request bodies/query parameters.

**Alternatives considered:** Fire-and-forget email; unpersisted mock outcomes; an extra queue/Worker service; unauthenticated retry route. They either fail recovery or expand scope.

**Evidence:** [Pages Function context](https://developers.cloudflare.com/pages/functions/api-reference/). Retry/state rules are project decisions detailed in operations.md.

## R8 — Privacy, geography and lifecycle feasibility

**Decision:** Keep D1 provisional, record region/jurisdiction selection as an external legal/vendor gate, and use only explicitly synthetic fixtures in protected preview. Do not choose EU as implicit approval. Review Functions, Turnstile, logs, staff access, GitHub artifacts, backups and future email processing separately.

**Rationale:** D1 location hints are not guarantees; no Africa/Middle East option is documented. A creation-time jurisdiction restriction does not confine the entire globally executed application. Saudi-only residency could block the required D1 architecture and would need an approved change before real intake.

**Alternatives considered:** Inferring compliance from encryption or a location hint; silently substituting another database. Both rejected.

**Evidence:** [D1 locations/jurisdictions](https://developers.cloudflare.com/d1/configuration/data-location/), [D1 security](https://developers.cloudflare.com/d1/reference/data-security/). This plan makes no legal-compliance determination.

**Lifecycle decision:** Numbered reviewed forward migrations, explicit local/remote targets, backup bookmark before approved remote changes, compatible app rollback. D1 Time Travel is recovery capability, not the proposed independent encrypted export policy: seven days on free/thirty on paid, restore overwrites the database. SQL exports require separately approved encryption/storage/deletion controls. Lead 12-month and backup 30-day periods remain proposals.

**Evidence:** [Migrations](https://developers.cloudflare.com/d1/reference/migrations/), [Time Travel](https://developers.cloudflare.com/d1/reference/time-travel/), [Export](https://developers.cloudflare.com/d1/reference/export/).

## R9 — Quality and delivery tooling

**Decision:** Vitest 4.1+ with @cloudflare/vitest-plugin 1.x for the Cloudflare runtime; separate Node/jsdom/component projects; Testing Library, Playwright, @axe-core/playwright, Lighthouse CI, Prettier and ESLint. Wrangler 4.x provides local Pages and explicit deploys. Resolve and pin compatible exact versions during implementation. GitHub Actions builds/tests then uploads a Direct Upload Pages project, with full-SHA-pinned Actions and environment-scoped secrets.

**Rationale:** Runtime D1 tests complement browser transport tests. Playwright WebKit/emulation is not actual Safari/device acceptance; manual evidence remains necessary. Privileged workflows never execute untrusted fork code.

**Alternatives considered:** Node-only API tests, native automatic Pages deploy before checks, dashboard uploads that omit Function compilation, or production credentials on PR jobs.

**Evidence:** [Cloudflare Vitest minimum](https://developers.cloudflare.com/workers/testing/vitest-integration/write-your-first-test/), [plugin migration](https://developers.cloudflare.com/workers/testing/vitest-integration/migration-guides/migrate-to-vitest-plugin/), [Pages test recipes](https://developers.cloudflare.com/workers/testing/vitest-integration/recipes/), [Playwright browsers](https://playwright.dev/docs/browsers), [accessibility](https://playwright.dev/docs/accessibility-testing), [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/configuration.md), [Wrangler releases](https://github.com/cloudflare/workers-sdk/releases), [Cloudflare CI upload](https://developers.cloudflare.com/pages/how-to/use-direct-upload-with-continuous-integration/), [GitHub Actions security](https://docs.github.com/en/actions/reference/security/secure-use).

## R10 — Headers, preview privacy and measurements

**Decision:** Protected stakeholder preview, noindex headers/meta and disallow robots; test every hash/base/branch/custom alias. Generate CSP hashes for static hydration scripts, allow necessary Turnstile origins, and apply equivalent safe API headers in Functions. Proposed mobile profile/budgets are in quality-strategy.md and require QA/Product Owner agreement.

**Rationale:** Built-in Pages preview Access protects hash deployment URLs, not every base/custom hostname. Static _headers do not cover Function responses. Navigation Lighthouse cannot prove INP or field p75; interaction runs and later sufficient approved field data are separate evidence.

**Alternatives considered:** Robots as access control, unsafe-inline CSP, public QA report uploads or calling TBT INP. Rejected.

**Evidence:** [Preview deployments](https://developers.cloudflare.com/pages/configuration/preview-deployments/), [Pages headers](https://developers.cloudflare.com/pages/configuration/headers/), [Router CSP](https://reactrouter.com/how-to/security), [Turnstile CSP](https://developers.cloudflare.com/turnstile/reference/content-security-policy/), [INP](https://web.dev/articles/inp), [lab/field differences](https://web.dev/articles/lab-and-field-data-differences).

## Resolution and external dependencies

No technical NEEDS CLARIFICATION remains. Exact dependency patches are an implementation lockfile action within the chosen supported baselines, not a product ambiguity. Provisioning, privacy decisions, business assets, named staff and approval evidence cannot be resolved by research; dependencies.md records them as external gates. Planning PASS never means preview acceptance, privacy clearance or production approval. No approved exception is assumed.

## R11 — Premium design and later cinematic feasibility (2026-10-13)

**Decision:** [design-direction.md](design-direction.md) defines the requested palette/type proposal and concise five-section Home with six stable service choices and an inline project/preparation status. Phase 1 uses a static architectural still when licensed media is supplied, otherwise an honest navy CSS surface, plus the existing short color/opacity feedback. No package installation, WebGL, video, door-opening motion or parallax is introduced.

**Rationale:** This preserves FR-005, SSG, accessible content/CTA availability, secure-lead-first sequencing and the existing performance ceilings. Two Arabic families may challenge the ≤120 KiB font budget; this is a measured T084/DEP-02/12 gate, not an assumed fit. Local font-display swap/selective preload and actual metric-matched fallback require browser traces. [Font guidance](https://web.dev/articles/font-best-practices).

**Later alternatives:** CSS 3D can create shallow door planes/perspective with native transforms but cannot promise physical reflections. Some grouping properties flatten preserve-3d trees; separate clip/opacity wrappers and test browser composition. [CSSWG transforms](https://www.w3.org/TR/css-transforms-2/). An opt-in pre-rendered silent clip can preserve realistic light/materials with decode/transfer costs; keep SSG poster, explicit Play/Stop, playback-error fallback and mobile still. [Media playback guidance](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Autoplay). Conditional client-only React Three Fiber can support actual geometry/material/camera response, with runtime/GPU/context-loss costs; demand rendering, one scene, bounded DPR/resources and Canvas fallback/error boundary are candidate measures. [R3F performance](https://r3f.docs.pmnd.rs/advanced/scaling-performance), [Canvas fallback](https://r3f.docs.pmnd.rs/api/canvas).

**Recommendation:** Separately approved Phase 3/P1-F003 study compares CSS depth and rendered media first; R3F requires an approved interactive need, compatibility/asset proof, schedule impact and unchanged baseline performance/accessibility. All cost/fps caps in design-direction.md are unmeasured proof proposals, not Phase 1 allowances or approved later implementation tasks. No new mandatory task/package, architecture exception or approval is inferred. Exact font/media files and supported versions must be checked during later authorized work.
