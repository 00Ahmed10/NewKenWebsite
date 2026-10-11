# Testing, Performance and CI/CD Strategy

Targets are acceptance requirements, not executed results. Trace candidate SHA, preview URL, timestamp, tool/browser versions, locale/mode, device/profile and outcome. Keep evidence private and synthetic-only. Blocked evidence is reported as blocked, never skipped-as-pass. QA/Product Owner own profile agreement before performance acceptance (DEP-12).

## Automated verification matrix

| Layer | Required cases | Traceability |
|---|---|---|
| Pure unit | NFC/code-point boundaries; Arabic/Persian phone digits, valid SA/international and invalid numbers; optional blanks/email/city; enums/no coercion; key/payload hash excludes token; query allowlist/key parity | FR-003/009/010/012/014, SC-001/005 |
| Component | Both locale/mode labels/errors, privacy unchecked, editable service, first-invalid and success focus, unknown/retry preservation, refreshed token, 409 explicit new action, 429 cooldown, menu Escape/restore and hidden tab targets | FR-004/007/008/011/018, SC-002/005 |
| Contract | OpenAPI shape/status/headers: 201/200/400/403/409/413/415/429/503/500-safe; malformed/chunked/unknown keys; no value echoes; GET/HEAD/method/child-path negative access | FR-012/015/019, SC-005/010 |
| D1 runtime integration | Fresh/upgrade migrations and constraints; both modes/locales commit inquiry+pending; simultaneous matching and changed key contenders; exact one lead/initial attempt; rollback if attempt insert fails; storage timeout/unknown response | FR-013/014/016, SC-004/006 |
| Verification/rate | Missing/expired/single-use token; hostname/action mismatch; Siteverify timeout/fail-closed; fresh-token accepted replay; window boundaries and network-key isolation; unavailable limiter; concurrent capped UPSERT | FR-012/014/021, SC-005 |
| Notification/recovery | Simulation success/failure/timeout; death after commit/before claim/after claim/before outcome; stale lease fencing; daily orphan reconciliation; retry limit/escalation; no duplicate inquiry; unauthorized operator rejection | FR-016/017/024, SC-006/010 |
| Build/content | 14 localized initial documents, six IDs, paired metadata, no missing keys/media/internal approval references, leaf/home canonical structure, no SPA catchall; production projection fails unapproved facts; CSP hashes/headers and secret bundle scan | FR-001–007/019/022, SC-001/002/010 |
| Browser/hosted | Arabic mobile entry → English → each mode → stored reference; direct refresh, client navigation data assets, true localized 404, invalid feedback, image/script/motion fallback, protected preview aliases, actual server Turnstile and restricted D1 retrieval | FR-021/023, SC-009 |

Run meaningful boundary cases, including name 1/2/100/101 and message 9/10/2000/2001, city 0/1/100/101, email blank/valid/254/255 and invalid shape, raw phone limits 2/3/64/65 plus numbering validity, floors omitted/null/0/1/200/201/noninteger/string, token 0/1/2048/2049, notice 0/1/64/65/current/stale, all enums and privacy missing/false/string/true. Total body below/at/above 32768 bytes includes multibyte Arabic and forged/missing Content-Length. ID UUID validity and rate limit requests 9/10/11 per window and 49/50/51 per day are tested; replays consume controls. Verify zero inserted leads for every rejected case.

Use separate Vitest Node/jsdom and Cloudflare runtime projects; @cloudflare/vitest-plugin fixtures load migrations and reset/isolate storage. Mock transient provider faults locally, label them, and use actual hosted D1/Turnstile for final preview evidence. A browser test process exercises real fetch behavior under wrangler pages dev; a function-in-isolation test does not prove hosting headers/routing. Static OpenAPI validation and reference checks belong to check:contracts.

## Bilingual/manual acceptance

Automate Chromium/Firefox/WebKit plus available Chrome/Edge channels; maintain actual supported-browser evidence separately. Latest two major Chrome/Firefox/Safari/Edge and current iOS Safari/Android Chrome must be recorded by version at execution. Emulated mobile and Playwright WebKit are not actual Safari/device proof. Missing access blocks the associated QA check.

Every implemented Home/Contact/privacy/preparation shell is checked at 360, 390, 768, 1024 and 1440 CSS pixels in both locales: no overflow/Arabic clipping, logical reading/focus order, numeric bidi, zoom/reflow, labels/contrast, ≥44px practical targets. Manual keyboard, NVDA with a supported desktop browser and VoiceOver Safari/iOS cover navigation/forms/confirmation, privacy link and screen-reader announcements. Native Arabic and English editors approve all public strings and metadata independently.

axe WCAG2A/WCAG2AA/WCAG21AA checks must have zero known critical/serious failures and all AA findings resolved or formally reviewed; Lighthouse accessibility ≥95 per representative template/locale does not replace manual compliance. Reduced-motion/media-failure/blocked-enhancement checks preserve content and CTA. Review runtime fallback and noscript explanation.

