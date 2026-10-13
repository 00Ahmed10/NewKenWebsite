# KEN Elevators Phase 1 — Specification Analysis Report

**Feature:** 001-phase1-lead-foundation
**Analysis date:** 2026-10-11
**Status:** Completed analysis, saved at the user's explicit request.
**Implementation readiness:** Resolve the CRITICAL finding before starting `speckit-implement`.
**Final severity inventory:** 1 CRITICAL, 0 HIGH, 6 MEDIUM, 1 LOW.

> **Documentation remediation — 2026-10-11:** The analysis below is the preserved historical snapshot. Its eight findings have been addressed in the planning artifacts; see the remediation record at the end. This is not a new speckit-analyze result or implementation pass. A fresh analysis remains required.

## Provenance and scope

This report preserves the most recent completed `speckit-analyze` analysis from this session, including the subsequent verification and the requirement-by-requirement coverage review. It is not an invented run or a claim that implementation tests passed. Relevant task and artifact references were checked again while preparing this saved report.

The earlier assessment was corrected after verification: scaffold ownership and early widget-test sequencing are not proven hard dependency cycles; the health response schema concern is LOW because its response descriptions distinguish the intended states. The final inventory below supersedes the earlier severity assessment.

The analysis reviewed:

- `../docs/PRD.md`
- `.specify/memory/constitution.md`
- `.agents/skills/speckit-analyze/SKILL.md`
- `specs/001-phase1-lead-foundation/spec.md`
- `plan.md`, `tasks.md`, `research.md`, `data-model.md`
- `quality-strategy.md`, `operations.md`, `dependencies.md`, `quickstart.md`
- `contracts/ui-localization.md`, `contracts/inquiries.openapi.json`
- `checklists/requirements.md`

Unless explicitly rooted elsewhere, artifact paths in this report are relative to `specs/001-phase1-lead-foundation/`. Application, configuration, test and workflow paths are relative to the project directory, `my-project/`. Line references identify the reviewed snapshot and may move after future edits.

The analysis and verification did not change source artifacts. This save operation creates only `analysis-report.md`; it does not authorize remediation, application implementation, deployment, real-data intake or external messages.

## Findings grouped by severity

### CRITICAL

#### C1 — Notice-version rollover conflicts with durable idempotent replay

**Category:** Constitution alignment / cross-artifact conflict
**Requirements:** FR-014, FR-015, FR-018, QC-005; constitution VII
**Affected tasks:** T033, T036, T038, T039, T043, T044, T047, T050, T053, T057

**Evidence locations:**

- `spec.md:145–149`: identical replay must return the original reference; privacy acknowledgement must be validated.
- `plan.md:144–147`: current-notice validation precedes atomic acceptance/replay resolution.
- `data-model.md:32`: submitted notice version must exactly match the environment's current notice.
- `data-model.md:45–49`: notice version is material payload content; replay identity lasts as long as the retained inquiry.
- `data-model.md:117`: matching existing payload returns 200 and the original reference/time.
- `contracts/inquiries.openapi.json:74` and `:455–460`: invalid current notice is a request error; notice must match the current server version.
- `contracts/ui-localization.md:27`: changed notice requires renewed acknowledgement.
- `tasks.md:80,85–86,90–91,94,107`: hashing, current-notice validation, repository replay and hosted retry tasks.
- `.specify/memory/constitution.md:163–166`: identical replay MUST return 200 with the original reference and no duplicate.

**Problem:** A request is accepted under notice A, its response is lost, and the environment changes to notice B before the visitor retries. An unchanged retry under A can fail current-notice validation before reaching the stored replay decision. Updating the draft to B changes the canonical payload and can produce 409 instead of an identical replay. Starting a fresh identity to recover the unknown outcome can create a second inquiry.

**Impact:** The planned flow cannot consistently satisfy the retained-identity replay guarantee across notice updates. This conflicts with the governing constitution's replay requirement and is an implementation blocker.

