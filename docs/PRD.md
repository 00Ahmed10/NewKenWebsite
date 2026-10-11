# KEN Elevators — Premium Corporate Website v1.0 — Product Requirements Document

## 1. Project Identity

| Field | Value |
|---|---|
| Project Name | KEN Elevators — Premium Corporate Website v1.0 |
| Project ID | PRD-001 |
| Version | v1.0 |
| Status | Draft — pending stakeholder approval |
| Priority | High |
| Created Date | 2026-10-10 |
| Last Updated | 2026-10-10 |
| Owner / Product Manager | KEN Elevators Management |
| Team Members / Roles | Product Owner; UI/UX Designer; React/TypeScript Frontend Developer; Cloudflare Functions Developer; Arabic/English Content Editor; SEO Specialist; QA Engineer (individual assignments [TBD]) |
| Technology Stack | React, TypeScript, Tailwind CSS, Vite, build-time prerendering, Cloudflare Pages, Cloudflare Pages Functions, Cloudflare D1, Cloudflare Turnstile |
| Repository | [TBD] |
| Git Branch Prefix | `NNN-feature-name` |
| PRD File Path | `docs/PRD.md` |
| Initial Market | Tabuk, Saudi Arabia; inquiries from elsewhere in Saudi Arabia subject to confirmed service coverage |
| Languages | Arabic (default, RTL) and English (LTR) |
| Target Public Launch | 2026-12-05 (proposed; subject to approval and asset readiness) |

## 2. Problem & Purpose

### Problem Statement
KEN Elevators (شركة كين للمصاعد), based in Tabuk, requires a credible premium digital presence through which prospective customers can evaluate elevator solutions, review authentic work, and contact the company without friction. In the absence of a polished, bilingual, conversion-focused corporate website, customers may have difficulty finding clear service information or establishing trust before requesting a quotation.

### Project Purpose
Create KEN Elevators' first official premium corporate website, with the visual quality of an international elevator brand, while remaining authentically grounded in KEN's identity and Saudi market. The site must communicate in Arabic by default, support English completely, and turn interest into qualified inquiries via quotation forms, WhatsApp, and telephone.

### Business Value
- Establish a consistent, professional brand presence for residential, educational, administrative, and hospitality-sector buyers.
- Reduce the effort required to discover services, review project evidence, and request quotations.
- Generate measurable qualified leads and route them reliably to KEN staff.
- Make content discoverable in Arabic and English search results, especially for customers researching elevator services in Tabuk.

### Opportunity
A mobile-first, image-led experience can differentiate KEN in a high-consideration category where visual trust, installation quality, post-installation maintenance, and responsive communication materially influence purchasing decisions. Claims about certifications, completed projects, years of experience, and service coverage must be substantiated before publication.

## 3. Goals & Objectives

### Primary Goal
Launch a bilingual, premium corporate website by **2026-12-05** that enables visitors to understand KEN's elevator offerings and submit a successfully stored quotation or general inquiry, or initiate direct contact via verified WhatsApp and phone links.

### Objectives
1. Publish all six primary pages, their Arabic and English equivalents, and accurate bilingual service content.
2. Showcase attractive, properly licensed elevator imagery and KEN's verified project photography without misrepresenting stock imagery as completed KEN projects.
3. Support reliable quotation and inquiry submissions with validation, anti-spam protection, durable storage, and operational notification.
4. Deliver an accessible, responsive navy-and-gold visual system with restrained cinematic motion and a reduced-motion fallback.
5. Meet the technical performance, SEO, lead-generation, and reliability targets defined in Section 12.

### Success Definition
A release is successful when all P0 acceptance criteria are met; KEN approves the content and brand presentation; both languages function on mobile and desktop; production leads can be delivered and retrieved; live contact routes are verified; and all launch-blocking security, accessibility, and SEO defects are closed.

### Non-Goals
A customer portal, user login, internal CRM/dashboard, online ordering or payments, native applications, and AI chatbot are not part of v1.0. The website is a marketing and lead-generation property, not an elevator configurator or maintenance management system.

## 4. Scope

### In Scope — v1.0
- **Six primary pages:** Home, About Us, Services, Projects, Why Choose Us, Contact Us.
- **Localized routes:** `/ar/` and `/en/`, with matching versions of `/about`, `/services`, `/projects`, `/why-ken`, and `/contact`; `/` defaults to Arabic.
- **Legal utility content:** linked Arabic and English privacy notices, outside the six primary navigation pages.
- **Service coverage in content:** villa elevators, school elevators, administrative-building elevators, restaurant elevators, elevator installation, and maintenance.
- Responsive header/navigation, footer, breadcrumbs where appropriate, accessible language switcher, and clear primary CTAs.
- Elegant navy-blue and gold visual identity, cinematic hero treatment, scroll reveals, hover interactions, and motion-safe behavior.
- Curated verified projects gallery, image optimization, descriptive alt text, and sensible empty-state behavior in staging.
- General inquiry and quotation request flows, server-side validation, spam defense, durable lead persistence, and operational email notification.
- WhatsApp deep links, telephone click-to-call actions, and verified company contact details.
- Build-time rendered crawlable content, localized metadata, canonical tags, `hreflang`, sitemap, robots directives, structured data where verifiable, and deployment to Cloudflare Pages.
- Basic security, testing, accessibility QA, error monitoring, and production handover.

### Out of Scope — v1.0
- Authenticated accounts, customer dashboards, admin CMS, ecommerce, payments, native iOS/Android apps, and AI chatbot.
- Self-service maintenance ticket tracking, live technician dispatch, automated instant pricing, and third-party CRM integration.
- Claims of nationwide operations, regulatory approvals, certifications, or completed project counts unless verified by KEN.

### Assumptions
- Arabic is the default for all first-time visits to `/`; English is a deliberate user choice, not an IP-based redirect.
- KEN will approve Arabic and English marketing copy, supply authentic projects and contact information, and designate a lead recipient.
- A managed transactional email provider will be selected and configured before launch; provider name remains [TBD].
- The six primary pages are marketing page types; service categories can be anchored sections on the Services page without increasing the primary navigation count.
- No user authentication is required; public visitors can submit inquiries without accounts.

### Constraints
- Technology: React + TypeScript + Tailwind CSS; compatible with Cloudflare Pages deployment.
- Arabic must render in RTL, English in LTR, with equivalent functionality and complete translations.
- The visual direction must be luxurious but not sacrifice contrast, keyboard usability, page speed, or form completion.
- Do not publish fabricated reviews, project imagery, awards, licenses, addresses, phone numbers, or opening hours.
- Personal information must be collected minimally and managed in line with applicable Saudi data-protection requirements, subject to legal approval.

### Dependencies
- **Launch blockers:** approved company logo and brand assets; verified office/contact phone, WhatsApp number, inquiry notification address, address/service-area wording, legal/privacy text, company project photographs and permissions, production domain, and transactional email credentials — all [TBD].
- Cloudflare account and Pages/D1/Turnstile access; DNS/domain configuration; source-code repository.
- Arabic/English editorial review, image usage rights, stakeholder approval of design and final content.
- Availability of a person responsible for responding to leads and checking notification failures.

## 5. Users & Personas

### Primary Users
Villa owners and homeowners; property developers; school administrators; owners/managers of administrative buildings and restaurants; facility managers and property maintenance decision-makers in Tabuk and other confirmed KEN service areas.

### Secondary Users
KEN sales and operations staff receiving leads, prospective commercial partners researching capabilities, and English-speaking decision-makers in the Saudi market.

### Persona A — Residential Buyer
- **Name:** Villa Owner (representative persona)
- **Role:** Homeowner researching a villa elevator
- **Goal:** Understand options, see finish-quality examples, and request a tailored quotation quickly.
- **Pain Point:** Unclear product suitability, unreliable visual examples, and too many steps to reach a supplier.
- **Tech Level:** Low–Medium; predominantly mobile
- **Frequency:** Infrequent, high-intent research over several visits
- **Success:** Identifies the villa offering and completes a request with basic building requirements in under three minutes.

