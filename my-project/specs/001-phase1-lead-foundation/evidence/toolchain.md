# T002 — Toolchain verification and dependency pins

Status: PASS. T002 verification completed at 2026-10-13T16:00:06.206Z: security, clean-install reproduction, native/integrity checks and all required Playwright launches passed. Only T002 is newly completed; T001 and its baseline remain unchanged.

## Authorized Lighthouse CLI remediation — 2026-10-13

This is the latest T002 execution record and supersedes the historical attempts below. The user explicitly authorized replacing vulnerable @lhci/cli 0.15.1 with exactly pinned lighthouse 13.5.0 if required quality behavior is preserved. No T003 or later implementation task is executed.

Environment: Node 24.21.0, npm 11.19.0, Windows x64; branch 001-phase1-lead-foundation; HEAD bb85a0e8aeea45002e486ea46362f9c51b0829f3. T001's checkbox and source-baseline.md remain unchanged; its baseline was not recaptured.

### Dependency decision and installation

Official [Lighthouse 13.5.0 metadata](https://registry.npmjs.org/lighthouse/13.5.0) was checked at 2026-10-13T15:27:39.559Z: Node >=22.19, accepted by 24.21.0; CLI entry cli/index.js. Its [pinned CLI documentation](https://github.com/GoogleChrome/lighthouse/blob/v13.5.0/readme.md) and [configuration documentation](https://github.com/GoogleChrome/lighthouse/blob/v13.5.0/docs/configuration.md) support mobile settings and JSON reporting. Viability depends on the future project's explicit assertions; a successful CLI run alone is not a threshold pass.

Minimal dependency changes:
- Removed direct @lhci/cli 0.15.1.
- Added direct lighthouse 13.5.0.
- Preserved all 31 other direct dependency pins, including the Node/npm pins.
- Added only version-specific native-script approvals in package.json: esbuild@0.28.2 and workerd@1.20261006.1. No blanket allowScripts rule, override or relaxed peer/engine setting was introduced.

`npm install --engine-strict --strict-peer-deps --no-fund --registry=https://registry.npmjs.org` exited 0: added 44, removed 249, changed 17 transitive installed packages, audited 418, 0 vulnerabilities. The genuine lockfile was regenerated without direct-pin drift. These transitive changes accompany the Lighthouse dependency-tree replacement; they are not additional direct package upgrades.

`npm install-scripts approve esbuild workerd` exited 0 and wrote the two exact-version allowScripts entries after their platform selection, pinned binary installation and version-check scripts were reviewed. This narrow project policy allows reproducible native installation. Global npm configuration was not changed.

### Full security and integrity results

- Full `npm audit --json --registry=https://registry.npmjs.org`: exit 0, 0 vulnerabilities at every severity, both immediately after replacement and after clean npm ci.
- Production `npm audit --omit=dev --json --registry=https://registry.npmjs.org`: exit 0, 0 vulnerabilities.
- The complete audit metadata covers 518 locked non-root package entries, including optional platform entries. npm installed/audited 417 packages plus the root on this Windows x64 machine.
- `npm audit signatures --registry=https://registry.npmjs.org`: exit 0; 417 installed packages have verified registry signatures; 164 have verified attestations. No signature failure was suppressed.
- Every resolved non-root lock entry has an integrity field; no non-official registry tarball location was found.
- No npm audit fix, force, legacy-peer-deps, vulnerability suppression, blanket security override or source/budget exception was used. The earlier 17 findings remain visible in the historical record; the full regenerated project audit, not an isolated-package audit, establishes the current result.

### Clean npm ci reproduction

`npm ci --engine-strict --strict-peer-deps --foreground-scripts --no-fund --registry=https://registry.npmjs.org` exited 0. npm removed/recreated generated node_modules in the application root, installed 417 packages and audited 418 in approximately one minute. Both esbuild and Workerd postinstall scripts visibly ran; no unreviewed native-script warning remained in this run. No user source/workspace directory was manually deleted.

Before/after hashes are identical:
- package.json SHA-256: `99b451da0b61f75743c20b243cf4e3bdba49d679edcc15e861633983812434db`
- package-lock.json SHA-256: `51b192fcd0fea2bba66e3c2ae3817d32bc967b6ac3574571fc2522948ccd6b5b`
- Sorted lock packages graph SHA-256: `14788be4affa71ecb865a5dfb7e24f04ff0b6b56e0fe6f236d3f0845f82e4cb3`

Lockfile version is 3, with 518 non-root entries. All 32 locked direct versions match package.json. `npm ls --depth=0` and `npm ls --all --json` exited 0 with no graph problems; all installed declared Node engine requirements accept 24.21.0. Verification timestamp: 2026-10-13T15:34:53.689Z. Package downloads use npm's lock integrity checks; registry signatures supply the additional recorded check.

### Native and CLI verification

An in-memory toolchain probe, with no application files or Cloudflare configuration, verified:
- esbuild 0.28.2: native transform service successfully processed a trivial JavaScript expression.
- Workerd package 1.20261006.1: node_modules/workerd/bin/workerd --version exited 0, output workerd 2026-10-06, empty stderr.
- Sharp 0.35.5 / libvips 8.18.7: created a 1x1 PNG buffer in memory (91 bytes); no website asset was written.
- Tailwind oxide native Scanner and Rolldown native module loaded successfully.
- Lighthouse CLI --version, --help and --list-all-audits exited 0; version 13.5.0, JSON/config/mobile/throttling flags available, LCP and CLS audits present.
- Installed Lighthouse schema/metric sources confirm lighthouseVersion, configSettings, categories, runtimeError and audit numericValue; CLS uses a unitless numeric result. No website performance score or accessibility acceptance was measured by these probes.

### Playwright verification

Installation command: `node node_modules/playwright/cli.js install --no-remove chromium firefox webkit`, using pinned Playwright 1.64.0. No branded-browser package or npm dependency was added. Existing cache versions are preserved.

Actual result: installer exited 0. It installed Chromium 156.0.8078.4 (revision 1248), matching headless shell, Firefox 157.0 (revision 1555), WebKit 27.2 (revision 2370), FFmpeg revision 1013 and Winldd revision 1007 in the normal local Playwright cache. ECONNRESET/ETIMEDOUT errors on auxiliary/headless downloads recovered through the installer's official-host retries; they were not suppressed and did not require a version change, system-browser substitution or force flag.

At 2026-10-13T16:00:06.206Z, a headless probe exited 0. Expected executable files existed for all three engines; each launched, opened about:blank, evaluated a trivial JavaScript expression to 4 and closed successfully. Actual browser.version results: Chromium 156.0.8078.4, Firefox 157.0, WebKit 27.2. Playwright package/CLI version is 1.64.0. This is local toolchain validation, not website QA or real Safari/device acceptance. The package-lock hash still matched the clean npm ci value after browser installation. A final npm install-scripts ls exited 0 with 'No packages with unreviewed install scripts.'

## Lighthouse CLI migration plan

This is a documented handoff for later tasks, not an implemented runner, CI workflow or performance test. The quality tooling row in plan.md and the migration note in quality-strategy.md now point to this approved replacement; the original research selection is superseded only for Lighthouse tooling.

| Existing owner | Future responsibility; retained files and gates |
|---|---|
| T020 | Implement scripts/check-performance.ts plus config/lighthouse.cjs and config/performance-profile.json using the pinned local Lighthouse CLI. Connect existing mandatory check:performance behavior only when owned implementation exists; no stub success. Existing build audit/performance-budgets.json retains transfer/CSP/content responsibilities. |
| T101 | Obtain QA/Product Owner DEP-12 agreement and freeze actual Node/npm/Lighthouse/Chrome versions, hardware/runner, throttling method and profile. Proposed settings remain 390x844, DPR1, 4x CPU, 150ms RTT, 1600Kbps down/750Kbps up, cold cache and no warm worker. Honor any subsequently approved profile; no unapproved replacement defaults. |
| T102 | Extend the baseline runner to five independent cold mobile runs for each Home/Contact locale: Home ar/en and Contact ar/en, 20 required reports total, plus representative privacy accessibility checks. Preserve per-run/median evidence, private artifacts, hosted Turnstile costs and locale/template separation. |

Runner contract:
1. Spawn the local cli/index.js with a URL selected from the verified route manifest, JSON output and private per-run output path; use the frozen config and a verified explicit Chrome binary. Each run starts an independent browser process/profile with cleared storage/cache and no warmed worker; never disable storage reset, reuse a warm browser result or aggregate across templates/locales. Actual resolved settings must be validated and recorded, not inferred from defaults. Proposed simulated Lighthouse throttling and DevTools-applied interaction throttling remain explicitly distinguished.
2. Parse each JSON report. Require the pinned lighthouseVersion, matching requested/final locale route, agreed configSettings and finite numeric category/metric values. Reject absent/invalid/truncated reports, runtimeError, audit errors, null/NaN scores, nonzero CLI exits, timeouts, profile mismatch and incomplete/duplicate run sets. Do not keep retrying until five favorable scores appear; retain attempted failures and require explicit remediation/retest.
3. Read categories.performance.score and categories.accessibility.score (0–1), audits['largest-contentful-paint'].numericValue (milliseconds) and audits['cumulative-layout-shift'].numericValue (unitless). Compute the median by sorting the five values and selecting the third, independently for each required group. Compare unrounded values; presentation rounding must not make a failure pass.
4. Enforce median Performance >=0.90 (90/100); Accessibility >=0.95 (95/100) for required representative Home/Contact/privacy reports; LCP <=2500ms and CLS <=0.10, with the existing per-run/median assessment and remediation requirements. Keep all failures visible; no score filtering, locale averaging, metric replacement or silently weakened threshold. CI exits nonzero when a required threshold or report/profile/run-count check fails.
5. Preserve transfer budgets independently of Lighthouse scores: Home/Contact/privacy-preparation JS gzip 150/180/150 KiB, CSS gzip 30 KiB each, selected-locale WOFF2 120 KiB each, above-fold media 200/80/80 KiB, initial first-party total 550/450/450 KiB. Count route-used shared chunks once, actual font/media bytes and all required HTML/data. A Lighthouse score cannot replace the build transfer audit. Include hosted Turnstile costs in speed measurement; do not block its traffic to inflate scores.
6. Keep the existing two-second critical-content trace, <=200ms interaction checks, manual accessibility/native reviews and real-device/browser gates. TBT is not INP, navigation Lighthouse is not an interaction/field-percentile test, and emulated WebKit is not real Safari evidence. No analytics collection is introduced.
7. Later CI must execute both performance assertions and the build/budget audit as mandatory failing steps, without continue-on-error or success masking. T020/T102 must verify failure behavior using deliberately violating/incomplete report fixtures in their implementation tasks. All raw/summary reports remain private, revision/tool/profile/locale linked and excluded from public build output.

The CLI's collection/reporting capabilities and typed fields are verified now; the proposed wrapper's threshold assertions, run orchestration and CI integration will be verified in their owning tasks. No check:performance script, lighthouse configuration, route/page, fixture suite or workflow was created during T002.

### T002 acceptance accounting

| Criterion | Actual result |
|---|---|
| Node/npm pins, supported patches/engines/peers | PASS: 24.21.0 / 11.19.0, unchanged unrelated direct pins |
| Authorized Lighthouse replacement preserves required quality contract | PASS for tool choice/documented contract; later runner execution explicitly pending |
| Genuine lock and clean npm ci reproduce same graph | PASS: identical manifest/lock/graph hashes |
| Complete project security audit | PASS: zero findings |
| Registry integrity/signatures | PASS: 417 verified signatures, 164 attestations |
| Native prerequisites | PASS: reviewed version-specific script approvals and actual binary probes |
| Required Playwright bundled browser installation and launches | PASS: installer exit 0; Chromium/Firefox/WebKit executable and headless JS probes pass |

**Completion decision:** All actual T002 toolchain criteria pass. T002 may be checked; this grants no T003/later-task, application quality, hosted, profile-approval or production acceptance. No T002 blocker remains. Known later obligations include implementing/testing the documented Lighthouse assertion runner in its owning tasks, renewed consistency analysis and existing external approval/manual/device/performance gates. The audit is a timestamped result, not a guarantee against future advisories.

T001 and its baseline remain unchanged. PRD, constitution, design direction and .node-version are preserved. Only related package/lock/toolchain/plan/quality documentation and, on a genuine pass, T002's checkbox may change. No T003 or later task, UI, production/customer data, deployment, Cloudflare configuration, commit or push is authorized/executed.

## Historical T002 attempts

The following records remain for provenance. Their old dependency security findings and pending checks describe earlier attempts; the latest remediation record above controls current status.


Status: BLOCKED. Authorized installation generated a genuine lockfile, but the full security audit failed. T002 remains unchecked; T001 was not repeated or modified.

## Authorized T002 continuation — 2026-10-13

Latest read-only verification timestamp: 2026-10-13T15:06:31.618Z.
Application root: `C:/Users/0heyw/OneDrive/Desktop/NewKenWebsite/my-project`.
Git root: `C:/Users/0heyw/OneDrive/Desktop/NewKenWebsite`; branch remains `001-phase1-lead-foundation`.
The user authorized pinned dependency and Playwright browser installation for T002 only, and explicitly required stopping on installation, compatibility or audit issues before unapproved dependency changes. Existing T001 status/evidence were retained.

### Active environment and compatible pins

- `node --version`: v24.21.0; `npm --version`: 11.19.0. Both match package.json engines/packageManager and .node-version.
- Official exact-version registry recheck at 2026-10-13T15:00:48.401Z: all 32 direct pins exist, are not deprecated and declare compatible Node engines. No direct peer conflict was found; playwright-core is provided through the pinned Playwright tree.
- After installation, every installed package with a declared Node engine accepts 24.21.0. `npm ls --depth=0` and `npm ls --all --json` both exited 0; the full listing had no reported problems.
- package.json and .node-version were not modified. No direct or unrelated dependency was added. No force, legacy-peer-deps, engine bypass, audit fix or override was used.

| Installed direct package / official metadata | Installed version | Approved pin | Node 24.21.0 engine |
|---|---|---|---|
| [libphonenumber-js](https://registry.npmjs.org/libphonenumber-js/1.13.15) | 1.13.15 | Match | Pass |
| [react](https://registry.npmjs.org/react/19.3.0) | 19.3.0 | Match | Pass |
| [react-dom](https://registry.npmjs.org/react-dom/19.3.0) | 19.3.0 | Match | Pass |
| [react-router](https://registry.npmjs.org/react-router/8.4.0) | 8.4.0 | Match | Pass |
| [zod](https://registry.npmjs.org/zod/4.6.7) | 4.6.7 | Match | Pass |
| [@axe-core/playwright](https://registry.npmjs.org/%40axe-core%2Fplaywright/4.13.0) | 4.13.0 | Match | Pass |
| [@cloudflare/vitest-plugin](https://registry.npmjs.org/%40cloudflare%2Fvitest-plugin/1.4.1) | 1.4.1 | Match | Pass |
| [@eslint/js](https://registry.npmjs.org/%40eslint%2Fjs/10.0.1) | 10.0.1 | Match | Pass |
| [@lhci/cli](https://registry.npmjs.org/%40lhci%2Fcli/0.15.1) | 0.15.1 | Match | Pass |
| [@playwright/test](https://registry.npmjs.org/%40playwright%2Ftest/1.64.0) | 1.64.0 | Match | Pass |
| [@react-router/dev](https://registry.npmjs.org/%40react-router%2Fdev/8.4.0) | 8.4.0 | Match | Pass |
| [@tailwindcss/vite](https://registry.npmjs.org/%40tailwindcss%2Fvite/4.3.3) | 4.3.3 | Match | Pass |
| [@testing-library/dom](https://registry.npmjs.org/%40testing-library%2Fdom/10.4.2) | 10.4.2 | Match | Pass |
| [@testing-library/jest-dom](https://registry.npmjs.org/%40testing-library%2Fjest-dom/7.0.1) | 7.0.1 | Match | Pass |
| [@testing-library/react](https://registry.npmjs.org/%40testing-library%2Freact/16.3.3) | 16.3.3 | Match | Pass |
| [@testing-library/user-event](https://registry.npmjs.org/%40testing-library%2Fuser-event/14.6.8) | 14.6.8 | Match | Pass |
| [@types/node](https://registry.npmjs.org/%40types%2Fnode/24.19.2) | 24.19.2 | Match | Pass |
| [@types/react](https://registry.npmjs.org/%40types%2Freact/19.3.0) | 19.3.0 | Match | Pass |
| [@types/react-dom](https://registry.npmjs.org/%40types%2Freact-dom/19.3.0) | 19.3.0 | Match | Pass |
| [eslint](https://registry.npmjs.org/eslint/10.12.0) | 10.12.0 | Match | Pass |
| [eslint-plugin-react-hooks](https://registry.npmjs.org/eslint-plugin-react-hooks/7.1.1) | 7.1.1 | Match | Pass |
| [eslint-plugin-react-refresh](https://registry.npmjs.org/eslint-plugin-react-refresh/0.5.7) | 0.5.7 | Match | Pass |
| [globals](https://registry.npmjs.org/globals/17.13.0) | 17.13.0 | Match | Pass |
| [jsdom](https://registry.npmjs.org/jsdom/30.1.2) | 30.1.2 | Match | Pass |
| [prettier](https://registry.npmjs.org/prettier/3.9.10) | 3.9.10 | Match | Pass |
| [sharp](https://registry.npmjs.org/sharp/0.35.5) | 0.35.5 | Match | Pass |
| [tailwindcss](https://registry.npmjs.org/tailwindcss/4.3.3) | 4.3.3 | Match | Pass |
| [typescript](https://registry.npmjs.org/typescript/6.0.3) | 6.0.3 | Match | Pass |
| [typescript-eslint](https://registry.npmjs.org/typescript-eslint/8.71.2) | 8.71.2 | Match | Pass |
| [vite](https://registry.npmjs.org/vite/8.3.4) | 8.3.4 | Match | Pass |
| [vitest](https://registry.npmjs.org/vitest/4.1.11) | 4.1.11 | Match | Pass |
| [wrangler](https://registry.npmjs.org/wrangler/4.150.0) | 4.150.0 | Match | Pass |

### Installation, lockfile and integrity

Command, run from my-project:

`npm install --engine-strict --strict-peer-deps --no-fund --registry=https://registry.npmjs.org`

Actual result: exit 0; added 622 packages and audited 623 in approximately four minutes. This is successful dependency resolution/download, not a completed native-runtime/security/toolchain pass. npm reported 17 vulnerabilities and pending install scripts.

package-lock.json parses as lockfileVersion 3 and contains 723 non-root package entries, including optional platform-specific packages not installed on Windows x64. This differs from the install's 623 audited installed-package count because the lock records optional platforms as well. All 32 direct locked versions match the manifest; every non-link resolved entry has an integrity field and valid version. No integrity-mismatch download error was reported. Registry signature/provenance verification was not run after the audit stop and is not claimed passed.

SHA-256:
- package-lock.json: `0ed5c7306841d889e7625e2cb6422bed8d1e1604f9d2e2686a0938e76de0026b`
- Unchanged package.json: `8980e8a190e67858c3513e2762a3d11d5eda852832f8158cfbafbe701cc62cd1`
- Unchanged .node-version: `73fb1b615e2043a933be1c0895cde4358036acc28d785692509b822aa53c761f`

`npm install-scripts ls` exited 0 and confirmed two scripts still not covered by allowScripts:
- esbuild 0.28.2: postinstall `node install.js`
- workerd 1.20261006.1: postinstall `node install.js`

No script approval/denial was applied, and no package/Cloudflare configuration was changed. Native-tool execution remains unverified; the install's exit 0 cannot establish that these scripts ran.

Deprecation warnings were preserved: inflight 1.0.6 (unsupported/memory leak), glob 7.2.3 (unsupported/security warning), rimraf 3.0.2 and 2.7.1, and uuid 8.3.2. These were not hidden or silently upgraded.

### Security audit — FAIL

`npm audit --json --registry=https://registry.npmjs.org` exited 1.
Actual totals: **17 affected package entries: 11 high, 4 moderate, 2 low, 0 critical**. These include meta-vulnerable parents, so they are not 17 distinct advisories.

`npm explain @lhci/cli lighthouse tmp extract-zip basic-ftp uuid sprintf-js` exited 0. The vulnerable chains are rooted in the direct development dependency @lhci/cli 0.15.1, including its @lhci/utils/inquirer/Lighthouse/Puppeteer/proxy dependencies. Their development classification does not make T002's security check pass.

| Affected package | Resolved version(s) | npm severity | Advisory / vulnerable child |
|---|---|---|---|
| @lhci/cli | 0.15.1 | high | Inherited from @lhci/utils, inquirer, lighthouse, proxy-agent, tmp, uuid |
| @lhci/utils | 0.15.1 | high | Inherited from js-yaml, lighthouse |
| @puppeteer/browsers | 2.13.2 | high | Inherited from extract-zip, proxy-agent |
| argparse | 1.0.10 | moderate | Inherited from sprintf-js |
| basic-ftp | 5.3.1 | high | [GHSA-c475-qrg2-pj4r](https://github.com/advisories/GHSA-c475-qrg2-pj4r) |
| external-editor | 3.1.0 | low | Inherited from tmp |
| extract-zip | 2.0.1 | high | [GHSA-jmr9-qjv8-65gv](https://github.com/advisories/GHSA-jmr9-qjv8-65gv), [GHSA-7pqw-9j4j-h8q3](https://github.com/advisories/GHSA-7pqw-9j4j-h8q3) |
| get-uri | 6.0.5 | high | Inherited from basic-ftp |
| inquirer | 6.5.2 | low | Inherited from external-editor |
| js-yaml | 3.15.2 | moderate | Inherited from argparse |
| lighthouse | 12.6.1 | high | Inherited from puppeteer-core |
| pac-proxy-agent | 7.2.0 | high | Inherited from get-uri |
| proxy-agent | 6.5.0 | high | Inherited from pac-proxy-agent |
| puppeteer-core | 24.43.1 | high | Inherited from @puppeteer/browsers |
| sprintf-js | 1.0.3 | moderate | [GHSA-hp3w-g68c-fv3c](https://github.com/advisories/GHSA-hp3w-g68c-fv3c) |
| tmp | 0.0.33, 0.1.0 | high | [GHSA-52f5-9888-hmc6](https://github.com/advisories/GHSA-52f5-9888-hmc6), [GHSA-ph9p-34f9-6g65](https://github.com/advisories/GHSA-ph9p-34f9-6g65) |
| uuid | 8.3.2 | moderate | [GHSA-w5hq-g745-h8pq](https://github.com/advisories/GHSA-w5hq-g745-h8pq) |

Representative verified chains:
- @lhci/cli 0.15.1 → Lighthouse 12.6.1 → puppeteer-core 24.43.1 → @puppeteer/browsers 2.13.2 → extract-zip 2.0.1.
- @lhci/cli / @puppeteer/browsers → proxy-agent 6.5.0 → pac-proxy-agent 7.2.0 → get-uri 6.0.5 → basic-ftp 5.3.1.
- @lhci/cli → inquirer 6.5.2 → external-editor 3.1.0 → tmp 0.0.33; @lhci/cli also directly resolves tmp 0.1.0 and uuid 8.3.2.
- @lhci/cli → @lhci/utils 0.15.1 → js-yaml 3.15.2 → argparse 1.0.10 → sprintf-js 1.0.3.

npm suggested `npm audit fix --force` and its JSON fix candidate for @lhci/cli is **0.1.0**, flagged as a breaking change. This would change the approved 0.15.1 pin and is not an approved or verified remedy. It was not executed. No vulnerability suppression, audit threshold weakening, dependency removal or unapproved substitution was performed.

### Clean npm ci and Playwright — NOT RUN / BLOCKED

The security stop occurred before clean npm ci. No clean-install reproduction or same-lock comparison is claimed. [npm ci documentation](https://docs.npmjs.com/cli/v11/commands/npm-ci/) describes its lock-preserving behavior; that documentation is not executed evidence.

@playwright/test, playwright and playwright-core 1.64.0 are installed in the resolved graph. A read-only executablePath existence check returned false for all three required bundled engines:
- Chromium: absent.
- Firefox: absent.
- WebKit: absent.

No browser download or launch was attempted after the audit issue. Existing Chrome/Edge from the historical inventory are not a substitute for these pinned engine checks. Later real Safari/device acceptance remains separate. [Playwright browser documentation](https://playwright.dev/docs/browsers) was reviewed; no website QA or T003 scaffold was created.

### Acceptance accounting and remaining blockers

| T002 criterion | Actual continuation result |
|---|---|
| Active supported Node/npm | PASS: 24.21.0 / 11.19.0 |
| Exact patch availability, engines and peers | PASS at metadata and installed npm ls/engine level |
| Approved exact direct pins preserved | PASS: all 32 unchanged |
| Genuine package-lock.json generation | PASS: v3, exact direct pins and integrity fields |
| Installation complete including native prerequisites | PARTIAL: downloads/resolution pass; esbuild/Workerd scripts pending and execution unverified |
| Full security audit | FAIL: 17 findings, including 11 high |
| Clean npm ci reproduces the same lock | BLOCKED: not attempted after audit stop |
| Additional registry signature/provenance verification | Pending; not claimed passed |
| Required Playwright browser availability | BLOCKED: three engines absent, no download after stop |
| T002 completion checkbox | Unchanged and unchecked |

The previous Node/npm mismatch is resolved. Remaining T002 blockers are the Lighthouse CI dependency-tree vulnerabilities, pending reviewed install scripts/native verification, clean npm ci reproduction and required browser installation/launch checks. No renewed speckit-analyze or later task was executed; the previously documented analysis prerequisite belongs before later scaffold work.

Only package-lock.json was created and this toolchain evidence document updated by this continuation; node_modules is generated local installation output. package.json, .node-version, tasks.md, T001 evidence, PRD, constitution, design direction and plan hashes match the continuation's initial checks. T001 stays completed and T002/T003 onward stay unchecked. No Git ignore/config file was added under this T002-only authorization. No application components/pages/tests/scaffold, deployment, Cloudflare resources/configuration, real data, commit or push was created.

### Recommended next action

Review and approve a specific secure, compatible remediation for the pinned Lighthouse CI dependency tree before any dependency changes. Do not adopt npm's force downgrade as an assumed fix. After the approved remediation is applied and the full audit passes, review the exact esbuild/Workerd install scripts, finish native/integrity checks, run clean npm ci in an isolated temporary directory with unchanged lock hash and resolved graph, then install and launch-check the pinned Chromium/Firefox/WebKit engines. T002 can be marked only after those actual checks pass. Stop before T003.

## Historical pre-installation record

The following record describes the earlier T001/T002 attempt, before the environment upgrade and installation authorization. Its pending permissions, absent lock/node_modules and old Node/npm statements are historical, superseded by the continuation above.


Status: BLOCKED. Partial outputs prepared; T002 remains unchecked.
Candidate HEAD: `bb85a0e8aeea45002e486ea46362f9c51b0829f3`; branch `001-phase1-lead-foundation`.
Final exact-version registry verification: 2026-10-13T14:28:33.973Z.
Local Windows x64 metadata verification only; no hosted URL, application/schema build, migration or synthetic customer submission applies.

## Detected development environment

| Tool | Detected version / availability | Result |
|---|---|---|
| Node.js | 24.11.1; `C:/Program Files/nodejs/node.exe` | Node 24 line matches plan; installed patch fails selected jsdom engine and prepared exact project pin |
| npm | 11.6.2 | Available; target pin is bundled npm 11.19.0 |
| Git | 2.51.0.windows.1; `D:/NewApp/Git/cmd/git.exe` | Available; correct parent-root branch/clean initial tree verified in T001 |
| PowerShell | 7.6.6 | Available; read-only Spec Kit helper ran |
| ripgrep | 15.2.0; PCRE2 10.45 | Available |
| Chrome | 154.0.8037.98 | Installed executable file version inspected; browser not launched |
| Edge | 155.0.4283.45 | Installed executable file version inspected; browser not launched |
| Wrangler, TypeScript CLI, Vite, Vitest, Playwright, ESLint, Prettier | No commands on PATH; no application node_modules | Not installed for this project; do not use download-on-demand npx |
| GitHub CLI | No gh command on PATH | Optional here; later repository/CI access is DEP-05 |
| Playwright browser binaries | Cache contains only .links; no browser distribution directory | Required downloads pending approval; existing Chrome/Edge do not prove pinned Playwright engine availability |
| Firefox | Not found at standard Program Files path | No claim of complete browser/device QA; later DEP-12 gate |

Inventory used Get-Command, node/npm/git version commands, PSVersionTable, rg --version, Test-Path, Get-Item VersionInfo and a names-only Playwright cache listing. No credentials or account login state was inspected. Node reported win32/x64.

Initial package.json, package-lock.json, .node-version and node_modules were absent. Prepared `package.json` now pins all direct dependencies exactly, declares private/module metadata, Node 24.21.0 and npm 11.19.0. `.node-version` pins 24.21.0. No scaffold, application scripts, source/UI, test configuration or Cloudflare configuration was created.

## Official availability, engines and peers

Initial research queried official npm registry package version lists, selected the highest stable patch within each planned range using npm's already-bundled semver implementation, and fetched engines/peerDependencies. A Vite version-list request timed out; the successful official latest endpoint returned 8.3.4, within the planned 8.3.x range. Final verification independently fetched every exact version endpoint below. Every endpoint succeeded, no selected version is deprecated, and the complete prepared direct set has zero unsatisfied mandatory peers in this metadata check. This is not an installed-graph or native-runtime pass.

All listed Node engine ranges accept target Node 24.21.0. Installed Node 24.11.1 fails jsdom 30.1.2. No planned major was silently substituted: TypeScript stays 6.0.x, Vite 8.3.x, React 19.3.0, Router/dev 8.4.0, Tailwind/plugin 4.3.x and Vitest 4.1.x. Newer TypeScript 7/Vitest 5/npm 12 dist-tags were not adopted.

| Package / official metadata | Exact version | Node engine | Installed 24.11.1 | Target 24.21.0 |
|---|---|---|---|---|
| [libphonenumber-js](https://registry.npmjs.org/libphonenumber-js/1.13.15) | 1.13.15 | Not declared | Pass | Pass |
| [react](https://registry.npmjs.org/react/19.3.0) | 19.3.0 | >=0.10.0 | Pass | Pass |
| [react-dom](https://registry.npmjs.org/react-dom/19.3.0) | 19.3.0 | Not declared | Pass | Pass |
| [react-router](https://registry.npmjs.org/react-router/8.4.0) | 8.4.0 | >=22.22.0 | Pass | Pass |
| [zod](https://registry.npmjs.org/zod/4.6.7) | 4.6.7 | Not declared | Pass | Pass |
| [@axe-core/playwright](https://registry.npmjs.org/%40axe-core%2Fplaywright/4.13.0) | 4.13.0 | Not declared | Pass | Pass |
| [@cloudflare/vitest-plugin](https://registry.npmjs.org/%40cloudflare%2Fvitest-plugin/1.4.1) | 1.4.1 | Not declared | Pass | Pass |
| [@eslint/js](https://registry.npmjs.org/%40eslint%2Fjs/10.0.1) | 10.0.1 | ^20.19.0 || ^22.13.0 || >=24 | Pass | Pass |
| [@lhci/cli](https://registry.npmjs.org/%40lhci%2Fcli/0.15.1) | 0.15.1 | Not declared | Pass | Pass |
| [@playwright/test](https://registry.npmjs.org/%40playwright%2Ftest/1.64.0) | 1.64.0 | >=20 | Pass | Pass |
| [@react-router/dev](https://registry.npmjs.org/%40react-router%2Fdev/8.4.0) | 8.4.0 | >=22.22.0 | Pass | Pass |
| [@tailwindcss/vite](https://registry.npmjs.org/%40tailwindcss%2Fvite/4.3.3) | 4.3.3 | Not declared | Pass | Pass |
| [@testing-library/dom](https://registry.npmjs.org/%40testing-library%2Fdom/10.4.2) | 10.4.2 | >=18 | Pass | Pass |
| [@testing-library/jest-dom](https://registry.npmjs.org/%40testing-library%2Fjest-dom/7.0.1) | 7.0.1 | >=22 | Pass | Pass |
| [@testing-library/react](https://registry.npmjs.org/%40testing-library%2Freact/16.3.3) | 16.3.3 | >=18 | Pass | Pass |
| [@testing-library/user-event](https://registry.npmjs.org/%40testing-library%2Fuser-event/14.6.8) | 14.6.8 | >=12 | Pass | Pass |
| [@types/node](https://registry.npmjs.org/%40types%2Fnode/24.19.2) | 24.19.2 | Not declared | Pass | Pass |
| [@types/react](https://registry.npmjs.org/%40types%2Freact/19.3.0) | 19.3.0 | Not declared | Pass | Pass |
| [@types/react-dom](https://registry.npmjs.org/%40types%2Freact-dom/19.3.0) | 19.3.0 | Not declared | Pass | Pass |
| [eslint](https://registry.npmjs.org/eslint/10.12.0) | 10.12.0 | ^20.19.0 || ^22.13.0 || >=24 | Pass | Pass |
| [eslint-plugin-react-hooks](https://registry.npmjs.org/eslint-plugin-react-hooks/7.1.1) | 7.1.1 | >=18 | Pass | Pass |
| [eslint-plugin-react-refresh](https://registry.npmjs.org/eslint-plugin-react-refresh/0.5.7) | 0.5.7 | Not declared | Pass | Pass |
| [globals](https://registry.npmjs.org/globals/17.13.0) | 17.13.0 | >=18 | Pass | Pass |
| [jsdom](https://registry.npmjs.org/jsdom/30.1.2) | 30.1.2 | ^22.22.2 || ^24.15.0 || >=26.0.0 | FAIL | Pass |
| [prettier](https://registry.npmjs.org/prettier/3.9.10) | 3.9.10 | >=14 | Pass | Pass |
| [sharp](https://registry.npmjs.org/sharp/0.35.5) | 0.35.5 | >=20.9.0 | Pass | Pass |
| [tailwindcss](https://registry.npmjs.org/tailwindcss/4.3.3) | 4.3.3 | Not declared | Pass | Pass |
| [typescript](https://registry.npmjs.org/typescript/6.0.3) | 6.0.3 | >=14.17 | Pass | Pass |
| [typescript-eslint](https://registry.npmjs.org/typescript-eslint/8.71.2) | 8.71.2 | ^18.18.0 || ^20.9.0 || >=21.1.0 | Pass | Pass |
| [vite](https://registry.npmjs.org/vite/8.3.4) | 8.3.4 | ^20.19.0 || >=22.12.0 | Pass | Pass |
| [vitest](https://registry.npmjs.org/vitest/4.1.11) | 4.1.11 | ^20.0.0 || ^22.0.0 || >=24.0.0 | Pass | Pass |
| [wrangler](https://registry.npmjs.org/wrangler/4.150.0) | 4.150.0 | >=22.0.0 | Pass | Pass |
| [npm](https://registry.npmjs.org/npm/11.19.0) | 11.19.0 | ^20.17.0 || >=22.9.0 | Pass | Pass |
| [playwright](https://registry.npmjs.org/playwright/1.64.0) | 1.64.0 | >=20 | Pass | Pass |
| [playwright-core](https://registry.npmjs.org/playwright-core/1.64.0) | 1.64.0 | >=20 | Pass | Pass |

The final three rows are tool/transitive verification: npm is pinned via packageManager/engines, and playwright/playwright-core 1.64.0 are supplied by @playwright/test → playwright. They are not added as redundant direct dependencies. libphonenumber-js/max is the max-metadata import of libphonenumber-js, not a separately installable package.

Key peer checks:
- react-dom requires react ^19.3.0; Router accepts React/DOM >=19.2.7.
- @react-router/dev accepts Vite ^7 || ^8, TypeScript ^5.1 || ^6 || ^7, Router ^8.4, and optional Wrangler ^4. RSC/serve peers are optional and omitted for the selected static/no-runtime-SSR architecture.
- Tailwind Vite accepts Vite ^8. Vitest 4.1.11 accepts Vite ^8 and selected Node types. Cloudflare plugin 1.4.1 accepts Vitest ^4.1 || ^5 and depends on Wrangler 4.150.0, matching the direct pin.
- Testing Library React accepts React/DOM/types 19 and DOM ^10; user-event and jest-dom accept selected DOM/Vitest.
- typescript-eslint 8.71.2 accepts TypeScript >=4.8.4 <6.1 and ESLint 10; @eslint/js/hooks/refresh accept selected ESLint 10.
- Optional canvas, Vitest UI/coverage/browser packages, Vite preprocessors/devtools and Wrangler worker types are not required by T002 and are not added speculatively.

[Cloudflare plugin documentation](https://developers.cloudflare.com/workers/testing/vitest-integration/migration-guides/migrate-to-vitest-plugin/) and [Sharp installation documentation](https://sharp.pixelplumbing.com/install/) were reviewed. Sharp 0.35.5 declares Node >=20.9.0 and an optional @img/sharp-win32-x64 0.35.5 binary; Tailwind oxide 4.3.3 declares Node >=20 and a win32-x64-msvc binary. These match this platform at metadata level. Binary availability in the installed tree and Sharp/Workerd/Playwright execution remain unverified until installation. A C++ toolchain is not assumed required for supported prebuilt packages; a source-build fallback would require a new prerequisite check.

No fonts, motion or 3D packages were selected. Proposed Alexandria / IBM Plex Sans Arabic / Manrope assets and the premium palette remain unchanged; exact font rights/bytes/shaping belong to T084 and DEP-02/12.

## Node and advisory review

The [official Node distribution index](https://nodejs.org/dist/index.json) reports Node 24.21.0, Krypton LTS, Windows x64 distributions and bundled npm 11.19.0. [Official release notes](https://github.com/nodejs/node/releases/tag/v24.21.0) confirm this Node 24 patch. The installed patch predates the [July 2026 security update](https://nodejs.org/en/blog/vulnerability/july-2026-security-releases), whose Node 24 fixes were released in 24.18.1. Upgrade within Node 24 rather than weakening jsdom's engine or changing the architecture. The target is prepared but not installed or executed.

The final official npm bulk advisory endpoint `https://registry.npmjs.org/-/npm/v1/security/advisories/bulk` returned HTTP 200 and `{}` for every exact manifest dependency, npm 11.19.0, playwright 1.64.0 and playwright-core 1.64.0 at the timestamp above. Initial direct candidates also returned no advisories. Only package names/versions were sent. This direct-package result does not audit all transitives, npm's bundled graph, tarball integrity, supply-chain provenance or runtime vulnerabilities. The complete locked graph must be audited after authorized resolution; no clean full-audit claim is made now.

## Verification criteria and blockers

| T002 criterion | Actual result |
|---|---|
| T001 completed | PASS; baseline recorded before existing-file edits |
| Planned release availability / exact patches checked | PASS for all prepared direct pins |
| Target engines and mandatory peers checked | PASS at metadata level; installed Node FAILS jsdom |
| package.json exact direct pins | Prepared |
| .node-version exact LTS patch | Prepared, actual machine upgrade pending |
| package-lock.json produced by genuine resolver | BLOCKED; absent, never fabricated |
| Authorized installation succeeds | BLOCKED; user explicitly requires approval first; none attempted |
| Clean npm ci reproduces the lock | BLOCKED; installation/lock absent, no npm ci attempted |
| Full transitive advisory/native/runtime verification | BLOCKED; no resolved installed graph |

Missing prerequisites to complete T002: approval and execution of the Node 24.21.0/npm 11.19.0 upgrade; approval to install the exact manifest dependencies and required Playwright binaries; genuine package-lock.json resolution; full lock audit and native-tool verification; an isolated clean npm ci run with identical lock hash and dependency resolution. Avoid clearing or deleting the user's existing workspace to simulate a clean checkout.

The renewed speckit-analyze review remains a documented prerequisite before later scaffold work; it was not run under this limited request. External DEP-01–13 approvals/access/assets remain outstanding where applicable and do not authorize cloud resources, real intake or deployment.

## Exact recommended next action

Request approval to upgrade to Node 24.21.0 with bundled npm 11.19.0 and install the pinned package.json set plus the required Playwright browsers, solely to finish T002. After approval, verify actual Node/npm versions, run npm install to create the genuine lockfile, run npm audit on the complete graph, verify installed versions/native CLIs, then run npm ci in a separate temporary clean directory and compare before/after lock hashes and resolved versions. Record the actual outcomes here. Mark T002 only if every required check passes, then stop again; T003 needs separate authorization.

No package installation, lock-only install, npm ci, application test/build, cloud provisioning, real-data connection, deployment, commit or push was executed. Optional Spec Kit commit hooks were inspected and skipped under the explicit user prohibition.
