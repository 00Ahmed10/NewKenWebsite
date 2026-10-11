# Local Development and Preview Deployment Quickstart

These are proposed interfaces for future implementation tasks. The repository currently contains Spec Kit documentation; no application package/scripts/configuration are created by this planning command. Commands below become valid after speckit-implement builds the planned scaffold. Do not run remote provisioning/deploy steps until account targets, access and synthetic-testing policy are confirmed.

## Prerequisites and commands

Use Node 24 LTS and npm, pinned to an exact supported patch/version in implementation; Git, approved Cloudflare organization access and GitHub repository permissions. Local code uses React 19.3/Router 8.4/Vite 8.3/Tailwind 4.3/TypeScript 6 baselines, with a reviewed committed dependency lock. On the initial scaffold, install the pinned set; subsequent checkouts use npm ci. Provision only the approved protected staging target for Phase 1; production remains disabled.

From project root in PowerShell:

~~~powershell
npm ci
npm run dev
npm run format:check
npm run lint
npm run typecheck
npm run check:contracts
npm run check:content
npm run check:routes
npm run test:unit
npm run test:integration
npm run build
npm run check:build
npm run test:browser
npm run check:performance
~~~

Planned script behavior: dev runs Router/Vite frontend hot reload; build invokes Router SSG, static finalization, media/metadata generation and audit; output build/client. test:integration uses isolated Cloudflare runtime/D1 fixtures. Browser checks start or target wrangler pages dev, not a frontend-only preview. Performance script uses the recorded agreed profile. check:build enforces CSP/budgets/projections/no-secret outputs. No nominal script pass can replace hosted evidence.

For a full local Pages/API session after the initial build:

~~~powershell
npx wrangler d1 migrations apply ken-preview --local --persist-to .wrangler/state
npx wrangler pages dev build/client --persist-to .wrangler/state
~~~

ken-preview is a proposed configuration database name, not an existing resource; resolve to the actual reviewed name/ID in wrangler.jsonc. The same local persistence directory is essential. D1 local migration must never silently choose --remote. Hot-reload-only frontend dev cannot prove Pages API/storage; rebuilding updates static HTML for local full-runtime QA.

## Configuration contract

| Public/build variable | Purpose |
|---|---|
| BUILD_ORIGIN | Validated actual preview origin for canonical/hreflang/hosting generation; approved domain only for later production |
| BUILD_ENVIRONMENT | local/preview/production; production build rejects unapproved content/projections |
| VITE_TURNSTILE_SITE_KEY | Public environment-specific widget key only; no server secret |
| PUBLIC_PRIVACY_NOTICE_VERSION | Displayed version matching selected environment notice; not approval evidence |

| Server binding/secret | Purpose |
|---|---|
| DB | Explicit local/preview/production D1 binding; no read replication initially |
| APP_ENVIRONMENT / ENVIRONMENT_ID | Enforces target identity and synthetic-only preview behavior |
| CURRENT_PRIVACY_NOTICE_VERSION | Current accepted notice, independent server validation |
| TURNSTILE_SECRET_KEY | Siteverify secret; server only |
| TURNSTILE_ALLOWED_HOSTNAMES / ALLOWED_ORIGINS | Exact reviewed hosting allowlists |
| PAYLOAD_HASH_KEYS / PAYLOAD_HASH_VERSION | Versioned payload HMAC key material; preserve old versions while retained identities need them |
| RATE_LIMIT_SECRET | Per-environment keyed network digest secret |
| RATE_LIMIT_10_MIN / RATE_LIMIT_DAY | Defaults 10 and 50, validated positive integers |
| NOTIFICATION_MODE / SIMULATION_OUTCOME | simulation and controlled success/failure/timeout; no request-controlled fault injection |
| REAL_DATA_INTAKE_ENABLED | false Phase 1; cannot enable without recorded approvals |

Store development secrets only in ignored .dev.vars/.env.local with appropriate file access; examples contain names only. CI uses environment secret stores; hosted Functions use provider secrets. Never put server secrets under VITE_ or source public content. Ensure ignored private configuration, SQL exports and local D1 state cannot enter Git or build/client. Test secret scanning using harmless canary strings, never printing real credentials.

Local Turnstile uses official test credentials obtained from documentation. Hosted acceptance uses actual staging widget/secret with hostname/action checking; automated deterministic test-key tests are separately labeled. Application retry refreshes tokens while retaining the same inquiry UUID key. Notification simulation labels do not replace actual hosted D1 or server verification proof.