### Persona B — Commercial / Institutional Buyer
- **Name:** Facilities Decision-Maker (representative persona)
- **Role:** School, restaurant, office, or building operator
- **Goal:** Evaluate suitability, installation capability, maintenance support, and the legitimacy of prior work.
- **Pain Point:** Generic supplier pages without credible evidence or a clear contact pathway.
- **Tech Level:** Medium
- **Frequency:** Periodic during procurement or maintenance sourcing
- **Success:** Reviews relevant services and projects, then sends a traceable request or contacts the company directly.

### Persona C — KEN Lead Recipient
- **Name:** KEN Sales / Operations Representative (role, individual [TBD])
- **Role:** Handles inbound contact and quotations
- **Goal:** Receive complete, actionable inquiries with contact details and service context.
- **Pain Point:** Missed messages, spam, and leads lacking the information necessary for follow-up.
- **Tech Level:** Low–Medium
- **Frequency:** Daily once the site launches
- **Success:** Receives new-lead notifications and can retrieve submissions securely if email delivery fails.

## 6. MoSCoW Feature Prioritization

### Must Have — P0

| ID | Feature | Status | Description | Assigned To | Sprint |
|---|---|---|---|---|---|
| P0-F001 | Bilingual six-page site and navigation | TODO | Complete Arabic RTL / English LTR routes, shared navigation, content and language switcher | Frontend + Content | 1–2 |
| P0-F002 | Premium responsive design and core motion | TODO | Navy/gold visual system, imagery, mobile-first layouts, accessible cinematic hero and restrained animations | Design + Frontend | 1–3 |
| P0-F003 | Six service categories | TODO | Discover and explore villa, school, administrative, restaurant, installation and maintenance offerings | Frontend + Content | 2 |
| P0-F004 | Verified projects gallery | TODO | Image-led portfolio with approved, genuine project content and optimized imagery | Frontend + Content | 2 |
| P0-F005 | Contact and quotation forms | TODO | Validated bilingual forms backed by secure server endpoint, storage and notification | Frontend + Functions | 1–2 |
| P0-F006 | WhatsApp, phone and contact conversion | TODO | Contextual working direct-contact actions, prefilled quotation context, accessible contact information | Frontend + Content | 2 |
| P0-F007 | SEO, performance, security and production launch | TODO | Crawlable localized pages, metadata, Core Web Vitals targets, deployment, testing and monitoring | Frontend + QA + SEO | 1–4 |

### Should Have — P1

| ID | Feature | Status | Description | Assigned To | Sprint |
|---|---|---|---|---|---|
| P1-F001 | Gallery filtering and image lightbox | TODO | Filter by relevant category and browse project photographs accessibly | Frontend | 3 |
| P1-F002 | Service FAQs | TODO | Approved bilingual answers to common elevator and maintenance questions | Content + Frontend | 3 |
| P1-F003 | Enhanced cinematic interactions | TODO | Optional depth effects, transitions and richer scroll storytelling without harming usability | Design + Frontend | 3 |
| P1-F004 | Privacy-conscious conversion analytics | TODO | Track page visits and lead conversion events without collecting form PII in analytics | SEO + Frontend | 3–4 |

### Could Have — P2

| ID | Feature | Status | Description | Assigned To | Sprint |
|---|---|---|---|---|---|
| P2-F001 | Downloadable company brochure | TODO | Approved bilingual corporate PDF for procurement teams | Content + Design | Post-launch |
| P2-F002 | Verified customer testimonials | TODO | Written testimonials with source consent and approval | Content | Post-launch |
| P2-F003 | Service-selection guide | TODO | Lightweight informational comparison for visitors choosing a service | Product + Frontend | Post-launch |

### Won't Have — P3

| ID | Feature | Status | Description | Assigned To | Sprint |
|---|---|---|---|---|---|
| P3-F001 | Customer authentication and accounts | TODO | No visitor login in v1.0 | Not assigned | Deferred |
| P3-F002 | Admin dashboard / CMS | TODO | Leads managed through restricted backend access and editorial updates through code | Not assigned | Deferred |
| P3-F003 | Ecommerce and online payments | TODO | Pricing and payment transactions remain offline | Not assigned | Deferred |
| P3-F004 | Native mobile application | TODO | Mobile-first website instead | Not assigned | Deferred |
| P3-F005 | AI chatbot and automated quoting | TODO | Human-led inquiries and manual quotations instead | Not assigned | Deferred |

## 7. Functional Requirements

**Global interaction contract:** Every user-facing asynchronous action has a visible pending state; invalid input has an inline, accessible correction message; recoverable errors preserve user-entered data; successful actions receive explicit confirmation. Arabic strings, layout direction, and focus order must be reviewed independently from English. Public GET content endpoints may be consumed at build time: the website must not depend on an extra network request to show its initial prerendered content.

### P0-F001 — Bilingual Six-Page Site and Navigation
- **Description:** Deliver the six primary marketing pages with identical capabilities in Arabic and English. The Arabic locale is the default and uses `lang="ar" dir="rtl"`; English uses `lang="en" dir="ltr"`. Shared content/navigation components must support both directions without duplicated page logic.
- **User Story:** As a Saudi visitor or English-speaking buyer, the visitor wants to browse KEN's content in a preferred language and switch languages without losing the current page.
- **Trigger:** Visit `/`, a localized deep link, a navigation item, or the language switcher.
- **Preconditions:** A supported route and built-in localized content are available; no account is required.
- **Postconditions:** The target page displays in the requested locale; navigation landmarks, document metadata, and text direction match the locale.
- **Main Flow:**
  1. Visitor opens `/`; the host sends them to `/ar/` without location-based language detection.
  2. The Arabic homepage displays the primary navigation: Home, About, Services, Projects, Why Choose Us, Contact.
  3. Visitor opens a page via header, footer, or CTA; the corresponding localized route loads directly and on refresh.
  4. Visitor selects English; the corresponding `/en/<same-route>` page renders LTR, with localized navigation and content.
  5. Visitor navigates normally and can return to Arabic with the same page context.
- **Alternate Flows:** Unsupported locale or nonexistent page shows a translated 404 with safe navigation home; if a paired translation is unexpectedly absent, route to that language's homepage with a visible explanation rather than showing untranslated strings.
- **Acceptance Criteria:**
  - [ ] All six primary pages are accessible directly at both `/ar/*` and `/en/*` and survive full-page refresh.
  - [ ] `/` resolves to Arabic; no forced geolocation redirect overrides a selected English route.
  - [ ] Language switching preserves the current page when a matching route exists.
  - [ ] HTML `lang`, `dir`, titles, navigation labels, form copy, alt text and validation messages match the locale.
  - [ ] Mobile menu opens and closes with keyboard, pointer and touch; `Escape` closes it and focus returns to the trigger.
  - [ ] Loading, missing-content and 404 states are visibly localized; no raw translation keys are exposed.

### P0-F002 — Premium Responsive Design and Core Motion
- **Description:** Establish a sophisticated dark navy, brushed-gold and warm-neutral design system with a cinematic elevator imagery hero, strong typographic hierarchy, responsive cards, discreet motion, and a premium but trustworthy tone. Final hex colors and Arabic/Latin font families require visual sign-off, not assumptions about existing KEN brand guidelines.
- **User Story:** As a prospective buyer, the visitor wants a polished visual experience that inspires confidence and is equally usable on a phone or desktop.
- **Trigger:** Visit any site page, scroll, hover, focus, or resize the viewport.
- **Preconditions:** Approved image rights and design assets are available, with responsive image alternatives.
- **Postconditions:** Content remains readable and CTAs discoverable at all supported widths; motion never blocks information or interactions.
- **Main Flow:**
  1. Homepage immediately displays a properly optimized elevator hero with legible headline and quotation CTA.
  2. Visitor scrolls through service cards, differentiators, projects preview and contact CTA.
  3. Nonessential sections reveal subtly when in view; interactions show clear hover and focus feedback.
  4. Layout adapts to tablet/mobile with accessible text size, touch targets and menu.
  5. Users requesting reduced motion receive static or minimal transitions with no content loss.