**Recommended fix:** Define existing accepted-request replay separately from new acceptance. A retained identical replay should resolve against its original accepted payload/notice without inserting or modifying a lead, while still enforcing transport, verification, rate and confidentiality controls. New inquiries must require the current notice. Changed content must remain a conflict. Document the distinction consistently in the plan, model, API/UI contracts and task acceptance criteria.

**Required validation:** Add explicit lost-response and concurrent retry cases spanning A → B notice rollover. Prove 200/original reference/original acceptance time, exactly one inquiry and one initial notification record; verify changed payload remains 409, and a genuinely new request under an obsolete notice is rejected. Do not weaken constitution VII.

### HIGH

No HIGH findings remain in the final verified assessment.

### MEDIUM

#### I1 — Scaffold file ownership and the minimal-build checkpoint are underspecified

**Category:** Task/path ownership
**Requirements:** FR-001, FR-022, QC-006
**Affected tasks:** T003, T008, T018, T019, T026
**Affected files:** `tasks.md:24,29,48–49,56`; `plan.md` project structure; intended `src/root.tsx`, `src/routes.ts`, `src/entry.client.tsx`, route/page modules and scaffold configuration.

**Problem:** T003 requires a working minimal Router scaffold/build, while T018 later owns the root, entry and route/page modules needed by that scaffold. The tasks do not clearly assign the minimal earlier versions or describe how T018 evolves them.

**Impact:** An implementer may create temporary files without an owner or interpret T003 as blocked by a later task. This is an ownership gap, not a proven hard dependency cycle.

**Recommended fix:** Explicitly assign a minimal buildable root/entry/route template to T003, with T018 enhancing the same files, or adjust the checkpoint ownership/order. Keep one authoritative owner for each shared file.

**Required validation:** T003 must build from a fresh checkout without future story modules. T018 must preserve and extend that scaffold without duplicating routing or entry files.

#### I2 — Early widget/CSP test scope is ambiguous

**Category:** Checkpoint sequencing
**Requirements:** FR-012, FR-021, FR-023, QC-006
**Affected tasks:** T020, T021, T025, T026, T037, T046, T053, T055
**Affected files:** `tasks.md:50–56,81,93,103–105`; `quality-strategy.md`; intended `tests/browser/static-routes.spec.ts`, `tests/component/turnstile-widget.test.tsx`, `src/features/inquiries/TurnstileWidget.tsx`, `.github/workflows/quality.yml`.

**Problem:** T021's early static/runtime delivery checks include CSP/widget compatibility before the actual widget is implemented in T046. Foundation CI/checkpoints depend on these earlier checks, while later tasks explicitly cover widget lifecycle and actual hosted verification.

**Impact:** The earlier checkpoint could be interpreted as requiring unfinished story functionality, or a fixture test could be mistaken for hosted proof. Later coverage exists; no explicit dependency cycle was established.

**Recommended fix:** Define T021 as a foundation-level CSP/script fixture check, and explicitly place real widget lifecycle and actual hosted CSP/Turnstile proof in T037/T046/T053/T055. Ensure early CI only runs checks executable for the current checkpoint, without granting false passes to future mandatory checks.

**Required validation:** Foundation checks pass on implemented foundation surfaces; later story checks remain pending until implemented. Hosted acceptance requires actual verification and cannot be replaced by a fixture or local mock.

#### U1 — Alert data source and evaluation cadence are underspecified

**Category:** Operational underspecification
**Requirements:** FR-024, QC-007
**Affected tasks:** T022, T063, T067, T071, T074, T075, T077
**Affected files:** `operations.md:21–29`; `dependencies.md` DEP-07/12; `tasks.md:52,122,129,133,139–142`; intended safe logging, alert rules and restricted operations tools.

**Problem:** The plan defines >1% API 5xx in a rolling 15-minute window, notification-age/failure triggers and escalation. It assigns alert logic/configuration/demonstration tasks, but does not concretely specify the source for request totals/errors, metric retention, evaluation frequency or mechanism that detects the 15-minute notification-age trigger. Daily manual reconciliation alone does not explain those shorter-window checks.

**Impact:** Operators cannot yet reproduce the monitoring behavior or demonstrate timely alerts from hosted data. Monitoring is mapped to tasks; it is not wholly absent.

