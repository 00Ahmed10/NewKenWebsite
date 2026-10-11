# Data Model and Migration Strategy

Planning design only. Canonical entities follow PRD §11.4 and spec FR-009–019. Public content remains typed source, not D1. Server/database fields are never public projections. All timestamps are server UTC ISO-8601 at the API boundary and epoch milliseconds in D1; UUIDs use crypto.randomUUID().

## Public source entities

| Entity | Fields and invariants |
|---|---|
| RoutePair/SitePage | Stable pageId, slug, locale, route, title, description, sections, publicationState=preparation/approved, seo, updatedAt; exactly one ar/en pair |
| Dictionary | Exact key parity for navigation/forms/errors/empty/loading/metadata/alt; build fails on absent or empty required translations |
| ServiceContext | Stable id from villa/school/administrative/restaurant/installation/maintenance; bilingual label, sortOrder, optional approved media; no detailed service claims needed here |
| MediaAsset | id, public derivative paths, width/height, altAr/altEn, kind=brand-editorial/ken-project, rightsStatus and build-only permission reference; public projection excludes internal permission evidence |
| SiteConfig | Locale labels/tokens, optional verified phone/WhatsApp/address/service-area/public SEO facts; omitted if unverified; no credentials |
| PrivacyNotice | Version, locale, text, status=fixture/approved and approval reference; one current version per environment, review evidence held outside public projection |
| Approval/Evidence | Owner role, status, required gate, approval reference/revision and test profile; not fabricated staff names or executed results |

Full Project and FAQ content arrives later: project approval/media/permission requirements and minimum gallery inventory remain unchanged. No user/account entity exists. Forms choose stable service IDs independent of translation text. Public projection validation rejects unapproved production records; internal rights references must not leak into bundles.

## Submission validation and canonicalization

All body keys are allowlisted; unknown keys, wrong types, arrays where scalars are required, malformed JSON and unsupported enum values are rejected. Body cap is 32,768 UTF-8 bytes, enforced while reading and regardless of Content-Length. Strings are NFC-normalized and trimmed at their ends. Text lengths count Unicode code points after normalization. Reject NUL and disallowed control characters; permit message newline/tab, normalize CRLF/CR to LF. Reject bidi override/control characters in human input rather than stripping hidden meaning. Render user content as text, never markup.

| Field | Required/type | Accepted bounds and normalization |
|---|---|---|
| idempotencyKey | Required UUID v4 string | Generated per intended submission; client retains through unknown/failure/retry; never stored raw server-side |
| locale | Required enum | ar/en only |
| type | Required enum | general/quotation |
| name | Required string | 2–100 code points; internal whitespace preserved |
| phone | Required string | Raw 3–64 code points; map Arabic/Persian digits, supported punctuation and whitespace; parse with SA national default or supplied international country code; library-valid E.164, ≤15 digits after +; discard raw form |
| message | Required string | 10–2,000 code points; normalized text including allowed line breaks |
| privacyAcknowledged | Required boolean | Literal true only; never coerced from strings |
| privacyNoticeVersion | Required string | 1–64 ASCII [A-Za-z0-9._-], must exactly match environment current notice |
| turnstileToken | Required string | 1–2,048 characters; verify only, never retain |
| email | Optional string/null | Null/omitted/blank becomes null; populated email ≤254 code points, valid address schema; trim, preserve local-part case, lowercase domain |
| city | Optional string/null | Null/omitted/blank becomes null; populated 1–100 code points |
| serviceId | Optional enum/null | Six stable IDs; optional in both modes; never infer from untrusted marketing text |
| propertyType | Optional quotation enum/null | villa/school/administrative/restaurant/other; labels explain that other covers additional building uses |
| floors | Optional quotation integer/null | 1–200; no numeric strings/float/coercion; unknown remains null |
| timeline | Optional quotation enum/null | planning/within_3_months/within_6_months/flexible |

Populated propertyType/floors/timeline in general mode are invalid; omitted/null passes. Switching mode clears building values with predictable UI feedback. These optional limits/enums are planning choices, not new business claims. Required city is expressly prohibited. Blank optional strings normalize to null. Client/server apply the same pure normalization functions, with server validation authoritative.

### Payload identity