- **Alternate Flows:** Slow connection loads a poster/still image and critical typography before nonessential motion; image failure shows a neutral branded fallback and meaningful alt text; unsupported motion APIs leave content visible.
- **Acceptance Criteria:**
  - [ ] Visual tokens and reusable header, footer, hero, button, card, form, section and modal components are documented.
  - [ ] Layouts tested at 360, 390, 768, 1024 and 1440 CSS-pixel widths without horizontal overflow or clipped RTL text.
  - [ ] Brand colors meet WCAG 2.1 AA text contrast; gold never becomes low-contrast body text on pale backgrounds.
  - [ ] Main CTA remains usable without motion or hover and touch targets are at least 44 by 44 CSS pixels where practicable.
  - [ ] `prefers-reduced-motion: reduce` suppresses parallax, lengthy movement and autoplay-style effects.
  - [ ] Primary content is visible if JavaScript animation initialization fails; nonessential assets do not block the hero.

### P0-F003 — Six Elevator Service Categories
- **Description:** The Services page provides six distinct, approved offerings: villas, schools, administrative buildings, restaurants, installation and maintenance. Each has a title, introduction, appropriate image, typical use cases, a set of benefits subject to verification, and a quotation CTA.
- **User Story:** As a homeowner or facilities manager, the visitor wants to identify the most relevant elevator solution and start a request with that service preselected.
- **Trigger:** Select Services from navigation, open a service card, or follow a homepage service CTA.
- **Preconditions:** Editorial content exists in both languages; claims about features, safety and maintenance obligations are approved.
- **Postconditions:** Visitor sees the chosen service section and can open a quotation request carrying the correct service identifier.
- **Main Flow:**
  1. Visitor opens `/ar/services` or `/en/services`.
  2. A six-item service overview displays localized category names and images.
  3. Visitor selects a category; the relevant detail section is focused or scrolled into view via a shareable anchor.
  4. Visitor reads the category overview and follows `Request a Quotation`.
  5. Contact page opens with inquiry type `quotation` and selected service populated but editable.
- **Alternate Flows:** Unknown service slug or malformed query is ignored safely and the service selector remains unselected; unavailable image falls back without hiding service details.
- **Acceptance Criteria:**
  - [ ] Exactly the six stated service categories are represented in both languages, with unique identifiers and useful descriptions.
  - [ ] Service sections are discoverable from both the Services page and applicable homepage CTAs.
  - [ ] Service CTA preselects the correct type on the quote form and does not prevent manual changes.
  - [ ] Any feature, installation capability, certification or coverage claim is verified before publication.
  - [ ] Deep links to service anchors work on direct navigation and keyboard focus is managed appropriately.
  - [ ] Content is readable before images and optional enhancements load.

### P0-F004 — Verified Projects Gallery
- **Description:** Present KEN's approved completed-project photography with project name or anonymized label, relevant service category, short scope description, and image credits/permissions as necessary. The primary gallery must not portray licensed stock images as real KEN jobs.
- **User Story:** As a buyer assessing supplier credibility, the visitor wants to inspect genuine examples of completed elevator work.
- **Trigger:** Navigate to Projects or choose `View Projects` from a related service.
- **Preconditions:** KEN has approved image use, supplied captions/categories and confirmed the project may be represented publicly.
- **Postconditions:** Visitor can view projects, understand their relevance, and move toward the appropriate service or contact CTA.
- **Main Flow:**
  1. Visitor opens the Projects page.
  2. A curated grid of project cards appears with optimized cover images and short factual captions.
  3. Visitor opens a project card or scrolls its images/summary.
  4. Visitor follows a category link or contact CTA after reviewing the project.
- **Alternate Flows:** While authentic assets are being prepared, staging shows an explicit editorial empty state; the public launch is blocked if minimum approved gallery content has not been supplied. Broken images show placeholders and retain captions. No fabricated projects are inserted.
- **Acceptance Criteria:**
  - [ ] The initial public gallery contains at least three approved, real KEN projects and at least six approved images (content dependency, not a claim of existing inventory).
  - [ ] Every public project includes a verifiable internal content reference, approved bilingual caption and at least one appropriate image.
  - [ ] Image assets use responsive dimensions, modern formats where supported, lazy loading below the fold, and accessible text alternatives.
  - [ ] Cards and related CTAs work by keyboard and touch and are fully usable without P1 filtering or lightbox.
  - [ ] Missing assets have safe fallbacks; staging empty states are explicit and cannot be mistaken for customer proof.

### P0-F005 — Working Contact and Quotation Forms
- **Description:** Provide a general inquiry form and a quotation mode through the Contact page. Both submit to a protected Cloudflare Pages Function, validate server-side, verify Turnstile, durably store the inquiry in D1, and attempt notification to KEN's verified inbox. The notification mechanism must support recovery when email delivery fails.
- **User Story:** As a prospective customer, the visitor wants to send a clear request and receive confirmation without creating an account; as a KEN representative, the recipient wants actionable and retrievable lead details.
- **Trigger:** Open the Contact form, choose inquiry/quotation, and submit.
- **Preconditions:** The inquiry API, D1 binding, anti-spam verification and operational notification recipient are configured; approved privacy notice is accessible.
- **Postconditions:** An accepted submission is stored with a unique ID and timestamp; visitor receives a localized success message; notification is queued for retry or marked for operational follow-up if the provider fails.
- **Main Flow:**
  1. Visitor opens `/ar/contact` or `/en/contact`, optionally with `type=quotation&service=<service-id>`.
  2. Visitor supplies name (2–100 characters), contact phone (normalized to valid E.164 format), optional email, inquiry type, optional service and city, message (10–2,000 characters), and explicit mandatory privacy acknowledgement.
  3. Quotation mode also displays relevant optional building information (property type, number of floors if known, and desired timeline); no numeric estimate is promised.
  4. Client displays inline field errors and enables submit only after required inputs are valid; the button enters a pending state on submit.
  5. Server repeats validation, verifies anti-spam token, checks rate limits/idempotency, and stores the lead in D1 before returning success.
  6. Server triggers notification delivery to an approved recipient. Email failure must not erase the stored inquiry; a retry or operator recovery path is required.
  7. Visitor receives a localized success confirmation with reference ID and no sensitive values in the URL.
- **Alternate Flows:** Invalid phone/email/message produces field-specific errors; network outage preserves the draft for retry; expired Turnstile token requests refreshed verification; duplicate submission using the same idempotency key returns the existing result; rate limit returns localized guidance; server storage failure returns an error rather than false success.
- **Acceptance Criteria:**
  - [ ] Both general and quotation modes work in Arabic and English and can be opened directly from service CTAs.
  - [ ] Required and optional fields are clearly marked; validation is consistent in browser and backend with no raw exception text shown to users.
  - [ ] Valid submissions return a persistent, unique inquiry ID; data remains queryable by authorized operations after notification failure.
  - [ ] A stored lead produces a verifiable notification attempt and recoverable failure status; lead recipient and escalation procedure are tested.
  - [ ] Duplicate POST retry with identical idempotency key never creates a second inquiry; conflicting payload/key returns a conflict error.
  - [ ] Invalid, spam, oversized, or rate-limited requests cannot insert a lead; no secrets or personal data are exposed in browser bundles or analytics.
  - [ ] User-facing states include pending, inline validation, transport failure, server error, retry and success; input is retained on recoverable failure.
  - [ ] Test submissions are verified end-to-end in production before public launch, including D1 storage and email failure recovery.

### P0-F006 — WhatsApp, Phone and Contact Conversion
- **Description:** Provide prominent and contextual WhatsApp, telephone and quotation pathways in hero, services, project sections and footer, using only verified KEN contact details.
- **User Story:** As a high-intent visitor, the user wants to contact KEN immediately through an available channel with as little typing as possible.
- **Trigger:** Tap or click a `WhatsApp`, `Call`, `Contact`, or `Request Quote` CTA.
- **Preconditions:** Verified production phone and WhatsApp numbers are published by the owner; contact URLs are correctly encoded.
- **Postconditions:** The device offers the correct call or WhatsApp application experience, or the localized contact page loads with appropriate context.
- **Main Flow:**
  1. Visitor encounters contact CTAs on a relevant page.
  2. Visitor selects WhatsApp; a `https://wa.me/<verified-number>` link opens with an optional localized, service-aware prefilled message.
  3. Alternatively, visitor selects phone; a `tel:` URI invokes the device dialer.
  4. If the visitor prefers not to leave the website, `Request Quote` opens the on-site form.
