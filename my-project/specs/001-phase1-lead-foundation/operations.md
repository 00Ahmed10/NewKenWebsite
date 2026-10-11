# Phase 1 Operations and Recovery Runbook Design

This is a procedure to implement and demonstrate, not evidence of deployed tooling or named staff. KEN Sales/Operations must assign a primary and backup authorized operator plus escalation recipient before acceptance (DEP-07). Use provider organization roles, least privilege and MFA; no public lead-read/retry/admin endpoint or visitor authentication. Supported provider roles may be broader than per-table permissions: validate actual role capability and restrict project/database/token scope as far as available; do not claim unsupported fine-grained access.

## Notification simulation and recovery

Hosted Pages Function commits the inquiry and sequence-one pending row together. Its best-effort waitUntil dispatcher claims the row and records mode=simulation plus simulated_success or safe failure/timeout category. The simulator never calls an email provider or suggests inbox delivery. Fault mode is set only through restricted preview configuration/deployment or authorized operational tooling, not public query/body/header values. Production configuration must reject simulation as a launch-ready notification mode.

The restricted CLI connects to explicitly selected preview D1 through provider-authenticated access. It must assert expected account/database/environment and synthetic-only mode before mutations, refuse production target by default and print references/counts/status only. No personal data in shell arguments/history/stdout/CI logs. Authorized detailed retrieval requires a deliberate reference selection and a private secure output destination; never dump leads into public report files. Default reconciliation does not select personal fields. Remote provider roles/access failures are tested; unauthenticated execution is denied.

1. Reconcile every business day at a fixed locally documented time (proposal 09:00 Asia/Riyadh); backup runs if primary is unavailable. Review new accepted totals and latest notification state, including inquiries with no attempt via left join, pending, failed, stale running leases and escalated work. Hand off every affected inquiry securely within one business day; record safe reconciliation timestamp/counts/reference evidence.
2. Repair an anomalous missing initial pending row with a unique guarded insertion. Do not recreate the inquiry.
3. Claim one eligible pending/retry row using compare-and-swap and a 120-second lease/fencing UUID. Persist running state before invoking the adapter; competing callers cannot claim the same attempt. A retry atomically creates/claims the next uniquely numbered attempt only if latest status is failed and due.
4. Run the controlled adapter; record terminal success/failure, times and allowlisted category with the same lease fence. Expired claims are marked interrupted and recovered; late owners cannot overwrite new work. Initial failure permits retry after 1 minute, second after 5 minutes, third escalates. These are earliest eligibility times for operator replay, not promised automatic scheduling.
5. After correction, an explicitly authorized recovery attempt can proceed with new sequence/evidence; no retry inserts another inquiry. Record simulated_success distinctly from future live provider_accepted. A provider accepting a message does not prove inbox receipt; actual recipient match is a later acceptance test.

Pages Functions have no assumed scheduled trigger. Phase 1 daily named-staff reconciliation/replay is the approved equivalent recovery mechanism. Later automated Worker/queue/scheduler/provider architecture needs a separate recorded decision. Live retries may deliver more than once if a provider succeeded before a crash; evaluate provider idempotency and reconciliation before Phase 2 production delivery. Exactly one stored inquiry remains mandatory.

## Failure and alert demonstration

Safe request log fields: server correlation UUID, timestamp, route category, response status, duration, validation category and notification category/mode. Exclude personal fields/messages, raw IP/digests, payload/key hashes, tokens, secrets, full URL/query and provider body. Logging wrappers must prohibit accidentally serializing Request/Error objects. Account for Cloudflare/provider automatic logs and access audit retention in privacy review.

Alert rules are planning defaults to be configured with approved recipients:

- API 5xx >1% of API requests in a rolling 15-minute window. Do not quietly introduce a minimum-request count that changes this requirement; include denominator/sample size in alert, and identify deliberate fault-test windows separately.
- Sustained notification failure: any latest failed/pending/stale-running record remains recoverable without success for ≥15 minutes, or three consecutive adapter failures within 15 minutes. Alert once per incident with counts/oldest age/references only, repeat/escalate after 60 minutes or three total failed attempts. Notify assigned primary/backup, then KEN Operations lead; identities/channels are external DEP-07/12 gates.
- Daily reconciliation missed its scheduled business-day window: notify backup and escalate before the one-business-day visibility requirement is breached.

Implement read-only safe summary checks and deterministic threshold tests. Hosted fault exercise proves durable failures reach summary/alert routing through the chosen operational mechanism; local simulation alone cannot count as monitored hosted recovery evidence. Monitoring provider/channel/permissions must be recorded before passing this gate. No new public counts/lead-status endpoint is needed. Production alerts later require provider integration/owner confirmation and no raw data in notifications.

## Environment and deployment separation

Use separate Direct Upload Pages projects for protected Phase 1 staging and later production for a strong account/configuration boundary. Within each Pages project explicitly declare preview/production bindings where used; the staging project's base deployment, if created, must still bind staging DB and simulation settings. Do not confuse a project's production branch name with permission to capture real customer data. Protect/deny all base/hash/branch/custom aliases; noindex is not access control. Turnstile hostname allowlists cover the actual approved staging domain; test dynamic preview hosts deliberately rather than using wildcard trust. Real-data intake stays disabled until legal/domain/content/operational gates close.

Trusted candidate deploys include SHA/environment/URL and reviewed migration versions. CI serializes migration/deploy work; a branch cannot alter shared D1 unreviewed. A prior compatible application deployment is the preview rollback target. Demonstrate rollback while verifying pre-existing synthetic references remain retrievable and pending work recoverable. Do not reverse SQL/drop tables as app rollback. If migration incompatibility arises, prefer a forward repair; incident restore needs authorized outage/reconciliation procedure and can lose recent writes.

## Data lifecycle, backup and incident readiness

Phase 1 uses deliberately synthetic fixture contacts/message data only, in protected previews. Testers still supply network metadata to providers; synthetic lead fields do not eliminate processor privacy review. Propose fixture deletion after evidence capture, at most seven days, by assigned operator; record the agreed test-data policy before hosted testing. Purge inquiry/linked attempt rows through an explicitly scoped authorized tool, expire rate buckets and retain only non-sensitive private evidence. Do not remove real records using fixture flags supplied by clients.

Production 12-month lead retention and daily encrypted exports with 30-day backup retention remain unapproved proposals. D1 Time Travel free/paid history and export features must be mapped to deletion obligations, backup locations/encryption keys/access and recovery objectives. A SQL export is sensitive plaintext until approved encryption protects it. No cloud backup bucket or email processor is assumed approved merely because Cloudflare is selected.

Before launch: Legal/KEN approve lawful basis, notices, transfer/processor regions and lifecycle; Operations approves secure retrieval/export/deletion, daily failure review, two staff access and encrypted restricted backups; Engineering rehearses restore in a separate synthetic database and compatible rollback. Document incident contacts, recovery point/time objectives and reconciliation of writes during restore. These are later blockers, not current pass claims.

## Phase 1 evidence pack

Record hosted URL/SHA/schema version; restricted access and bindings evidence; actual D1 inquiry reference matched in a fresh operator session; labeled simulator outcome; failure/interruption → reconciliation → authorized replay; alert route/threshold demonstration; duplicate/conflict counts; preview rollback retaining accepted reference; synthetic cleanup receipt. Exclude raw personal data, secrets, complete lead dumps and provider credentials. Link later approval dependencies without asserting live email/production readiness.