**Recommended fix:** Select and document the actual restricted provider/manual operational mechanism, its safe inputs, rolling-window calculation, retention, evaluation cadence, owner, incident deduplication and escalation. Verify actual account-tier capabilities. Do not assume a Pages scheduled trigger, add an unapproved scheduler, or change the required threshold by inventing a minimum denominator.

**Required validation:** Hosted controlled faults must reach the approved mechanism with correct numerator/denominator, timing, reset/repeat behavior and restricted routing. Demonstrate missed-review handling and exclude deliberate test windows from normal metrics.

#### G1 — Promised malformed-JSON flood protection lacks an explicit implementation/configuration task

**Category:** Detailed coverage gap
**Requirements:** FR-012, QC-004
**Affected tasks:** T034, T040, T041, T044, T053, T058, T111
**Affected files:** `plan.md:142–144`; `tasks.md:78,87–91`; intended `server/security/body.ts`, `server/security/rate-limit.ts`, API boundary and hosted edge configuration.

**Problem:** The plan promises edge-level body/invalid-JSON flood protection in addition to application counters. The application counters consume parsed submissions; malformed requests can fail earlier. T034 names a malformed-JSON/flood boundary, but no task explicitly owns the promised edge configuration or another pre-parse control.

**Impact:** A plan-level protection can remain unimplemented even though FR-012 has broad validation/rate-limit task coverage.

**Recommended fix:** Assign the supplemental edge/pre-parse protection to a concrete task with provider capability, policy, target and owner, or document an approved alternative and its tradeoffs. Preserve bounded body reading and independent server validation.

**Required validation:** Exercise repeated malformed/oversized requests on the protected hosted target, prove the supplemental control applies, and verify zero lead insertion and safe rejection responses.

#### U2 — Submission UUID case normalization is unspecified

**Category:** Identity normalization ambiguity
**Requirements:** FR-014, QC-005
**Affected tasks:** T033, T036, T038, T039, T043
**Affected files:** `data-model.md:25,47`; `contracts/inquiries.openapi.json:350–352`; `quality-strategy.md`; intended schema/normalization and `server/inquiries/idempotency.ts`.

**Problem:** The model requires a UUID v4 submission identity and hashes its textual representation, but does not state whether accepted uppercase/lowercase forms are canonicalized before hashing. The OpenAPI UUID format does not define that application decision.

**Impact:** Equivalent textual UUID forms may yield different key hashes, or client/server validators may disagree.

**Recommended fix:** Choose one canonical representation, preferably validated lowercase UUID v4, before environment-scoped hashing. Apply the same rule to accepted client/server inputs and describe it in the model/contract.

**Required validation:** Case variants either resolve to the same reference without another inquiry or are consistently rejected according to an explicit contract. Include invalid UUID/version/type cases.

#### U3 — Disabled submit and first-invalid-field focus need one explicit interaction path

**Category:** Accessible interaction ambiguity
**Requirements:** FR-011, QC-002
**Affected tasks:** T037, T048, T050, T059
**Affected files:** `spec.md:61,142`; `contracts/ui-localization.md:25`; `tasks.md:81,95,97,109`; intended `ContactForm.tsx`, `useInquiryForm.ts` and form tests.

**Problem:** The UI contract enables submit only after required inputs are valid, while requiring an attempted invalid submit to focus the first invalid field. It correctly says guidance must not depend on a disabled button event, but leaves the concrete keyboard/pointer/Enter path and first-attempt behavior unresolved.

**Impact:** Errors may be available on blur while the mandated invalid-attempt focus behavior is still unreachable.

**Recommended fix:** Define exactly how users initiate validation and receive first-invalid focus. Resolve the submit-enablement rule and invalid-attempt behavior consistently; distinguish missing token/pending restraint from invalid form input.

**Required validation:** Demonstrate empty/partially completed forms, keyboard Enter and pointer activation in both modes/locales, including announced errors and first-invalid focus without relying on activation of a disabled native button.

### LOW

#### I3 — Shared health schema permits status/HTTP combinations broader than intended