- **Alternate Flows:** A browser without WhatsApp support still offers phone and web form options; if a contact number has not been verified during staging, the related CTA is disabled or hidden rather than linked to an invented number.
- **Acceptance Criteria:**
  - [ ] Every live WhatsApp/phone link uses verified digits in international format and has a descriptive accessible name.
  - [ ] Prefilled WhatsApp copy is percent-encoded and uses the correct language and service context.
  - [ ] CTA destinations are tested on representative iOS/Android and desktop browsers.
  - [ ] Every primary page has a readily identifiable path to quotation/contact.
  - [ ] No test or placeholder numbers ship to production; unavailable direct channels do not break the working form.

### P0-F007 — SEO, Performance, Security and Production Launch
- **Description:** Ship crawlable localized pages, predictable routes, comprehensive technical SEO, secure backend boundaries, fast initial render and a repeatable Cloudflare Pages deployment.
- **User Story:** As a searching customer, the visitor wants to discover relevant KEN service content in search engines and load the website rapidly; as KEN, the company needs stable production delivery and secure handling of leads.
- **Trigger:** Search engine crawl, direct request, new code deployment, or form/API request.
- **Preconditions:** Production domain, bilingual content, Pages project and secrets, verified organization fields and deployment permissions are available.
- **Postconditions:** Visitors and crawlers receive appropriate localized HTML and metadata; production deploys are traceable; security checks protect lead data.
- **Main Flow:**
  1. Build emits prerendered HTML for both locales of the six primary pages plus legal utility content, with canonical and `hreflang` alternates.
  2. A visitor opens a localized deep link and receives meaningful HTML before client hydration.
  3. The page loads critical fonts and responsive hero imagery efficiently; nonessential gallery/motion scripts load later.
  4. The site serves a sitemap and robots instructions; applicable structured data includes only validated company facts.
  5. CI runs lint, types, tests and build; a reviewed deployment publishes to Cloudflare Pages and smoke tests validate critical journeys.
- **Alternate Flows:** Unknown routes receive an appropriate localized 404; blocked form endpoints fail closed without leaking secrets; build fails on missing locale keys or invalid route metadata; rollback restores a verified prior deployment.
- **Acceptance Criteria:**
  - [ ] All 12 main localized page URLs render meaningful server-delivered HTML with distinct titles/descriptions, matching canonicals and reciprocal `hreflang` tags.
  - [ ] `sitemap.xml`, `robots.txt`, social preview metadata and localized 404 behavior are validated on the production domain.
  - [ ] LocalBusiness/Organization schema includes only owner-approved facts; absent phone/address fields are omitted rather than fabricated.
  - [ ] Mobile field data or repeatable synthetic tests meet Section 12 performance targets; reduced-motion and low-bandwidth cases are tested.
  - [ ] Endpoint secrets remain in Cloudflare environment secrets; validation, Turnstile, rate limiting and restricted D1 access are demonstrated.
  - [ ] Deployment pipeline runs static/type/unit/integration checks, preview QA, production smoke tests and a documented rollback.
  - [ ] Search Console ownership, domain routing/HTTPS and monitoring ownership are established before public launch.

### P1-F001 — Gallery Filtering and Image Lightbox
- **Description:** Add filtering by verified project category plus an accessible image viewer; the unfiltered gallery remains usable if enhancements fail.
- **User Story:** As a buyer, the visitor wants to narrow examples to a relevant project type and inspect details without losing browsing context.
- **Trigger:** Choose a filter or open a gallery image.
- **Preconditions:** Gallery data has approved category keys and full-size images.
- **Postconditions:** Matching items display, or a lightbox closes to the original card with focus restored.
- **Main Flow:** Visitor loads all projects, chooses a category, sees a matching count and cards, opens an image, navigates with arrows/swipes, then closes to the previous position.
- **Alternate Flows:** No matching projects shows a localized zero-results message and `Clear filter`; image failure shows a fallback; disabled JavaScript leaves an accessible image link.
- **Acceptance Criteria:**
  - [ ] Category filtering never invents or silently reassigns project categories.
  - [ ] Zero results, pending-image and failure states have readable localized feedback.
  - [ ] Viewer supports Escape, focus trap/restore, accessible previous/next controls and touch navigation.
  - [ ] Images retain appropriate descriptions and do not download full-resolution assets until requested.

### P1-F002 — Service FAQs
- **Description:** Provide KEN-approved, localized FAQ content relevant to selection, site survey, installation, and maintenance, with cautious, factually supported answers.
- **User Story:** As a buyer, the visitor wants common questions answered before contacting sales.
- **Trigger:** Expand a question in a service or shared FAQ section.
- **Preconditions:** Answers have been approved in both languages.
- **Postconditions:** The answer is available, and visitor can proceed to a contextual request CTA.
- **Main Flow:** Visitor scans questions, expands one, reads the answer, and chooses another or contacts KEN.
- **Alternate Flows:** Missing translated answer is caught at build time; unsupported specifics direct visitors to request a tailored assessment instead of publishing guessed specifications.
- **Acceptance Criteria:**
  - [ ] At least six approved FAQ items are published across relevant services in both languages.
  - [ ] Questions work with keyboard and screen readers and expose correct expanded states.
  - [ ] FAQ text never guarantees prices, code compliance, or repair response times unless KEN verifies those claims.
  - [ ] The section remains functional without animations and has no layout clipping in RTL.

### P1-F003 — Enhanced Cinematic Interactions
- **Description:** Add optional layered transitions or parallax-like depth to major sections after P0 performance and accessibility are stable.
- **User Story:** As a visitor, the user enjoys premium editorial presentation without delays or distracting movement.
- **Trigger:** Scroll or navigate between supported sections.
- **Preconditions:** Device capabilities and reduced-motion preference permit effects; base content is already visible.
- **Postconditions:** Enhancement adds polish without modifying page semantics, CTA behavior or reading order.
- **Main Flow:** Visitor enters an eligible viewport section, the visual layer animates in a short bounded transition, and scrolling continues uninterrupted.
- **Alternate Flows:** Reduced-motion, low-end device or animation initialization failure uses static imagery and no blank section.
- **Acceptance Criteria:**
  - [ ] All enhanced sections remain fully useful with animations disabled.
  - [ ] Effects do not hijack scrolling, trap focus, trigger vestibular motion for reduced-motion users, or delay primary content.
  - [ ] Performance targets remain satisfied after P1 animation assets are included.
  - [ ] Motion QA includes Arabic and English layouts on mobile and desktop.

### P1-F004 — Privacy-Conscious Conversion Analytics
- **Description:** Track anonymous site and funnel events with a privacy-aware analytics solution (recommended: Cloudflare Web Analytics plus non-PII custom events where supported and legally approved).
- **User Story:** As KEN management, the company wants to understand which pages lead to genuine inquiries and improve the site using reliable metrics.
- **Trigger:** Page view, relevant CTA click, form start, validation failure, accepted lead, or external contact click.
- **Preconditions:** Analytics approach and consent/legal treatment have been approved; event schema is defined.
- **Postconditions:** Aggregated counts support KPI reporting without transferring raw name, phone, email or message fields to analytics.
- **Main Flow:** Visitor browses; permitted events record locale/page/service identifiers; a completed submission triggers an anonymous `lead_submitted` event only after the API confirms durable storage; dashboard shows conversion trends.
- **Alternate Flows:** Ad blocker or analytics failure does not affect browsing or form submission; consent denial, if required by chosen tooling, disables nonessential tracking.
- **Acceptance Criteria:**
  - [ ] Event schema includes `page_view`, `service_cta`, `whatsapp_click`, `phone_click`, `form_started`, `lead_submitted` and a non-sensitive `form_error` category.
  - [ ] No personal information, raw messages, tokens or full user-entered URLs enter analytics payloads.
  - [ ] `lead_submitted` only fires on confirmed server acceptance, and the dashboard reconciles its total against authorized D1 counts within an agreed reporting window.
  - [ ] Analytics failure does not delay LCP, block navigation or disrupt submitting forms.

## 8. Non-Functional Requirements