## Protected preview preparation and deploy sequence

1. Assign primary/backup operators, QA/editorial/design owners and access policies; record DEP-04/05/07/10/12 evidence. Privacy reviewer assesses processor/network metadata while leads remain synthetic. No real customer intake.
2. Create a staging Direct Upload Pages project (proposed ken-elevators-staging) and isolated D1/widget. Choose D1 location/jurisdiction only according to reviewed synthetic setup and approved real-data plan, not an assumed Saudi hint. Separate later production project is not a Phase 1 deployment.
3. Configure top-level/local defaults and explicit Pages env.preview/env.production blocks for this staging project, both using staging-only bindings if base deployment is used. Provision secrets before consumers. Validate actual hostname widget allowlists; protect/deny every base/hash/branch/custom hostname and test Access rejection. Built-in preview Access alone is insufficient for base/custom aliases.
4. Run all quality checks and review forward migrations. Execute remote staging migration in a serialized authorized job with explicit actual database name/ID. No arbitrary PR mutates shared staging schema.
5. Deploy from repository root so functions/ compiles alongside build/client; attach explicit branch/SHA and record returned URL. No dashboard drag-and-drop shortcut.
6. Run hosted HTML/route/header/verification/persistence/recovery checks and manual approval evidence; record candidate ready only when all applicable gates pass. A missing dependency remains blocked.

Proposed CLI forms after approved provisioning (names resolved in real configuration; tokens never embedded):

~~~powershell
npx wrangler d1 migrations list ken-preview --remote
npx wrangler d1 migrations apply ken-preview --remote
npx wrangler pages deploy build/client --project-name ken-elevators-staging --branch 001-phase1-lead-foundation --commit-hash <candidate-sha>
~~~

Replace the SHA placeholder with the verified candidate revision; the displayed command is illustrative, not ready to paste unchanged. CI supplies explicit account/project/database identity via reviewed environment settings and least-permission credentials. Pre-migration bookmark/backup feasibility and incompatible rollback review precede remote changes. No production migration/deployment command is authorized by this plan.

## Repeatable hosted synthetic walkthrough

Open approved protected preview at / → /ar/. At 390px inspect navigation, switch to English preserving page/context, directly refresh Contact/privacy and inspect initial HTML/metadata. Open quotation with type=quotation&service=villa, edit/clear service and optional fields, then submit clearly synthetic data plus actual human verification and fixture privacy acknowledgement. Match returned reference to exactly one D1 record through an authorized fresh operational session; keep personal values out of report output.

Exercise general/quotation in both locales, rejection/no insert, same-identity fresh-token retry (200), changed content (409), storage unavailability, notification failure and interrupted work. Switch simulator outcome using restricted settings and replay existing pending/failed reference. Demonstrate authorized primary/backup retrieval, daily visibility, alerts and rollback retaining leads. Unknown ar/en/unsupported-locale routes return actual 404 with appropriate HTML. Confirm no indexing, no accessible unprotected alias, no public record access, no leaked secrets/data and no production records.

Planned operator interfaces (implemented later): reconcile --environment preview, retrieve --reference <uuid> --private-output <approved-local-path>, replay --reference <uuid> --environment preview and cleanup --environment preview --synthetic-only. CLI defaults show safe counts/status/reference only, validate account/target and refuse production. Never put actual personal fields or secrets in arguments/logs. See operations.md for lease/retry/escalation and data lifecycle.

## Troubleshooting and release boundary

503 means configuration/control/storage/verification service may be unavailable; check safe correlation category through restricted logs, not raw payloads. Retain draft/identity and refresh verification before retry. 429 observes Retry-After; 409 requires deliberate fresh submission for changed content. Unapproved contacts remain suppressed, missing imagery has an honest fallback, and missing locale content fails validation.

If direct routes return 200 SPA not-found pages, inspect top-level/locale 404 output and remove generic SPA rewrite. If client navigation requests missing manifests/data, verify initial route discovery and preserved generated route assets after leaf flattening. If CSP blocks hydration/widget, correct final-document hashes/necessary origins rather than broadly enabling unsafe-inline.

Phase 1 ends with verified stakeholder preview and dependencies, not public launch. Later complete marketing pages/assets/contacts/live email, legal geography/lifecycle, production domain/SEO, backup/restore/monitoring and KEN launch authorization must close before enabling real intake/deploying production.