**Category:** Contract precision
**Requirements:** FR-015, FR-019, FR-021
**Affected tasks:** T035, T044, T060
**Affected files:** `contracts/inquiries.openapi.json:275–323,829–849`; intended `server/health.ts` and `tests/contract/health.test.ts`.

**Problem:** Both HTTP 200 and HTTP 503 use a shared Health schema whose status enum permits both `ok` and `unavailable`. Response descriptions distinguish the intended states, so the semantic intent is present.

**Impact:** Schema-only validation may accept 200/unavailable or 503/ok.

**Recommended fix:** Constrain each response's status with a response-specific schema/const, or add explicit response/status assertions.

**Required validation:** 200 has status=ok; 503 has status=unavailable. Both remain minimal, correlated, no-store and free of configuration, lead counts or binding details.

## Dependency and path assessment

### Explicit dependency validation

The completed review found no missing referenced task IDs and no cycles in the explicit task-ID dependency graph. Phase prerequisites and external DEP gates remain additional constraints; the absence of a graph cycle does not resolve the ownership/checkpoint ambiguities in I1/I2.

The principal execution sequence is:

Setup → local localized/static/D1 foundation → secure local inquiry → actual protected hosted inquiry proof → authorized hosted recovery → initial Home acceptance → complete browser/performance/usability preview proof → final Phase 1 acceptance.

Specific qualifications:

- T003 versus T018: assign ownership of the minimal files required by the earlier build; see I1.
- T021/T025/T026 versus T046/T055: distinguish early fixtures from implemented/hosted widget checks; see I2.
- T056 needs authorized retrieval access under DEP-07 before T074 later formalizes/proves both primary and backup roles. This is a real access prerequisite, not a proven cycle. Do not defer all retrieval authorization to T074.
- T074 depends on US1 acceptance, and US2 cannot be accepted without US1.
- T079–T092 wait for hosted recovery acceptance T078 before Home enhancement.
- Parallel markers apply only after listed dependencies and phase gates are complete. Shared-file edits must be serialized.
- A task checkbox requires its output and verification; missing credentials, reviewers, equipment or approvals cannot be replaced by invented evidence.

### Paths and project boundaries

No confirmed broken implementation path was established by the completed run. The application/configuration/test paths are intended future outputs, not proof those files already exist.

- The working project is `my-project/`; the governing PRD is `../docs/PRD.md` from that directory.
- Feature documents live in `specs/001-phase1-lead-foundation/`; constitution lives in `.specify/memory/constitution.md`.
- Command/path instructions should state their working directory explicitly. A Git repository root in a parent directory is not interchangeable with the application working directory.
- I1 concerns ownership of `src/root.tsx`, `src/routes.ts`, `src/entry.client.tsx` and minimal route/page modules.
- The selected output is `build/client/`, not an assumed `dist/` directory or generic SPA catchall. Final static routes, headers, redirects, robots and API-only route manifest are assigned to T019/T044.
- Shared implementation helpers belong in `server/` or other planned directories; only thin handlers/middleware belong in `functions/`.
- Operational exports and sensitive evidence must remain outside Git and public build output. Evidence filenames describe safe reports, not permission to store raw leads or secrets.

### External dependency gates