| Area | Requirement | Verification |
|---|---|---|
| Performance | p75 mobile Largest Contentful Paint (LCP) ≤ 2.5 seconds, Interaction to Next Paint (INP) ≤ 200 ms, Cumulative Layout Shift (CLS) ≤ 0.10 on launch-critical pages | Web Vitals field monitoring when traffic allows; reproducible mobile synthetic tests before launch |
| Initial Load | Homepage critical content is usable within 2 seconds on the agreed synthetic profile where practicable; target Lighthouse mobile performance score ≥ 90 across each page template | CI/QA Lighthouse runs on throttled mobile profiles |
| Media | Generate AVIF/WebP derivatives with JPEG fallback; responsive `srcset`; lazy-load below-the-fold images; prefer a lightweight hero poster to blocking background video | Network traces and build image-audit report |
| JavaScript | Route-split gallery/lightbox and enhanced motion; avoid third-party blocking scripts; establish per-route compressed asset budgets during Sprint 1 | Build bundle report; Lighthouse unused-JS check |
| Security | All form payloads validated on the server; anti-spam verification, rate limiting and idempotency; secrets stored only as environment bindings; HTTPS-only delivery | Endpoint penetration checklist, negative tests and source scan |
| Data Protection | Collect only lead-contact data needed for response; publish bilingual privacy notice; control lead access by staff role; define lawful basis, international transfers and retention with Saudi PDPL legal review | Approved privacy document and data-handling review before launch |
| Data Retention | Proposed lead retention: 12 months unless a shorter lawful business period is approved; provide documented deletion/export process | Data lifecycle test and owner sign-off |
| Backup and Recovery | Proposed daily D1 export to restricted, encrypted backup storage with 30-day rolling retention, plus restore drill before launch; validate actual provider features and legal data-location requirements | Backup job log and successful test restore |
| Availability | Target ≥ 99.9% monthly successful availability for primary pages and lead API, excluding documented agreed maintenance | Synthetic probes and operational incident log |
| Accessibility | WCAG 2.1 AA target; semantic landmarks, keyboard access, visible focus, alt text, form labels/errors, sufficient contrast and reduced-motion behavior | Axe checks plus manual keyboard and screen-reader spot checks in Arabic and English |
| Compatibility | Latest two major versions of Chrome, Firefox, Safari and Edge; current iOS Safari and Android Chrome; desktop and touch breakpoints | QA device/browser matrix |
| Localization | 100% of public UI strings and metadata translated; stable bidirectional layout, Latin phone number formatting and locale-specific typography | Missing-key build check; bilingual content sign-off |
| Scalability | Cache static/pre-rendered assets at CDN; isolate form endpoint from traffic spikes with bot protection and configurable rate limits | Burst tests and edge analytics |
| Observability | Structured request logs with correlation ID, validation category and notification status; no raw personal data in logs; alert on > 1% 5xx over a 15-minute window or sustained notification failure | Alert test and dashboard review |
| Data Residency | Validate whether Cloudflare D1 and email provider storage/processing locations are permissible for KEN's Saudi personal-data processing obligations; change provider/architecture before launch if not approved | Documented legal/security sign-off |

## 9. Technical Architecture

### Frontend Stack and Rendering
- **Framework:** React + TypeScript with Vite and Tailwind CSS, typed content models, reusable components and consistent design tokens.
- **Routing:** React Router or a compatible equivalent; stable locale routes `/ar/...` and `/en/...` with Arabic default at `/`. Build-time prerender/SSG must emit separate accessible HTML for all 12 primary localized routes; React hydrates optional interactions client-side.
- **Content Source:** Version-controlled, typed bilingual content modules (pages, services, projects and FAQ); editorial change via pull request until a future CMS is justified. A build step validates missing keys, IDs, image references, route pairings and metadata.
- **Shared Components:** SiteShell, Navbar, LanguageSwitcher, MobileMenu, PageHero, ServiceCard, ProjectCard, ImageViewer, CTASection, ContactForm, FormField, Footer, SeoHead, MotionReveal and localized EmptyState/ErrorState.
- **Fonts and Images:** Licensed Arabic and Latin webfonts served locally and subset/preloaded where feasible; responsive elevator photography; distinct decorative hero media versus real KEN project images. Avoid unapproved branding or trademarks on stock assets.
- **Motion:** Lightweight CSS transitions for essentials; lazy-loaded animation library only if needed, respecting `prefers-reduced-motion`.

### Backend and Lead Delivery
- **Runtime:** Cloudflare Pages Functions exposing a minimal `/api/v1/` REST surface; no Express server required.
- **Lead Storage:** Cloudflare D1, with migration-managed `inquiries` and `notification_attempts` tables. D1 is provisional pending privacy/data-location approval.
- **Form Security:** Cloudflare Turnstile server verification, input size caps, allowlisted content fields, rate limiting, parameterized D1 statements, idempotency key, safe error responses and least-privilege environment bindings.
- **Notifications:** Transactional email provider [TBD] sends to KEN's verified inquiry address [TBD]. Persist before notification; record delivery state and configure a retry/recovery worker or an equivalent operational replay procedure. Staff do not access inquiries via a public API.
- **Authentication / Authorization:** No visitor accounts and no user JWT. Operational access to D1, secret management and delivery logs is governed by Cloudflare/provider organization roles and multi-factor authentication. Any future read/update inquiry API requires new authenticated authorization design.

### Database Architecture
- **Content:** Source-controlled, typed static records are the system of record for public pages, services, projects and media metadata; localized representations are generated at build time and may be served through cacheable GET endpoints.
- **Transactional Records:** D1 stores inquiries and notification attempts. Each inquiry has a UUID, created timestamp, normalized contact fields, type/service context, consent timestamp/version, locale, processing status and idempotency token hash.
- **Persistence Rules:** Submission success is based on durable database acceptance, not email provider success. Personally identifiable fields are excluded from publicly cached responses, URLs, analytics events and application logs.
- **Backup and Migration:** Version SQL migrations and tested rollback strategy; create restricted daily export and restore procedure if approved within provider/region constraints.

### Infrastructure and Deployment
- **Hosting:** Cloudflare Pages for built/prerendered files, edge delivery and Pages Functions; attach D1 and Turnstile secrets through deployment environments.
- **Environments:** Local, preview/staging and production; production and preview use separate D1 databases, Turnstile configurations and email/test recipients.
- **CI/CD:** GitHub Actions (proposed) runs formatting, lint, TypeScript, unit tests, route/content checks, integration tests, accessibility smoke checks and production build before Cloudflare deployment.
- **Operations:** Connect custom domain [TBD], TLS, redirects, domain verification, sitemap and Search Console; documented rollback, operational contacts and incident escalation.

### External Integrations
| Integration | Purpose | Status |
|---|---|---|
| Cloudflare Pages | Static hosting and function runtime | Selected |
| Cloudflare D1 | Reliable lead record storage | Proposed; privacy review required |
| Cloudflare Turnstile | Anti-bot form protection | Selected |
| Transactional email provider | Lead notification | [TBD] |
| WhatsApp deep links | Direct sales contact | Number [TBD] |
| Telephone deep links | Click-to-call | Number [TBD] |
| Cloudflare Web Analytics / approved equivalent | Conversion measurement | P1 proposal |
| Google Search Console | Search indexing diagnostics | Production domain [TBD] |

## 10. Implementation Phases

### Phase 1 — Foundation and Critical Lead Prototype
- **Goal:** Prove hosting, locale architecture, brand direction and a minimal end-to-end secure lead pathway.
- **Duration:** 2 weeks — 2026-10-10 to 2026-10-23.
- **Tasks:**
  - [ ] Approve wireframes, route map, multilingual content model, and provisional design tokens.
  - [ ] Create React/TypeScript/Tailwind project, typed reusable shell, `/ar/` and `/en/` routes, and basic mobile navigation.
  - [ ] Establish Cloudflare Pages preview deployment, environment separation and CI baseline.
  - [ ] Implement an initial Contact form, D1 migration, server-side submission route and Turnstile verification in staging.
  - [ ] Demonstrate inquiry persistence and recovery after simulated notification failure.
  - [ ] Define performance budgets, event names, test fixtures and dependencies on KEN-owned assets.
- **Validation:** A mobile user can reach the Arabic preview, switch languages, submit a valid test inquiry and retrieve its stored record through authorized operations; invalid requests are rejected.