SC-003/008 usability: at least ten representative residential/commercial testers spanning both locales, record sample split (proposal ≥5 per locale), fixture task and completion/timing; ≥85% unassisted completion, prepared villa journey <3 minutes and mean trust/contact clarity ≥4.5/5. No private participant details in public reports. Numbers are targets, not invented outcomes.

## Proposed performance profile and budgets

Freeze exact Node/Chrome/Lighthouse/Playwright versions and applied configuration with evidence. Proposed lab profile: 390×844 viewport, DPR 1, CPU slowdown 4×, 150ms RTT, 1600Kbps download, 750Kbps upload, cold cache, no warm service worker, five separate cold runs per Home/Contact template and locale; accessibility also covers privacy. Use DevTools-applied throttling for interaction timing and clearly record Lighthouse simulated versus applied throttling when used. CI uses an agreed runner/hardware class; do not compare unlike profiles as equivalent.

Median Lighthouse mobile performance ≥90, accessibility ≥95. Record per-run and median lab LCP≤2.5s/CLS≤0.10, investigate regressions and retain reports privately. Measure two-second critical-content objective with a trace from navigation start until localized H1 and primary quotation CTA are visible/usable, not merely FCP. On the slower agreed profile, a practicability exception requires owner/approval/expiry rather than silently dropping the objective.

Instrument menu, locale switch, validation/correction and confirmation interactions in local synthetic browser runs and check lab INP≤200ms. TBT is a diagnostic proxy, not INP. Do not introduce RUM/analytics collection in this phase. Later field p75 LCP≤2.5s, INP≤200ms and CLS≤0.10 requires approved instrumentation and sufficient real samples; current field evidence is insufficient.

| Compressed/transfer budget | Home | Contact | Privacy/preparation |
|---|---|---|---|
| Initial first-party JS, gzip (shared + route) | ≤150 KiB | ≤180 KiB | ≤150 KiB |
| Route-used CSS, gzip | ≤30 KiB | ≤30 KiB | ≤30 KiB |
| Selected locale fonts, actual WOFF2 bytes | ≤120 KiB | ≤120 KiB | ≤120 KiB |
| Mobile above-fold imagery, selected derivative | ≤200 KiB | ≤80 KiB | ≤80 KiB |
| Initial first-party total transfer including HTML/data/CSS/JS/fonts/media | ≤550 KiB | ≤450 KiB | ≤450 KiB |

Fonts/images are already compressed; audit actual transferred size instead of fictitious gzip savings. Count shared chunks once per cold route. Report third-party Turnstile separately and include it in total hosted performance measurements; the first-party budget is not an exclusion from performance acceptance. Lazy-load below-fold assets and split future gallery/motion; no blocking video. Budgets are chosen planning defaults requiring QA/Product Owner agreement; increases need documented review with performance evidence, not silent drift.

## GitHub Actions and Cloudflare delivery

1. PR quality: npm ci → format/lint/types → contracts/content/routes → unit/component/runtime integration → SSG build/finalize → HTML/header/bundle/budget audit → local Pages browser/axe/performance checks. Fail any mandatory stage; upload private evidence tied to SHA. No deployed URL by itself establishes readiness.
2. Untrusted forks: read-only quality pipeline, no secrets or remote D1. Never execute their code in a privileged pull_request_target job.
3. Trusted staging job: environment-scoped limited Cloudflare token and account ID; serialized reviewed schema changes; deploy Direct Upload from repository root with explicit project/branch/commit. Prefer a stable staging candidate for shared D1 evidence; ordinary branches do not auto-migrate shared D1. Validate both preview and production configuration blocks fully instead of accidental inheritance.
4. Hosted smoke: protection on every reachable alias, HTTPS/noindex/route/CSP checks, current widget plus actual server verification, synthetic stored leads in both locales/modes, restricted reference retrieval and hosted notification failure/recovery. Access service credentials stay in the private runner, never frontend. Test-widget fixtures alone cannot substitute for real hosted configuration evidence.
5. Preview-ready: all automated candidate checks, manual/localization/browser/performance/usability evidence and Phase 1 provisional design/recovery ownership approval. DEP failures produce blocked status with owner/gate.
6. Production: protected separate project/configuration/database/widget/secrets; required reviewers, serialized migrations and explicit KEN launch authorization after all later release gates. Disabled throughout Phase 1. Build from approved origin/content and rerun metadata/contact/notification/HTTPS smoke; app rollback must preserve stored leads.

Pin all action references to reviewed full commit SHAs, dependencies to lockfile and least permissions to each job. Deployment tokens do not belong in test reports. Current supported tooling baseline and source citations are in research.md; SHA/patch resolution occurs during implementation, not as an invented planning value.

## Future operational baselines

Track ≥99.9% monthly site/API availability, ≥99.5% durable acceptance of valid non-spam attempts in a 30-day window and unexpected backend errors <0.1% of requests. Controlled fault tests are excluded from normal metrics. Phase 1 short tests cannot establish these production percentages. Later business ≥20 qualified leads/month, ≥3% form conversion and ≥5% direct-contact intent are proposed day-90 goals; missing session data remains insufficient data.