Canonical lead content is a fixed-key-order serialization of locale, type, serviceId, name, phoneE164, email, city, message, propertyType, floors, timeline, privacyAcknowledged=true and privacyNoticeVersion. Every absent optional key is explicit null. It excludes idempotencyKey, turnstileToken, correlation ID, server timestamps and notification mode/status. Different locale or notice version is materially different lead content. Refreshed token and equivalent phone formatting are not.

- idempotency_key_hash: SHA-256(environment identity + delimiter + UUID key). Key is high-entropy, not derived from phone/name.
- payload_hash: HMAC-SHA-256(server payload secret, canonical lead bytes), preventing offline guessing from an unkeyed personal-data digest. Store hash_version. Old keys remain available for the lifetime of matching retained inquiries; verify original row using its version during rotation. Never log either hash or canonical payload.
- Lifetime: replay identity lasts as long as its retained inquiry. Do not silently expire a 24-hour key while retaining the lead. Real-data retention is unapproved, so no production duration is adopted. Preview synthetic cleanup ends that fixture identity; do not reuse purged fixture UUIDs.
- Client changes after an unknown outcome must not silently rotate the key: offer explicit new submission after explaining possible prior acceptance/conflict. Confirmation clears the completed draft; a new form action creates a new key. No browser persistent personal storage.

## D1 tables

### inquiries

| Column | Type / constraints |
|---|---|
| id | TEXT primary key UUID; also visitor referenceId |
| created_at | INTEGER NOT NULL server epoch ms |
| locale | TEXT NOT NULL CHECK ar/en |
| type | TEXT NOT NULL CHECK general/quotation |
| service_id | Nullable TEXT CHECK six IDs; static-source relationship, no dynamic service table |
| name | TEXT NOT NULL; validation bounds enforced by application and meaningful SQL checks |
| phone_e164 | TEXT NOT NULL; normalized only |
| email, city | Nullable TEXT |
| message | TEXT NOT NULL |
| property_type, floors, timeline | Nullable TEXT/INTEGER/TEXT, allowed enums/ranges and quotation-mode CHECK |
| consent_at | INTEGER NOT NULL server epoch ms; set on durable acceptance |
| privacy_version | TEXT NOT NULL current notice at acceptance |
| idempotency_key_hash | TEXT NOT NULL UNIQUE |
| payload_hash, hash_version | TEXT NOT NULL, INTEGER NOT NULL |
| status | TEXT NOT NULL DEFAULT received; later qualification workflow is deferred |
| test_record | INTEGER NOT NULL CHECK 0/1; assigned by server environment, never trusted from body |

Indexes: unique key hash; created_at for secure reconciliation/export; no phone/email search index initially. CHECK constraints supplement, not replace, typed/Unicode-aware server rules. consent_at records acknowledgement reception, not an asserted lawful basis. No raw IP, token, origin URL, secret or raw idempotency key is retained.

### notification_attempts

One inquiry has many attempt rows. Sequence one is created pending in the same acceptance batch. A pending row records recoverable work before external activity, not a claim of provider delivery.

| Column | Type / constraints |
|---|---|
| id | TEXT primary key UUID |
| inquiry_id | TEXT NOT NULL FK inquiries(id), deletion cascades only in authorized lifecycle tooling |
| attempt_number | INTEGER NOT NULL ≥1; UNIQUE(inquiry_id, attempt_number) |
| mode | TEXT NOT NULL CHECK simulation/live; live disabled in Phase 1 |
| provider | TEXT NOT NULL; simulation for Phase 1, approved identifier later |
| status | TEXT NOT NULL CHECK pending/running/simulated_success/provider_accepted/failed/escalated |
| created_at | INTEGER NOT NULL |
| started_at, finished_at | Nullable INTEGER |
| next_retry_at | Nullable INTEGER; eligibility, not a guaranteed scheduled execution time |
| lease_token, lease_expires_at | Nullable TEXT UUID / INTEGER; claim fencing, never logged |
| error_code | Nullable allowlisted category; no raw provider error/body/message |

Indexes: (status,next_retry_at), (inquiry_id,attempt_number). A current delivery summary is derived from the highest attempt_number, avoiding a second mutable status on the inquiry. Record attempt count from row count/number. Mode-specific terminal status must agree: simulated_success cannot mean provider acceptance. Retain failed attempt history; subsequent attempts create new rows, never erase prior outcome.