| DEP | Unresolved gate | Affected task anchors / consequence |
|---|---|---|
| DEP-01 | PRD/scope/metrics sign-off | T108/T117; no stakeholder acceptance can be inferred |
| DEP-02 | Provisional route/content/design approval and asset/font rights | T084/T090/T092/T117; local provisional work does not establish visual approval |
| DEP-03 | Native bilingual visible copy and privacy review | T059/T091/T092/T117; fixture notice is synthetic only |
| DEP-04 | Actual Cloudflare projects, D1/Turnstile bindings and Access | T028–T032/T053–T060/T076/T096–T100/T106; hosted proof blocked without access |
| DEP-05 | Repository/GitHub/CI permissions and reviewed deployment policy | T029–T031/T054/T094/T096/T106; local workflow drafting does not authorize trusted deployment |
| DEP-06 | Live email provider/sender/recipient/credentials | Later release gate; labeled Phase 1 notification simulation may proceed |
| DEP-07 | Authorized primary/backup operators, MFA and escalation | T056/T074–T078/T098/T106/T114/T117; actual access/recovery cannot be asserted |
| DEP-08 | Verified direct-contact facts | T086/T112; suppress unavailable links; enabled actions need real device evidence |
| DEP-09 | Media/project rights and genuine assets | T083/T085/T091; honest fallbacks permitted, full gallery remains later |
| DEP-10 | Processing/location/privacy approval | T027–T030/T053/T074/T096/T107; synthetic setup assessed separately, real intake disabled |
| DEP-11 | Lifecycle/export/backup/restore policy | T027/T028/T031/T070/T107/T114; proposed durations are not approved defaults |
| DEP-12 | Actual devices/testers/profile/monitoring resources | T058/T059/T075/T077/T089/T100–T105/T117; missing evidence blocks its acceptance gate |
| DEP-13 | Production domain, complete P0 and launch approval | T108/T112/T116 track later obligations; no production authorization |

Missing live email or a production domain does not itself block permitted Phase 1 simulation. Missing hosted D1/Turnstile, approved protected synthetic setup, authorized operators, required reviewers or actual QA resources blocks the corresponding Phase 1 acceptance.

## Coverage results

All 25 functional requirements and all 7 quality criteria have implementation and verification anchors. None is wholly unmapped. This is planned coverage, not complete scenario coverage or passed acceptance. C1/G1/U1/U2/U3 identify gaps within mapped requirements.

### Functional requirements

| Requirement | Implementation anchors | Verification anchors |
|---|---|---|
| FR-001 Locale entry/routes | T012/T018/T019 | T013/T021/T080/T097 |
| FR-002 Shared navigation/switching | T009/T012/T017 | T013/T080/T092 |
| FR-003 Complete bilingual states | T011/T014/T018/T082 | T013/T014/T091 |
| FR-004 Accessible mobile navigation | T017 | T021/T080/T089 |
| FR-005 Honest initial Home | T081/T082/T085 | T079/T088/T091/T092 |
| FR-006 Design foundation/patterns | T015/T016/T081/T084 | T079/T089/T090 |
| FR-007 Responsive/resilient/bidi | T015/T017/T083/T087 | T080/T088/T089/T100 |
| FR-008 Account-free modes | T038/T048/T049 | T033/T037/T050/T056 |
| FR-009 Exact field contract | T010/T038/T048 | T033/T045/T052 |
| FR-010 Safe editable service context | T012/T049/T081 | T013/T037/T080 |
| FR-011 Accessible lifecycle | T046/T047/T048 | T037/T050/T057–T059 |
| FR-012 Independent secure controls | T038/T040–T044 | T033–T035/T045/T055/T058 |
| FR-013 Durable acceptance | T023/T043/T044 | T036/T045/T056 |
| FR-014 Idempotent retry | T039/T043/T047 | T036/T050/T057 |
| FR-015 Safe submission responses | T022/T044/T047 | T035/T060 |
| FR-016 Recorded notifications | T023/T043/T064–T066 | T036/T062/T076 |
| FR-017 Authorized recovery/access | T067–T069/T074 | T063/T073/T076–T078 |
| FR-018 Privacy acknowledgement | T011/T038/T043/T048 | T033/T037/T056/T059/T091 |
| FR-019 Confidentiality/isolation | T006/T022/T040/T068 | T051/T063/T095/T099/T111 |
| FR-020 Verified direct actions | T017/T049/T086 | T079/T086/T112 |
| FR-021 Actual isolated preview | T028–T031/T054/T094/T096 | T032/T055/T056/T098/T099 |
| FR-022 Initial HTML/metadata/404 | T018/T019/T085 | T020/T021/T097 |
| FR-023 Mandatory CI/evidence | T005/T007/T008/T025/T094 | T100–T105/T109/T113 |
| FR-024 Operational readiness | T067–T072/T075 | T076/T077/T106/T107/T114 |
| FR-025 Dependencies/approvals | T027/T029/T074/T108/T116 | T090/T091/T109/T115/T117 |