### Phase 2 — Core Pages, Services and Contact Conversion
- **Goal:** Complete all P0 content journeys, six page types and primary contact channels.
- **Duration:** 2 weeks — 2026-10-24 to 2026-11-06.
- **Tasks:**
  - [ ] Implement Home, About, Services, Projects, Why Choose Us and Contact in both languages.
  - [ ] Add all six service categories, anchors and quotation preselection.
  - [ ] Populate verified KEN projects and optimized licensed corporate media.
  - [ ] Finalize inquiry/quote fields, notification retries/recovery, WhatsApp and telephone links.
  - [ ] Add clear success/error/loading UX and link privacy notice to forms.
  - [ ] Review content accuracy, RTL layout and mobile responsiveness with KEN management.
- **Validation:** All P0 visitor journeys operate in both languages; the gallery contains only approved project evidence; live contact numbers are confirmed in staging settings.

### Phase 3 — Premium Polish and P1 Enhancements
- **Goal:** Achieve visual refinement and add enhancements without undermining performance or accessibility.
- **Duration:** 2 weeks — 2026-11-07 to 2026-11-20.
- **Tasks:**
  - [ ] Refine hero art direction, typography, section transitions and premium navy/gold details.
  - [ ] Add gallery filters and accessible lightbox where approved.
  - [ ] Publish approved bilingual FAQs and optional enhanced motion.
  - [ ] Integrate approved privacy-conscious analytics and validate anonymous events.
  - [ ] Implement and review localized SEO, schema, sitemap and social sharing metadata.
  - [ ] Run cross-browser accessibility, image optimization and performance tuning.
- **Validation:** P1 features pass keyboard/reduced-motion tests and do not regress P0 Core Web Vitals or lead submission reliability.

### Phase 4 — Launch Hardening and Production Handover
- **Goal:** Complete operational readiness, legal/security reviews, testing and public release.
- **Duration:** 2 weeks — 2026-11-21 to 2026-12-04; target launch 2026-12-05.
- **Tasks:**
  - [ ] Approve final Arabic/English copy, approved brand imagery and substantiated business claims.
  - [ ] Complete Saudi PDPL/privacy, data-location, retention and consent review; confirm vendor configuration.
  - [ ] Verify actual production phone/WhatsApp, transactional email, lead ownership and escalation plan.
  - [ ] Perform end-to-end positive/negative tests, accessibility audit, SEO crawl and mobile Lighthouse checks.
  - [ ] Validate data backup and restore, notification error handling, alerts, rollback and production smoke tests.
  - [ ] Conduct controlled beta review, resolve blockers and obtain final owner approval.
  - [ ] Publish production build, submit sitemap and establish 1-, 2- and 30-day checks.
- **Validation:** The release checklist passes in both locales, all critical dependencies are present, live form data is retrievable, and the Product Owner authorizes launch.

## 11. User Flows, Edge Cases, API Design, Data Model, Build Order and UX Rules

### 11.1 User Flows

**Flow A — Villa quotation (primary conversion)**
1. A Saudi homeowner finds a villa elevator service page through search or opens the Arabic homepage.
2. The visitor chooses `Services`, then `Villa Elevators`, and reviews the images and offering details.
3. The visitor selects `Request a Quotation`; the Contact page opens in Arabic with `quotation` and `villa` preselected.
4. The visitor provides name, phone, city, message and privacy acknowledgement; optional property/floors/timeline details can be added.
5. Browser validates the fields; user corrects any inline errors, submits, and sees a progress indicator.
6. Pages Function validates, verifies bot token, enforces idempotency/rate limiting and writes the inquiry to D1.
7. System returns a reference ID and shows an Arabic confirmation; delivery status is recorded for KEN operations even if email notification needs a retry.
8. KEN representative receives the notification or retrieves the lead securely and follows up outside the site.

**Flow B — School manager reviews proof then calls**
1. Visitor opens `/en/services` and reviews `School Elevators`.
2. Visitor opens Projects and sees verified, approved project evidence; without gallery filtering the page remains usable.
3. Visitor selects `Call KEN`; the verified `tel:` link launches the device dialer.
4. If calling is unavailable, the visitor returns to the visible WhatsApp and on-site inquiry alternatives.

**Flow C — Language switching from a deep link**
1. Visitor arrives directly at `/ar/projects`.
2. Visitor selects English; `/en/projects` displays the same page type LTR with English alt text and metadata.
3. Visitor refreshes or shares the link; English remains active because the route encodes the locale.

### 11.2 Edge Cases — Condition → System Behavior → User Feedback

| Condition | System Behavior | User Feedback |
|---|---|---|
| Required name or phone missing; malformed email/phone; message too short or too long | Block submission client-side and server-side; mark invalid fields | Localized inline correction next to each field; entered content retained |
| Form has no network connection or API times out | Do not claim a submission succeeded; preserve draft in page state | Localized retry guidance; no field data lost during retry |
| D1 write fails | Respond 503 with safe correlation ID, emit restricted alert | Clear unsuccessful-submission message and alternative phone/WhatsApp contact route |
| Transactional email fails after D1 insert | Keep durable lead, mark notification pending/failed, retry or escalate | Visitor still sees successful submission and reference ID; operations receive a failure alert |
| Turnstile token invalid/expired | Reject request before storage; allow challenge refresh | Localized message to retry human verification |
| Too many requests from an origin | Respond 429; apply cooldown without revealing sensitive rate-limit details | Non-punitive localized try-later text with direct phone fallback |
| Browser resends accepted request with same idempotency key | Return original acceptance, never create new lead | Original success confirmation and reference ID |
| Same idempotency key is reused for materially different payload | Reject with 409 and log safe conflict metadata | Localized retry option using a fresh form action |
| No public project assets approved | Do not invent projects; show explicit staging empty state; block public release | Staging displays a clear editorial message; production acceptance fails |
| Image fails to load | Retain caption/alt text and use visual fallback | Layout remains readable with no misleading blank card |
| Unsupported URL or locale | Return correctly status-coded localized 404 and navigational links | Page-not-found explanation and path to homepage/services |
| Unauthorized attempt to retrieve lead records | Do not expose inquiry data through public GET endpoints; deny restricted operational access | Generic 403/404; no user-identifying data in response |
| Missing production WhatsApp/phone setting | Suppress unusable CTA and fail launch readiness check | Working contact form remains visible in staging; no placeholder link |
| Reduced-motion preference or JavaScript enhancement failure | Keep content and links available without reveals or parallax | Same readable copy and CTA, without motion |
| Analytics blocked or consent absent | Skip nonessential tracking | No popup error and no interruption to core journey |

### 11.3 API Design (High Level)

All public API responses are JSON, use versioned resources and proper HTTP status codes, and never reveal server secrets or raw stack traces. Pre-rendered pages may bundle the same content at build time to avoid unnecessary client fetches; GET endpoints are not a prerequisite for first paint.

| Method | Endpoint | Purpose / Feature IDs | Contract and Behavior |
|---|---|---|---|
| GET | `/api/v1/pages/:slug?locale=ar\|en` | P0-F001, P0-F007 | Public localized page data and approved SEO metadata, or 404 for unknown slug |
| GET | `/api/v1/site-config?locale=ar\|en` | P0-F002, P0-F006, P0-F007 | Public approved theme settings, site labels, contact channels and public business metadata only; CDN cacheable |
| GET | `/api/v1/services?locale=ar\|en` | P0-F003 | Six localized service records, immutable IDs, anchors and approved imagery |
| GET | `/api/v1/projects?locale=ar\|en&category=...` | P0-F004, P1-F001 | Approved project metadata; optional category filter; no unpublished projects |
| POST | `/api/v1/inquiries` | P0-F005 | Validate and durably insert form submission; 201 new / 200 idempotent repeat / 400 validation / 409 conflict / 429 limit / 503 storage failure |
| GET | `/api/v1/faqs?locale=ar\|en` | P1-F002 | Approved bilingual FAQs, available when P1 is released |
| GET | `/api/v1/health` | P0-F007 | Minimal non-sensitive service health indicator; no details about secrets or internal data |