### rate_limit_buckets

| Column | Type / constraints |
|---|---|
| network_digest | TEXT keyed HMAC digest; IP not stored |
| window_kind | TEXT CHECK ten_minutes/day |
| window_start | INTEGER epoch ms |
| request_count | INTEGER NOT NULL; bounded atomic increment |
| expires_at | INTEGER NOT NULL |

Composite primary key (network_digest,window_kind,window_start). Index expires_at. Digest uses environment/day-derived rate secret and trusted network identity; rotation aligns with day boundary. Counter defaults: 10 per ten-minute fixed window and 50 per UTC day. Conditional UPSERT with RETURNING increments only below cap; no returned row means refusal. Claim both windows in a batch; any refusal yields no lead. A consumed shorter-window quota is not refunded if the other fails. Expired rows are ignored immediately and deleted by restricted cleanup, with a proposed maximum 48-hour operational cleanup window. Digests are pseudonymous network data and require privacy review; never log them. This is not a guaranteed abuse-proof capacity policy.

## Durable acceptance and concurrency

After successful validation/rate/Turnstile, one parameterized batch:

1. Insert proposed inquiry UUID using ON CONFLICT(idempotency_key_hash) DO NOTHING.
2. Insert pending sequence-one attempt by selecting only the proposed newly stored inquiry UUID, guarding uniqueness. A replay/conflict cannot create another sequence-one attempt or change notification state.
3. Select the authoritative inquiry by key hash and compare canonical payload using the stored hash version.

New row id matches proposed UUID: 201. Matching existing normalized payload: 200/original reference/time. Conflicting payload: 409/no new inquiry. Batch SQL failure: rollback and 503. A lost response or uncertain transport result is recoverable by same-key retry with fresh challenge. D1 remains authoritative. Concurrency tests must prove one inquiry/one initial attempt. Do not rely on a separate preliminary SELECT or local lock.

## Notification state transitions

pending → running under compare-and-swap lease → simulated_success (Phase 1) or provider_accepted (approved later live adapter). Failure/timeout → failed with safe category and next eligible retry. An expired running lease becomes failed/interrupted; fenced late results cannot overwrite a new owner. Each next eligible attempt is a new sequence row, claimed without creating an inquiry. After maximum three total attempts, transition the latest failed work to escalated; authorized deliberate recovery can add a separately audited attempt after correction. Retry delays are one minute after attempt one and five minutes after attempt two; manual replay runs when eligible, not as an assumed cron service.

A defensive reconciliation query left-joins inquiries with latest attempts; missing sequence-one status is pending/unattempted and can be repaired only by authorized tooling with uniqueness guard. Process death before/after claim and before outcome update is tested. Later live provider calls are at-least-once under crash uncertainty; use provider idempotency when available, and never claim exactly-once inbox delivery. No retry creates another inquiry.

## Migration and lifecycle strategy

Planned files: 0001_inquiries.sql, 0002_notification_attempts.sql, 0003_rate_limit_buckets.sql. Commit forward-only SQL and migrate fresh and prior-schema local databases in tests, including indexes/FKs/CHECKs. Record migration ordering and worker compatibility. D1 migrations tracking remains provider-managed; no hand-edited schema outside migrations.

Preview remote migrations require explicit target ID/name, serialized reviewed deployment, synthetic fixtures and account privileges. Do not let every PR alter a shared schema automatically. Before an approved remote change record a Time Travel bookmark and feasible encrypted export procedure; destructive changes require approved lifecycle review. Prefer expand/contract so the previous app build works after migration; rollback app without deleting leads or automatically reversing SQL. A restore is an incident action, not routine app rollback.

D1 has provider-managed encryption, but raw SQL export is plaintext unless the approved tooling encrypts it. Time Travel rollback overwrites state and can remove newly accepted records: rehearsal occurs in a separate synthetic database, and real incident restoration requires outage/reconciliation controls. Seven-day free/thirty-day paid history is not the proposed independent daily restricted encrypted backup with 30-day retention. Production storage geography, 12-month lead proposal, backups, deletion/export and history purge effects remain DEP-10/11 decisions. Preview cleanup removes synthetic inquiry and linked attempts, expires rate rows and keeps only non-sensitive pass/fail evidence; capture approval of any needed evidence retention before operation.