**Conditional FR-020 qualification:** T086 explicitly covers suppression, encoding and deliberate activation with fixture tests. If a verified contact action is enabled, attach actual mobile/desktop launch evidence explicitly to T086/T100 or another acceptance task. DEP-08 records that obligation; fixture encoding tests alone do not prove device launch. This is an additional coverage qualification, not a ninth severity finding.

### Quality criteria

| Criterion | Covered checks | Anchors |
|---|---|---|
| QC-001 Localization | 100% bilingual strings/metadata/alt review, lang/dir, route switching/bidi and native editorial approval | T011–T014/T080/T091 |
| QC-002 Accessibility | Five widths, contrast, keyboard/screen readers, practical ≥44px targets or exceptions, reduced motion/media failures, Lighthouse accessibility ≥95 | T037/T059/T079/T080/T088/T089/T100/T102 |
| QC-003 Performance/discovery | Per-route compressed budgets, initial HTML/SEO, five cold Home/Contact runs per locale, median performance ≥90, LCP ≤2.5s, CLS ≤0.10, lab INP ≤200ms and critical content ≤2s where practicable | T019/T020/T083–T085/T097/T101–T103 |
| QC-004 Security/privacy | Independent validation, fail-closed verification, size/rate limits, parameterized storage, unauthorized access, secret/data isolation and legal feasibility gates | T022/T027/T033–T045/T051/T095/T099/T107/T111 |
| QC-005 Lead reliability | Durable identity/consent, duplicates/conflicts/races, storage/notification faults, interrupted delivery, authorized reconciliation/replay | T023/T036/T043/T056–T058/T062–T078/T098 |
| QC-006 Verification | Formatting/lint/types/unit/component/integration/content/routes/accessibility/build/CI plus actual supported browser/device versions | T002/T004/T005/T008/T025/T045/T052/T073/T088/T094/T100/T113 |
| QC-007 Operations | Safe logs, error/notification alert thresholds, two operators, daily review, rollback preserving leads, lifecycle/backup feasibility | T022/T063/T067–T078/T106/T107/T114/T116 |

The ten success criteria also have task anchors. T104/T105 cover usability outcomes with at least ten testers, ≥85% unassisted completion, villa quotation completion under three minutes and mean trust/contact clarity ≥4.5/5.

Production 30-day reliability, monthly availability, field performance percentiles, full release SEO, approved production lifecycle and restore drills remain future obligations. Preview tests do not establish these outcomes.

## Constitution alignment and phase boundaries

C1 is the confirmed constitution alignment issue. Other reviewed safeguards preserve:

- Arabic RTL default and English LTR with bilingual acceptance.
- Meaningful initial HTML, true localized 404s, noindex protected preview and safe metadata.
- Durable D1 acceptance before confirmation and recoverable notification failure.
- No public inquiry reads/updates; minimal, restricted operational access.
- Synthetic-only protected preview pending legal and processing clearance.
- Actual hosted D1/Turnstile proof; notification simulation explicitly labeled.
- Honest project/contact/content fallbacks and no fabricated facts or approvals.
- Later full marketing pages, genuine gallery, analytics, live email, production deployment and real customer intake kept outside Phase 1 implementation scope.

The draft planning documents' positive readiness statements do not override this analysis's unresolved critical conflict.

## Validation metrics and limitations

| Metric | Result |
|---|---|
| Functional requirements | 25 |
| Quality criteria | 7 |
| Success criteria | 10 |
| FR planned coverage | 25/25, 100% |
| QC planned coverage | 7/7, 100% |
| Wholly unmapped FR/QC | 0 |
| Tasks | 117 unique IDs, T001–T117 |
| Missing task IDs | 0 |
| Parallel markers | 45 |
| Unmapped tasks | None identified; shared tasks support requirements/quality/constitution/research |
| Missing explicit task dependency references | None found |
| Explicit task-ID graph cycles | None found |
| OpenAPI | Valid JSON declaring OpenAPI 3.1; 13 internal references resolved |
| Confirmed duplication findings | 0 |
| Ambiguity/underspecification findings | U1/U2/U3 plus ownership/scope issues I1/I2 and schema precision I3 |
| Severity totals | 1 CRITICAL, 0 HIGH, 6 MEDIUM, 1 LOW |
| Implemented/accepted evidence | Not established by this analysis; all task checkboxes remain unchecked |