**`POST /api/v1/inquiries` proposed body (field definitions, not populated data):**
```json
{
  "idempotencyKey": "uuid-v4",
  "locale": "ar",
  "type": "quotation",
  "serviceId": "villa",
  "name": "string",
  "phone": "+9665XXXXXXXX",
  "email": null,
  "city": "string",
  "message": "string",
  "propertyType": "villa",
  "floors": 3,
  "timeline": "planning",
  "privacyAcknowledged": true,
  "privacyNoticeVersion": "v1",
  "turnstileToken": "short-lived-secret-token"
}
```
The above phone/token values illustrate format only and are not real credentials or KEN contact data. `email`, `propertyType`, `floors`, `timeline` and `serviceId` are optional where applicable; server enforces permitted enums, maximum payload size and correct data types. Response on new acceptance: `201 { "referenceId": "uuid", "status": "received" }`. The browser must never request lists of submitted inquiries.

**API-to-P0 coverage:** P0-F001 → pages; P0-F002 → site-config; P0-F003 → services; P0-F004 → projects; P0-F005 → inquiries; P0-F006 → site-config; P0-F007 → pages/site-config/health and build-time HTML artifacts. Rendering, visual effects and static SEO also have non-API acceptance tests, because they are presentation/build responsibilities.

### 11.4 Data Model

| Entity | Storage | Key Fields | Relationships / Notes |
|---|---|---|---|
| `SitePage` | Typed source content | `slug`, `locale`, `title`, `description`, `sections`, `seo`, `updatedAt` | One logical page has `ar` and `en` variants; generates prerendered HTML |
| `Service` | Typed source content | `id`, `locale`, `title`, `summary`, `useCases`, `mediaIds`, `sortOrder` | Exactly six stable IDs: `villa`, `school`, `administrative`, `restaurant`, `installation`, `maintenance` |
| `Project` | Typed source content | `id`, `locale`, `label`, `description`, `categoryIds`, `mediaIds`, `approved`, `publicationPermissionRef` | Has many `MediaAsset` records; only `approved=true` is public |
| `MediaAsset` | Source metadata + Pages assets | `id`, `src`, `width`, `height`, `altAr`, `altEn`, `rightsStatus`, `kind` | `kind` distinguishes `brand-editorial` from `ken-project`; never conflate them |
| `SiteConfig` | Public source config | `locale`, `themeTokens`, `contactPhone`, `whatsappNumber`, `publicAddress`, `serviceAreaWording`, `seoDefaults` | Only verified non-sensitive fields shipped to frontend |
| `FAQ` | Typed source content | `id`, `locale`, `question`, `answer`, `serviceIds`, `approved` | Optional P1 entity linked to Service |
| `Inquiry` | Cloudflare D1 | `id`, `createdAt`, `locale`, `type`, `serviceId`, `name`, `phoneE164`, `email`, `city`, `message`, `propertyType`, `floors`, `timeline`, `consentAt`, `privacyVersion`, `idempotencyKeyHash`, `payloadHash`, `status` | `serviceId` optionally references static service ID; unique idempotency hash prevents duplicate leads |
| `NotificationAttempt` | Cloudflare D1 | `id`, `inquiryId`, `provider`, `attemptCount`, `status`, `lastAttemptAt`, `nextRetryAt`, `errorCode` | Many attempts may relate to one Inquiry; no message content in logs |

The Inquiry storage region and any processor/subprocessor relationships require approval before production. No table named `User` or generic admin profile is needed because there is no login feature.

### 11.5 Build Order and Dependency Logic
1. Establish repository, design tokens, Arabic/English route model, Pages preview and D1 staging integration.
2. Implement secure `POST /inquiries` plus one end-to-end form and prove data persistence before investing in decorative motion.
3. Complete six page templates, source content, service CTAs, project evidence and direct contact links.
4. Add localized SEO/prerendering and operational notification/retry path; validate every primary flow.
5. Layer gallery filtering, FAQ, analytics and cinematic enhancements only once baseline accessibility and speed pass.
6. Execute security/privacy review, real asset/contact verification, production smoke tests, rollback drills and launch approval.

### 11.6 UX State Rules
- **Forms:** Idle → editing/validation → submitting → success or recoverable failure. Focus first invalid input after attempted submit; success moves focus to confirmation. Do not wipe entered fields unless successfully stored or user explicitly resets them.
- **Content lists:** Display readable content without waiting for images; explicit localized empty/error states; loading skeleton only when content genuinely requires a network request.
- **External contact:** Always a clear user-triggered action; accessible names indicate WhatsApp or telephone. No automatic application launch.
- **Language switching:** Preserve page context; maintain correct direction of text, numbers, icons, breadcrumb order, form field order and focus traversal.
- **Animations:** Decorative, interruptible, progressively enhanced and disabled when reduced motion is requested.
- **Error feedback:** Human-readable Arabic/English copy with retry or safe alternative path; no internal implementation details or personal data exposed.

## 12. Success Metrics and KPIs

Targets below are **proposed success thresholds**, not claims about KEN's current traffic, lead volume, or performance. The owner approves final thresholds at kickoff. All conversion metrics exclude known bots and internal test events.

| Category | Metric | Numeric Target | Measurement Method | Review Cadence | Owner |
|---|---|---|---|---|---|
| Business | Qualified inquiries per month | ≥ 20/month by day 90 after launch | Count D1 submissions marked qualified by KEN's lead recipient; deduplicate and exclude test/spam records | Weekly; day 30/60/90 | KEN Sales / Operations |
| Business | Visitor-to-lead conversion | ≥ 3.0% by day 90 | Unique accepted web-form leads ÷ unique website sessions, using approved analytics and D1 reconciliation | Weekly | Product Owner + SEO |
| Business | Direct-contact intent | ≥ 5.0% of service-page sessions trigger WhatsApp/phone CTA | Non-PII click events ÷ service-page sessions, reported by locale | Biweekly | Product Owner + SEO |
| Product | Quotation journey completion | ≥ 85% of moderated users complete a simulated quotation without assistance | At least 10 representative Arabic/English usability tests with a fixed scenario | Before beta | QA + Product Owner |
| Product | Content localization coverage | 100% of public strings, alt text and SEO metadata have reviewed Arabic and English variants | Build missing-key audit plus bilingual editorial checklist | Every release | Content Editor |
| Product | Form submission reliability | ≥ 99.5% of valid non-spam submissions receive a durable acceptance response | Accepted D1 writes ÷ attempts that pass validation/Turnstile, by 30-day window | Daily dashboard / weekly review | Functions Developer |
| Technical | Mobile LCP (p75) | ≤ 2.5 seconds | Real-user Web Vitals when sample size is sufficient; synthetic runs until then | Weekly | Frontend + QA |
| Technical | INP (p75) | ≤ 200 ms | Field Web Vitals, grouped by locale and page type | Weekly | Frontend + QA |
| Technical | CLS (p75) | ≤ 0.10 | Field Web Vitals and Lighthouse | Weekly | Frontend + QA |
| Technical | Lighthouse mobile performance | ≥ 90 for every main page template in both locales | Repeatable CI/test-environment Lighthouse audits | Per release | Frontend + QA |
| Technical | Monthly site/API availability | ≥ 99.9% | HTTPS synthetic health/page checks and incident records over rolling calendar month | Monthly | Operations |
| Technical | Unexpected backend error rate | < 0.1% of API requests | Aggregated `5xx` responses ÷ all API requests, excluding deliberate chaos tests | Weekly | Functions Developer |
| Accessibility | Lighthouse accessibility | ≥ 95 per representative page template, with no critical manual keyboard failures | Automated audit plus keyboard/screen-reader spot checks | Every release | QA |
| User Satisfaction | Perceived trust and ease of finding contact | Mean ≥ 4.5/5 across ≥ 10 moderated testers | Five-point post-task question collected from residential and commercial personas | Before launch; 30 days after | Product Owner |
| Operations | Notification failure recovery | 100% of persisted inquiries with failed notification are visible to the designated operator within 1 business day | Daily reconciliation of D1 inquiry records and notification statuses | Daily | KEN Sales / Operations |

**Tracking:** D1 is the authoritative source for stored lead totals; approved privacy-conscious analytics provides anonymized traffic and CTA denominators; Cloudflare operational logs/probes provide errors and uptime; Lighthouse/field Web Vitals provide performance data. Review at 1 week, 2 weeks and 30 days after launch, with a separate day-90 business impact assessment. When session data is unavailable or blocked, report the KPI as insufficient data rather than manufacturing a conversion rate.

## 13. Timeline and Milestones

