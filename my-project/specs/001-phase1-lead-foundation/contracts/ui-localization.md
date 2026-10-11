# UI, Localization and Build Interface Contract

## Route and content manifest

| Page ID | Arabic | English | Phase 1 state |
|---|---|---|---|
| home | /ar/ | /en/ | Initial homepage |
| about | /ar/about | /en/about | Preparation |
| services | /ar/services | /en/services | Preparation; six choices on Home/Contact |
| projects | /ar/projects | /en/projects | Honest preparation; no fabricated evidence |
| why-ken | /ar/why-ken | /en/why-ken | Preparation |
| contact | /ar/contact | /en/contact | General/quotation prototype |
| privacy | /ar/privacy | /en/privacy | Explicit test notice until approved |

Root redirects to Arabic without geolocation. Language switching resolves page ID through paired manifest, preserving only validated type/service query context. Unsupported locale requests use Arabic 404 with English option; /en/unknown returns English 404, /ar/unknown Arabic 404. Documents set lang/dir at html level before hydration. Direct load and client navigation share labels/content/metadata.

Build interfaces: validate-content checks 100% dictionary/metadata/alt parity, IDs/media rights references and route pairs; SSG emits 14 localized documents; finalize-static flattens leaf HTML, preserves route data/hydration assets and generates static localized 404s/hosting directives; audit-build checks initial meaningful HTML, canonical/hreflang, URLs/status expectations, secret boundaries and compressed budgets. Missing required translation fails the build; unexpected runtime absence uses localized explanation/safe home, not raw keys.

## Safe quotation query

Allowed query keys: type=general|quotation and service=<one of six IDs>. Valid service preselects only with quotation context; missing/malformed/duplicate/overlong values are ignored safely without disabling the form. Unknown query keys are never copied by locale switching. No personal values, token or inquiry reference enters URLs. Valid choices remain editable/clearable. Canonicals exclude query parameters.

## Form state and focus

Idle → editing → validating → submitting → received or recoverable error/unknown outcome. Required labels, optional labels, help and notices exist in both languages. Submit is enabled only when client-required inputs are valid; touched/blur and input handling exposes corrections, and attempted submit focuses the first invalid field. Do not make correction guidance depend on a disabled button event. Server errors use a focusable summary plus associated field messages; visible aria-live feedback announces pending/error and durable confirmation. Inputs remain available on failure. Confirmation receives focus and shows a bidi-isolated reference, never raw personal data.

During submit disable repeated submit activation, not text readability. If a request times out, acknowledge that acceptance is unknown, retain the same identity/draft, refresh verification and retry; do not claim success. 409 offers an explicit new-submission action after explanation. Token refresh keeps lead identity. 429 displays localized cooldown based on Retry-After; 503 supports retry and only verified direct contact alternatives. Changed notice version requires renewed acknowledgement of the current notice. A successful completed form reset/new request gets a fresh identity.

Drafts live in current component/page memory only. Locale switch/reload does not promise draft persistence; warn of unsaved input before intentional navigation when needed, using localized accessible confirmation. Nothing is written to localStorage/sessionStorage or URLs. Pure page switching carries only safe service/type context. Privacy link may open in a clearly announced new tab so current draft survives notice review.

## Navigation, components and resilience

One six-item header/footer map plus separate privacy link; every preparation route exposes an on-site contact/quotation path. Mobile menu is a disclosure with aria-expanded/controls and Escape/focus restoration. Hidden links are not tabbable. If a modal is later used, focus containment and inert background become required. Route navigation moves focus predictably to main heading; visible skip link is first in keyboard order.

Use semantic buttons/links, associated labels and aria-describedby errors; phones/numbers/reference fragments use LTR/bdi inside RTL. Controls target ≥44px where practicable. Motion preference suppresses movement; content starts visible, images reserve dimensions and fallbacks retain text. No hover-only action or scroll hijacking. Without JavaScript, ordinary links and initial content work, while the form has a localized explanation rather than false working submission.

No phone/WhatsApp anchor exists until its number is approved. After verification, encode international tel/wa.me destinations and localized service copy, triggered only by explicit user action. Project/editorial images remain distinguishable; absent evidence has honest empty states. A simulation label belongs to stakeholder evidence/preview notice, never a claim that email reached an inbox.

## SEO/public projection

Every localized document has reviewed title/description, self-canonical and reciprocal language alternates, safe social metadata and meaningful H1. Preview origin is an actual deployment origin; no invented production URL or company facts. All preview states noindex; confidential materials additionally require access protection. Structured company data is emitted only from approved facts. Later production sitemap/robots includes completed approved routes and legal utilities; preparation states cannot pass launch gates.

## Deferred event schema

Reserve page_view, service_cta, whatsapp_click, phone_click, form_started, lead_submitted and form_error with only non-sensitive locale/page/service/category metadata. No collector or analytics script is enabled in Phase 1. Future lead_submitted requires durable API acceptance and client duplicate suppression; no reference, personal field, token, full URL or form text may be transmitted. D1 remains authoritative and missing session data means insufficient data.