No application tests, lint/build, real device checks, hosted fault demonstrations, provisioning or deployment were executed as analysis validation. Structural checks and artifact inspection are not substitutes for those future task outputs.

The prerequisite script ran once during the completed analysis:
`.specify/scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks`.
Required artifacts were available. Its Git-detection warning was checked independently; the feature branch was verified as `001-phase1-lead-foundation`. The observed untracked `tasks.md` was pre-existing and was not created by the analysis.

Some shell calls encountered `helper_unknown_error: setup refresh had errors`; simpler read commands succeeded. An initial CRLF-sensitive task parser was corrected before confirming task counts. No validation pass was inferred from a failed command.

## Readiness for speckit-implement and recommended next steps

**Overall decision: resolve C1 before invoking `speckit-implement`.** The artifacts are complete enough for analysis and have comprehensive task mapping, but a core replay contract remains contradictory.

Recommended order:

1. Reconcile notice rollover/replay semantics across plan, model and contracts; assign explicit tests in T036/T050/T057. Preserve the constitution.
2. Clarify scaffold ownership and foundation-versus-story widget/CSP checks (I1/I2).
3. Define monitoring inputs/cadence/mechanism (U1) and assign supplemental malformed-request flood protection (G1).
4. Specify UUID normalization and reachable invalid-form interaction (U2/U3); tighten health response validation (I3).
5. Explicitly attach real device evidence to any enabled direct-contact action.
6. Re-run `speckit-analyze` on the revised artifacts and resolve remaining blockers.
7. Start `speckit-implement` only after an explicit implementation request. Preserve the existing branch/user work; capture source baselines under T001.
8. Execute independent local work where its prerequisites are met. Record external gates as blocked and never substitute local mocks for required hosted D1/Turnstile, authorized recovery or actual manual/device evidence.
9. Obtain exact-candidate story and Phase 1 acceptance under T061/T078/T092/T109/T117. Phase 1 acceptance does not grant production, real-data or launch authorization.

The recommendations above have not been applied. No remediation to spec, plan, tasks, PRD, constitution or application code is included in this report-saving operation.


## Documentation remediation record — 2026-10-11

The user's remediation request authorizes documentation corrections only. The original finding evidence, line references, severity inventory and analysis metrics above describe the pre-remediation snapshot; this record describes the revised documents without pretending a new analysis ran.