- **Project Start:** 2026-10-10.
- **Proposed Launch:** 2026-12-05.
- **Total Duration:** Eight implementation weeks (four two-week phases) plus launch authorization on the following day.
- **Dependencies:** Dates move if legal/data-location approvals, verified contact numbers, production domain, gallery images or lead delivery setup are not available at the relevant gate.

| Milestone | Description | Due Date | Status | Owner |
|---|---|---|---|---|
| Kickoff | Confirm scope, roles, project access and critical content owners | 2026-10-10 | Planned | KEN Elevators Management |
| PRD Approved | Sign off requirements, success metrics and planned release scope | 2026-10-13 | Pending | KEN Elevators Management |
| Phase 1 Done | Preview environment, localized shell and secure lead prototype pass validation | 2026-10-23 | TODO | Frontend + Functions Developer |
| Phase 2 Done | Six pages, six services, approved portfolio and primary CTAs operational | 2026-11-06 | TODO | Frontend + Content Editor |
| Phase 3 Done | Premium polish, P1 features, SEO and accessibility/performance validation | 2026-11-20 | TODO | Designer + Frontend + QA |
| Beta Launch | Stakeholder-only production-like acceptance testing begins | 2026-11-28 | TODO | QA + KEN Management |
| Phase 4 Done | Operational, privacy/security and launch readiness gates passed | 2026-12-04 | TODO | QA + Operations |
| Public Launch | Custom domain points to approved bilingual Cloudflare Pages deployment | 2026-12-05 | TODO | KEN Management + Engineering |
| Week-1 Review | Assess lead reliability, contact routes, indexability and initial user issues | 2026-12-12 | Planned | Product Owner + Operations |
| Week-2 Review | Review funnel behavior and technical regressions | 2026-12-19 | Planned | Product Owner + SEO |
| Day-30 Review | Review first-month leads, performance and improvement backlog | 2027-01-04 | Planned | KEN Management |

## 14. Risk Register

**Scoring:** Likelihood × Impact, where High = 3, Medium = 2, Low = 1. Scores 7–9 are Critical, 4–6 are High, and 1–3 are Monitor.

| ID | Description | Likelihood | Impact | Score | Mitigation | Owner |
|---|---|---|---|---|---|---|
| R-01 | Authentic project photography or permissions arrive too late to build a credible gallery | High (3) | High (3) | 9 | Request minimum approved assets and captions at kickoff; block publication of fabricated references; stage content review weekly | KEN Management + Content Editor |
| R-02 | Contact number, email inbox or lead owner remains unverified | Medium (2) | High (3) | 6 | Establish owner of incoming leads in Phase 1; run live WhatsApp/phone/email tests before beta | KEN Sales / Operations |
| R-03 | Saudi PDPL or cross-border transfer obligations conflict with proposed D1/email data locations | Medium (2) | High (3) | 6 | Perform legal/vendor data-location review in Phase 1; choose compliant storage/provider before personal data enters production | KEN Management + Functions Developer |
| R-04 | Email provider outage or configuration silently loses quote requests | Medium (2) | High (3) | 6 | Store in D1 before notification; persist attempt status; retry and reconcile daily; alert failures | Functions Developer + Operations |
| R-05 | Arabic RTL defects or inconsistent English translation undermine professionalism | Medium (2) | High (3) | 6 | Shared direction-aware components, missing-key build failures, native-speaker review and bilingual device QA | Frontend + Content Editor |
| R-06 | High-resolution media and cinematic effects harm mobile Core Web Vitals | High (3) | Medium (2) | 6 | Media budget, static poster, responsive images, lazy-load motion and performance gates for each release | Frontend + Designer |
| R-07 | Unverified quality, safety or compliance claims expose the brand to reputational/legal risk | Medium (2) | High (3) | 6 | Require written KEN approval of every factual claim, testimonial, certification and project caption | KEN Management + Content Editor |
| R-08 | Bot traffic or API abuse increases load and contaminates lead records | Medium (2) | Medium (2) | 4 | Turnstile, rate limiting, validation, idempotency and monitored spam categories | Functions Developer |
| R-09 | Scope expansion into CMS, instant pricing or application features jeopardizes launch | Medium (2) | Medium (2) | 4 | Enforce P0/P1/P2/P3 gates; require written change approval and schedule impact assessment | Product Owner |
| R-10 | External design/content approval delays compress final test time | Medium (2) | High (3) | 6 | Weekly approvals, fixed review deadlines, explicit beta freeze and escalation to owner | KEN Management + Product Owner |
| R-11 | Cloudflare/service configuration differs between preview and production | Medium (2) | Medium (2) | 4 | Separate environment configurations, documented bindings and production smoke tests | Functions Developer + QA |
| R-12 | Single-person ownership or undocumented lead retrieval blocks operations | Low (1) | High (3) | 3 | Document runbooks, ensure two authorized staff members and test backup access before launch | KEN Operations |

## 15. Stakeholders and Approvals

### Stakeholders

| Name | Role | Involvement | Contact |
|---|---|---|---|
| KEN Elevators Management | Project Owner / final approver | Business objectives, brand accuracy, scope and launch authorization | [TBD] |
| Product Manager (individual [TBD]) | Delivery coordination | Requirements, backlog, prioritization and acceptance decisions | [TBD] |
| UI/UX Designer (individual [TBD]) | Design owner | Responsive visual direction, components and motion/accessibility | [TBD] |
| Frontend Developer (individual [TBD]) | Frontend implementation | React, localization, SEO rendering, image performance | [TBD] |
| Functions Developer (individual [TBD]) | Backend/data owner | Form endpoint, D1, security, notifications, deployment secrets | [TBD] |
| Arabic/English Content Editor (individual [TBD]) | Editorial owner | Translations, service descriptions, projects and claim verification | [TBD] |
| QA / Accessibility Engineer (individual [TBD]) | Quality owner | Cross-browser, RTL, form/security and accessibility acceptance | [TBD] |
| KEN Sales / Operations Lead (individual [TBD]) | Lead-process owner | Contact details, notification inbox, response workflow and data access | [TBD] |
| Legal / Privacy Reviewer (individual [TBD]) | Compliance advisor | PDPL, consent, privacy notice and processor/data-region approval | [TBD] |

### Approval Gates

| Gate | Approver | Required By | Status |
|---|---|---|---|
| PRD and MoSCoW sign-off | KEN Management | 2026-10-13 | Pending |
| Visual design and brand direction | KEN Management + Designer | 2026-10-23 | Pending |
| Approved bilingual copy and real project evidence | KEN Management + Content Editor | 2026-11-06 | Pending |
| Form operation and lead notification ownership | KEN Sales / Operations + Functions Developer | 2026-11-06 | Pending |
| Security, privacy and data-location clearance | KEN Management + Legal Reviewer | 2026-11-28 | Pending |
| Beta acceptance: SEO, speed, accessibility and all P0 journeys | QA + Product Owner | 2026-12-04 | Pending |
| Production launch authorization | KEN Management | 2026-12-05 | Pending |

## 16. References and Links

| Reference | Location / Identifier | Notes |
|---|---|---|
| Design files / Figma | [TBD] | Approved navy/gold system, mobile and desktop layouts |
| Company logo / brand guidelines | [TBD] | Rights and approved usage required |
| Approved KEN project photography | [TBD] | Project-specific consent/permissions and descriptive metadata required |
| Repository | [TBD] | Canonical source repository containing this PRD |
| API documentation | [TBD] | Implementation contract for `/api/v1/` defined in Section 11 |
| Architecture diagram | [TBD] | React prerendering, Pages Functions, D1 and email notification path |
| Staging environment | [TBD] | Cloudflare Pages preview address |
| Production environment / domain | [TBD] | Public custom domain, HTTPS and localized routes |
| CI/CD pipeline | [TBD] | Proposed GitHub Actions workflow |
| Monitoring dashboard | [TBD] | Operational form, uptime and performance observability |
| Analytics dashboard | [TBD] | P1 privacy-conscious site and funnel events |
| Legal privacy notice | [TBD] | Approved Arabic/English copy and retention details |
| Related PRDs | [TBD] | No related document supplied |
| Team communications / Slack channel | [TBD] | Optional; not a delivery prerequisite |
| Meeting notes and approvals | [TBD] | Decision and sign-off log |

## 17. Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| v1.0 | 2026-10-10 | KEN Elevators Management | Initial PRD created |
