# External Dependencies and Approval Register

As of 2026-10-11. PRD is Draft; owner roles below are inherited from the PRD, not assigned individuals. Planning resolves technical choices while recording externally blocked execution/acceptance. No credential belongs here. Source feature branch is 001-phase1-lead-foundation; Git branch was independently verified, but local Git does not establish remote/deploy access.

| ID | Status / unresolved decision | Owner role | Required gate/deadline and consequence |
|---|---|---|---|
| DEP-01 | PRD/MoSCoW/final metric sign-off pending | KEN Management / Product Owner | PRD target 2026-10-13; planning may proceed, no stakeholder approval claim |
| DEP-02 | Wireframes/route-content model, logo rights, exact tokens/fonts/visual approval not supplied | Designer / KEN / Content | Phase 1 target 2026-10-23; provisional choices support review, acceptance requires sign-off |
| DEP-03 | Native-reviewed ar/en Home/form/privacy/preparation copy absent; legal notice not approved | Content / Legal / KEN | Visible-copy review before Phase 1 acceptance; real intake requires approved notices; fixture notice expressly synthetic |
| DEP-04 | Cloudflare organization/Pages projects, D1 region/account tier/bindings, Turnstile hostname keys, Access policies and permissions not verified | Frontend / Functions / Engineering | Before hosted proof; missing actual D1/Turnstile/protected preview blocks Phase 1 hosted acceptance |
| DEP-05 | Canonical repository ownership/GitHub permissions and reviewed CI deployment jobs unverified | Product Owner / Engineering | Phase 1 CI/preview gate; Actions selected by current user instruction, not claimed organizationally reviewed |
| DEP-06 | Live email provider/sender/recipient/credentials TBD | Functions / Sales/Operations | Hosted labeled simulation is permitted Phase 1; not a Phase 1 live-email blocker. Finalize live setup Phase 2 target 2026-11-06; approved processing and actual delivery before launch |
| DEP-07 | Primary/backup operator and escalation recipient unassigned; provider access/MFA not demonstrated | Sales/Operations / Functions | Before Phase 1 retrieval/recovery/alert acceptance; no staff access or daily handoff claim until demonstrated |
| DEP-08 | Verified phone/WhatsApp/address/service-area facts absent | KEN / Sales / Content | Suppress unavailable preview links/facts; Phase 2 and production smoke require verified channels |
| DEP-09 | Licensed editorial hero, real project photos/captions/permission evidence absent | KEN / Designer / Content | Honest fallback Phase 1; Phase 2 content target 2026-11-06; public gallery requires ≥3 real approved projects/≥6 images |
| DEP-10 | Lawful basis, bilingual notices, D1 jurisdiction/processor/Functions/Turnstile/logging/staff/email transfers not approved | Legal / KEN / Functions | Begin feasibility Phase 1; no real customer data before clearance, PRD target 2026-11-28. D1 location hints cannot prove Saudi residency; incompatibility needs approved architecture change |
| DEP-11 | Lead/backup/history retention, encrypted export location, deletion/access/restore/RPO/RTO approval pending | Legal / Operations / Functions | Phase 1 feasibility/owner record; lifecycle policy and restore drill before launch. 12-month leads/30-day daily backup proposal is not adopted policy |
| DEP-12 | Profile/budgets agreement, real browser/device/participant access, monitoring channel and assigned QA staff not supplied | QA / Frontend / Functions / Product Owner | Agree planning defaults before measurement acceptance; demonstrate alerts and manual/usability matrix by Phase 1 gate; missing evidence blocks readiness |
| DEP-13 | Production domain/DNS/HTTPS, Search Console, separate production project/bindings, complete later P0 and launch approval absent | KEN / Engineering / SEO / QA | Later beta target 2026-12-04/public launch 2026-12-05; dates move if incomplete; production disabled Phase 1 |

## Concrete decisions versus approvals

Technical choices resolved: Router framework SSG, source models, schema/enums/bounds, atomic D1 persistence/idempotency/rate controls, hosted simulation and operator recovery, alert rules, proposed budgets/profile, Direct Upload via GitHub Actions, version baselines and local/remote procedures. These are ready to break into tasks.

External decisions cannot be inferred: permitted processor regions and D1 jurisdiction; real-data lawful basis/notice/retention; approved font/assets/company facts; actual provider roles/account tier/cost limits; named staff/access; real devices/testers; agreed measurement profile; monitoring recipient/channel; production domain and later email vendor. Every dependent task must carry the corresponding DEP ID and be blocked at its evidence gate if absent.

Account-level D1 size/query quotas, deployment/build quotas and monitoring availability must be checked against the actual chosen tier during provisioning. The low-volume design does not imply load capacity or paid features are purchased. Tier affects Time Travel history and operations. Staging base/hash/branch/custom host protection and explicit bindings must be checked, including the staging project's base production-environment configuration if used.

## Planning readiness

Constitution Check: PASS for design with no exception; no technical NEEDS CLARIFICATION remains. speckit-tasks may generate work now using plan/data/contracts/quality/operations. Access or approvals block their dependent hosted/acceptance tasks, not documentation generation. Phase 1 completion requires candidate checks, actual hosted D1/Turnstile, authorized recovery, visible native copy review and provisional design/content-model approval; pending items cannot be called accepted. Production remains separately blocked by all PRD release gates.

No application code, dependency install, remote migration, hosted preview, real-data processing, live email or public deployment was performed in this planning command. Preserve PRD/constitution/spec bytes and retain evidence of this check.