| Finding | Documentation resolution | Affected files (feature-relative) |
|---|---|---|
| C1 CRITICAL | Retained identical requests replay original notice/payload with 200/original reference/createdAt; changed valid retained payload is 409 before new-only current notice; independent controls and atomic race arbitration preserved. Immutable client retry snapshot and explicit A → B lost-response/concurrency/new-request tests assigned. | spec.md, plan.md, data-model.md, contracts/inquiries.openapi.json, contracts/ui-localization.md, tasks.md, quality-strategy.md, quickstart.md, research.md |
| I1 MEDIUM | T003 owns a self-contained minimal root/entry/scaffold route and fresh-checkout build; T018 enhances those same files and removes temporary route; T019 owns final output. | plan.md, tasks.md, quality-strategy.md, quickstart.md |
| I2 MEDIUM | T021 is inert foundation CSP/script fixture scope; T025/T026 run implemented foundation suites. T037/T046 own real widget lifecycle, T053/T055 actual hosted CSP/Turnstile, and candidate CI includes all implemented story suites. | plan.md, tasks.md, quality-strategy.md, quickstart.md |
| U1 MEDIUM | Restricted complete API status feed plus D1 latest/history queries, attended minute evaluation, retention/freshness/coverage, private incident state, owners/backup heartbeat, reset/repeat and escalation specified. Actual source capability and staff/channel approval remain external gates rather than invented provider features. | spec.md, operations.md, dependencies.md, tasks.md, quality-strategy.md, quickstart.md |
| G1 MEDIUM | Existing D1 quota claimed before body reading/parsing replaces unverified edge promise; malformed/oversized attempts consume quota once. Named owner/target/tasks/local+hosted zero-insert/flood criteria and D1-cost/distributed-network tradeoffs recorded. | spec.md, plan.md, data-model.md, contracts/inquiries.openapi.json, tasks.md, quality-strategy.md, research.md |
| U2 MEDIUM | Exact UUID v4/variant validation accepts both hex cases, rejects whitespace/types/other versions, lowercases before exact environment + LF + UUID UTF-8 hashing; case replay tests assigned. | spec.md, data-model.md, contracts/inquiries.openapi.json, tasks.md, quality-strategy.md, research.md |
| U3 MEDIUM | Preserve PRD's disabled Send until valid. Enabled Check form and explicit invalid single-line Enter share validation, announcements and first-invalid focus; textarea newline and token/pending/cooldown paths are testable without disabled-button activation. | spec.md, contracts/ui-localization.md, tasks.md, quality-strategy.md |
| I3 LOW | Separate HealthOk/HealthUnavailable schemas constrain 200/ok and 503/unavailable; crossed combinations fail local/hosted assertions, retaining minimal correlated no-store bodies. | spec.md, plan.md, contracts/inquiries.openapi.json, tasks.md, quality-strategy.md |
| Additional path check | Git root NewKenWebsite versus app/Spec Kit my-project made explicit. Workflows are ../.github/workflows from app root; Actions run steps and npm/Wrangler use my-project with explicit non-run inputs. Existing helper .specify root/Git-warning semantics and independent branch/feature-path checks documented. | spec.md, plan.md, tasks.md, quickstart.md, quality-strategy.md |

**Remaining original findings:** None left intentionally unresolved in documentation; renewed speckit-analyze must independently confirm the resolutions. DEP-01–13 access/approval/capability/equipment gates remain as applicable. In particular, complete monitoring-source capability/permissions, permitted retention and staffed alert coverage are unverified; failure to supply them blocks hosted monitoring acceptance. No credential, named staff member, approval or provider capability is invented.

**Structural validation:** 117 unique task IDs T001–T117; all 117 unchecked; 45 parallel markers; no missing dependency IDs, self-dependencies or explicit dependency cycles (227 explicit task-ID edges); phase-gate expansion is also acyclic. Existing phase counts remain 8/24/29/17/14/17/8; US1/US2/US3/US4 remain 29/17/14/17. T075 additionally depends on T028/T027 for source/policy evidence; T018 explicitly depends on T003 scaffold ownership and T044 on T035 contract-test definition. No task is marked implemented or accepted. Shared-file ownership/phase/external gates still constrain scheduling. OpenAPI JSON parses and all 13 internal references resolve, including status-specific health schemas. Documentation fences/whitespace/local links and path conventions are checked; these are artifact checks, not application/hosted tests.

**Files modified:** analysis-report.md, spec.md, plan.md, tasks.md, data-model.md, contracts/inquiries.openapi.json, contracts/ui-localization.md, quality-strategy.md, operations.md, dependencies.md, quickstart.md, research.md (all inside specs/001-phase1-lead-foundation/). PRD and constitution bytes and feature branch remain unchanged; pre-existing untracked analysis-report.md/tasks.md remain uncommitted.

**Final integration check:** The existing concurrent documentation updates were retained, the spec PRD link was verified as ../../../docs/PRD.md (three parent levels from the feature directory), original-snapshot retry gating was clarified independently of new-draft edits, and the scaffold/contract test-definition dependencies were made explicit. No concurrent work was reset or overwritten.

**Readiness:** Ready for a new non-destructive speckit-analyze run on the revised artifacts. Implementation requires a subsequent explicit request and renewed review; no application code, scripts or workflow files are implemented, no deployment is performed, and no commit/push/task completion occurs. Documentation remediation stops here.
