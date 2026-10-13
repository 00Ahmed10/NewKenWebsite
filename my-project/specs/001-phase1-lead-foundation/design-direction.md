# KEN Elevators — Premium UI/UX Design Direction

**Feature:** 001-phase1-lead-foundation
**Date:** 2026-10-13
**Status:** Proposed design direction for review and later authorized implementation. No visual sign-off, implemented UI, measured browser performance or release approval is claimed.
**Sources:** [spec.md](spec.md), [plan.md](plan.md), [tasks.md](tasks.md), [quality-strategy.md](quality-strategy.md), [research.md](research.md), [dependencies.md](dependencies.md), [historical analysis](analysis-report.md), [PRD-001 v1.0](../../../docs/PRD.md), [constitution v1.0.0](../../.specify/memory/constitution.md).

## 1. Authority, approval status and phase boundary

This document translates the user's requested Quiet Luxury, Premium Architecture and Precision Engineering direction into a reviewable design system. It replaces the earlier provisional palette/font proposal in the plan and research, without changing the PRD, constitution, routes, form contracts or task sequence. Exact colors/fonts/imagery still require DEP-02/03/09 approval. The source PRD remains Draft pending stakeholder approval; “required baseline” below means an existing governing requirement, not proof that KEN has approved it.

| Status | Direction and consequence |
|---|---|
| Existing required baseline | Arabic-first RTL with equivalent English LTR; six primary route pairs plus privacy; six stable service IDs; initial SSG HTML; accessible quotation/general forms; verified contacts; honest preparation/project states; restrained progressive motion; existing speed and accessibility gates |
| User-requested design proposal | Five concise homepage sections, the specified five-color palette, Alexandria Arabic headings, IBM Plex Sans Arabic body, Manrope English, architectural imagery, precise component proportions and spacious composition; final stakeholder visual/editorial acceptance pending |
| Phase 1 implementation candidate | Static cinematic composition using licensed still media when supplied, or an honest navy CSS surface; visible content/CTAs from first HTML; existing 120–180ms color/opacity feedback only; no door movement, camera motion, video or parallax |
| Later optional proposal | Door-opening storyboard, desktop pointer depth and richer materials under P1-F003 / PRD delivery Phase 3; separately approved scope, assets, technical proof, schedule and QA evidence required |
| Conditional later architecture proposal | Lazy-loaded React Three Fiber/Three.js only if simpler media/CSS cannot achieve the approved look and measured evidence justifies the cost; not a Phase 1 dependency or a committed v1.0 deliverable |

Delivery Phase 1 is distinct from PRD enhancement priority P1 and from the numbered execution phases inside tasks.md. T087 keeps its limited Phase 1 transitions. T079–T092 homepage decoration still waits for hosted lead/recovery acceptance T078. Design documentation and review preparation may happen earlier. All 117 task IDs stay unchanged and unchecked.

## 2. Visual idea: an architectural threshold

KEN's visual signature is a carefully framed elevator threshold: one vertical champagne-bronze seam, warm indirect light and a deep navy architectural surround. A large Arabic headline and two clear actions occupy calm negative space beside that threshold. Precision comes from alignment, measured spacing, crisp type and consistent material detail. Luxury comes from restraint and image quality.

Use Saudi corporate luxury through Arabic editorial confidence, dignified composition and warm architectural materials. Geography, nationwide coverage, safety certification, response times, warranty terms and credentials must come from verified KEN content. Do not use a Saudi seal, flag motif, award badge, competitor branding or skyline to imply endorsement or an unverified project location.

Proposed visual distribution: navy carries the hero, Why KEN and closing CTA; ivory carries solutions and service rows. Graphite anchors light-surface text. Gold accents buttons, selected navigation, section markers and the elevator material. As a review heuristic, gold should occupy roughly 5–10% of the interface surfaces outside the editorial photograph, not entire sections. Do not tint every icon, card, heading and border gold. This ratio is an art-direction guide, not an asset audit requirement.

The memorable detail is the door seam, reused sparingly as a section divider or narrow border. Avoid crowded dashboards, decorative statistics, rotating banners, gradient text, excessive rounded pills, constant glow, particles, floating objects and high-frequency reflection sweeps. Use one deliberate hero image rather than a carousel.

## 3. Design system

### 3.1 Palette and semantic roles

These are proposed named design tokens, not implemented CSS. Solid-color pairings below use the WCAG relative-luminance calculation; ratios were calculated during documentation review and rounded to two decimals. Final rendered contrast, opacity, photographic backgrounds and interaction states still require QA.

| Token | Hex | Intended use |
|---|---|---|
| Midnight Navy | #081722 | Primary dark canvas, hero, Why KEN, final CTA and footer |
| Deep Navy | #0B1220 | Recessed surfaces and menu; distinguish adjoining navy surfaces through spacing/borders rather than color alone |
| Champagne Gold | #BEA073 | Primary CTA fill with navy text, gold text/icons on navy, selected dark-surface marker, decorative material |
| Warm Ivory | #F5F2EB | Reading surfaces and text on navy; form panel background |
| Graphite | #28343D | Light-surface body text, labels and control outlines |
| Error utility, proposed | #B42318 | Error text/icon/outline on ivory form panels; accompany with plain text |
| Success utility, proposed | #216E50 | Durable-success text/icon on ivory confirmation panels; accompany with reference and text |

| Solid pairing | Ratio | Decision |
|---|---:|---|
| Ivory / Midnight | 16.25:1 | Body/headings on dark sections |
| Ivory / Deep Navy | 16.75:1 | Navigation and recessed dark surfaces |
| Graphite / Ivory | 11.39:1 | Light-surface text and essential control outlines |
| Gold / Midnight | 7.32:1 | Accent text, icons and primary-button navy text on gold |
| Gold / Deep Navy | 7.55:1 | Accent text and control indicators on deep navy |
| Gold / Ivory | 2.22:1 | Decorative only; fails normal/large text and essential 3:1 control contrast |
| Graphite / Midnight | 1.43:1 | Do not use for essential text, controls or boundaries |
| Error / Ivory | 5.88:1 | Error text on the ivory form panel |
| Success / Ivory | 5.51:1 | Confirmation text on the ivory panel |

Normal text needs at least 4.5:1; large text and applicable non-text indicators need at least 3:1 under the existing WCAG 2.1 AA target. The gold/ivory ratio also applies to gold outlines: use graphite or navy for an essential outline on ivory. Do not assume that a low-opacity border or a gradient has these solid-color ratios. [W3C contrast guidance](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html).

Keep form/error/success panels ivory even inside a navy Contact layout so utility colors have one tested pairing. Dark disabled buttons retain readable labels and a visible reason; state is conveyed through semantics and text, not opacity alone. Hover keeps the solid pairings and adds an underline or border change without shifting geometry.

Focus proposal: a 2px inner ivory ring and 2px outer navy ring with clear spacing. On navy, the ivory band remains visible; on ivory, the navy band remains visible. Render-test against gold buttons, images, outlines and browser forced-colors settings; retain a system outline in forced colors. Focus must not be clipped by image/card overflow.

### 3.2 Geometry, grid and spacing

- Content maximum width: 1248 CSS px; center the container. At 1440px, approximately 96px outer margins. Desktop uses a 12-column alignment grid and 24–32px gaps, not twelve visible card columns.
- Gutters: 20px at 360/390, 32px around 768, 48px around 1024; allow fluid growth into the maximum container. Respect device safe areas for edge controls.
- Spacing scale: 4, 8, 12, 16, 24, 32, 48, 64, 80, 96, 120px. Section block padding: 80–120px desktop, 64–80px tablet, 48–64px mobile. Internal heading-to-copy 16–24px; copy-to-action 24–32px.
- Controls: minimum 44×44px targets; standard button/input height 52px desktop, 48–52px mobile, allowed to grow for text. Radius 6px controls, 10px cards, 12px major image frame; no arbitrary radius variations.
- Cards: 24–32px padding desktop, 20–24px mobile. Thin decorative borders, nearly flat surfaces, at most one soft shadow for a raised form/menu. Hover never lifts an entire content block in Phase 1.
- Dividers: 1px decorative rules; do not rely on them alone to distinguish required inputs or active controls. Narrow seam motifs occupy blank space and do not slice through headings.
- Reading width: Arabic body generally 38–52 characters per line, English 50–65; maximum around 640px for paragraphs. Legal notices may use a longer single reading column with comfortable line height.

Alignment is logical: Arabic content aligns to inline-start on the right; English to inline-start on the left. DOM reading/tab order follows the visible logical sequence; avoid visual reversal that leaves keyboard order inconsistent. Text and CTAs never inherit the media's camera transforms.

### 3.3 Typography

| Role | Arabic proposal | English proposal | Mobile / tablet / desktop sizes (CSS px) |
|---|---|---|---|
| Hero H1 | Alexandria 600, optional approved 700 | Manrope 600–700 | 36–42 / 48–56 / 64–72; line height ar 1.30–1.40, en 1.10–1.20 |
| Section H2 | Alexandria 600 | Manrope 600 | 28–32 / 36–40 / 40–48; ar 1.35, en 1.20–1.30 |
| Card H3 | Alexandria 600 | Manrope 600 | 22–24 / 24 / 24–28; ar 1.40, en 1.30 |
| Body / supporting sentence | IBM Plex Sans Arabic 400 | Manrope 400 | 17–18 / 18 / 18; ar 1.75–1.85, en 1.60–1.70 |
| Form labels / buttons | IBM Plex Sans Arabic 500 | Manrope 600 | 16–18 at all widths; line height ≥1.5 and wrap allowed |
| Caption / utility | IBM Plex Sans Arabic 400 | Manrope 400–500 | 14–16; no tiny gold legal text |

Choose a two-line Arabic hero where reviewed copy permits, up to three on narrow screens; natural wrapping takes precedence over an art-directed fixed height. No clipping, line-clamp or forced manual breaks in translated headings. Set Arabic letter spacing to zero; preserve joining, diacritics, lam-alef and mixed-direction punctuation. Avoid justified Arabic body text and fake/synthetic bold. Prefer weight 600 for most headings; use 700 only for the hero if it can be delivered within budget. English uses Manrope throughout, with normal body spacing and at most subtle display tracking after readability review. No additional serif display family is proposed.

**Licensing research, checked 2026-10-13:** Alexandria and Manrope publish SIL OFL 1.1 licenses. IBM's Plex source license is OFL 1.1 and identifies the reserved name Plex; Google Fonts metadata separately identifies IBM Plex Sans Arabic as OFL and lists its static weights. This supports a local-webfont candidate, not final approval of an unspecified binary or derivative. Preserve copyright/license notices, confirm reserved-name obligations for any modified subset, record upstream revision, exact file hash and conversion/subset provenance under DEP-02. No font files were downloaded or installed in this work. [Alexandria license](https://github.com/google/fonts/blob/main/ofl/alexandria/OFL.txt), [IBM Plex license](https://github.com/IBM/plex/blob/master/LICENSE.txt), [IBM Arabic metadata](https://raw.githubusercontent.com/google/fonts/main/ofl/ibmplexsansarabic/METADATA.pb), [Manrope license](https://github.com/google/fonts/blob/main/ofl/manrope/OFL.txt).

**Delivery proposal:** same-origin WOFF2; Arabic heading 600 (optional 700), Arabic body 400/500, English Manrope 400/600/700. Compare static subsets against a restricted variable file; do not assume all requested weights fit 120 KiB. Request only the current locale's needed glyphs/weights, including any Latin fragments actually used in Arabic. Alexandria variable metadata covers 100–900, Manrope 200–800; these ranges are not permission to load every weight. [Alexandria metadata](https://raw.githubusercontent.com/google/fonts/main/ofl/alexandria/METADATA.pb), [Manrope metadata](https://raw.githubusercontent.com/google/fonts/main/ofl/manrope/METADATA.pb).

Use font-display: swap, selective preload for the critical heading face only if traces justify it, and system fallbacks with measured metrics. Arabic fallback: a tested locally available Arabic-capable sans-serif such as Tahoma/Arial, then sans-serif; English: system-ui, Arial, sans-serif. Match fallback size/ascent/descent/line-gap using the actual chosen files where supported, not invented metric values. Do not preload both locales. Fallback must show readable content immediately and avoid layout shift. [Browser-vendor font guidance](https://web.dev/articles/font-best-practices).

T084 must record actual WOFF2 bytes for the selected locale, including mixed-script dependencies, shaping specimens, slow/blocked-font screenshots and CLS traces. If the two Arabic families cannot fit the existing ≤120 KiB budget while preserving shaping, first reduce nonessential weights and glyph coverage safely. If still too large, retain the reviewed system/provisional fallback and record the proposed type treatment as pending; any font substitution or budget exception needs a documented DEP-02/12 decision. This document does not claim a measured font-size/performance/accessibility pass.

### 3.4 Imagery and materials

Hero brief: symmetrical brushed champagne-bronze doors, understated vertical grain, controlled highlights and warm off-frame architectural light. Surround with navy/graphite stone or a calm architectural surface. Preserve physical door proportions; no saturated yellow-gold, mirror-like glare, exposed brand labels or dramatic fisheye. Provide a wide desktop crop and a portrait mobile crop with a clear focal point; use matching opening/final posters for a later sequence.

Use approved editorial media for the hero and solution inspiration. Mark editorial imagery as illustrative through an adjacent reviewed bilingual caption when it could be mistaken for KEN work. This includes any future commissioned render; such a render must never be classified as a completed KEN project. Project inset/gallery accepts only genuine approved KEN assets and captions with internal permission evidence. Never put editorial photographs inside a project evidence card.

Media content is an external DEP-09 dependency. Without supplied rights-cleared media, use a flat navy surface with a subtle decorative seam and a visible localized preparation explanation; do not fabricate a luxury elevator photo. Image failure preserves aspect ratio, text, actions and any relevant alternative. Decorative hero imagery has empty alt; meaningful solution/project imagery has native-reviewed Arabic/English alternatives. Do not bake headlines, service labels or CTA text into photographs.

## 4. Five-section homepage wireframe

### 4.1 Shared frame

Header sits in normal flow, roughly 80–88px desktop/64–72px mobile, with approved logo, six primary destinations, language switch and quotation action. At narrow widths use the already planned nonmodal disclosure menu, not a new full-screen modal. Keep the desktop header solid navy so navigation contrast does not depend on a photograph. Collapse whenever labels no longer fit, expected near 1024px, and verify with actual Arabic/English copy. Visible skip link appears on focus.

Footer is outside the five editorial sections. It retains all six primary links, both locale access, matching-locale privacy link and only verified company/contact facts. No invented address, schedule, social account or certifications. Missing contact facts leave the on-site form path visible. Do not add a persistent floating WhatsApp or bottom CTA that obscures content, verification or keyboard focus.

### 4.2 Section wireframes and copy limits

Copy limits are editorial targets excluding required accessible labels and preparation/legal explanations. They never truncate translations or remove required information.

| Section | Desktop wireframe | Mobile wireframe | Content and paths |
|---|---|---|---|
| 1. Cinematic hero | Navy canvas; copy occupies about five columns at inline-start, framed elevator imagery about seven at inline-end. H1, one sentence, two CTAs; no text over the door seam. Image may be tall within a 600–720px natural hero; no fixed viewport trap. | Copy first, primary/secondary actions next, portrait still last. Headline and primary action should be reachable in the initial viewport under normal settings; enlarged text may extend height. Media never pushes the only quotation path below a full-screen image. | One H1, roughly 4–8 Arabic words / 5–10 English words; supporting sentence ≤20 Arabic / 25 English words. Primary “اطلب عرض سعر” / “Request a quotation” → locale/contact?type=quotation. Secondary “استكشف الحلول” / “Explore solutions” → ordinary #solutions anchor on this homepage. Native editors approve wording. |
| 2. Three featured solutions | Ivory; short H2 and three equal image-led cards. Proposed ordering: villa, school, administrative. Each has approved category name, one short sentence and one visible quotation link. Under cards, a compact fourth-category restaurant entry, equally legible; not a fourth featured image card. | Three cards stack in logical order; no swipe carousel. Restaurant is a full-width text/action row beneath, with ≥44px target. | Villa, school, administrative links → locale/contact?type=quotation&service=ID. Restaurant row uses service=restaurant. #solutions exists in initial HTML. Phase 1 shows category labels/selection only plus preparation copy for unapproved detail, not invented suitability specifications. Phase 2 may add a distinct Services anchor link per category. |
| 3. Why KEN — three benefits | Navy; H2 plus three concise aligned columns/rows with restrained line icons. Below, one slim project-evidence/status inset and Projects link, within this section rather than a sixth homepage section. | Three benefit rows stack; icon never replaces text. Project status stays visible as a compact inset with explanatory copy and a link. | Proposed benefit themes: building-fit discussion, finish/detail consideration, installation-to-maintenance continuity. These are content themes for approval, not verified KEN claims. Unapproved benefits use explicit localized preparation copy. Project inset: honest preparation/empty text in Phase 1 unless real evidence is approved; later one real approved preview/caption → locale/projects. Why KEN path → locale/why-ken, a preparation destination in Phase 1. |
| 4. Installation and maintenance | Ivory; two generous text-led service rows/cards, optional one shared architectural/detail image if licensed and budgeted. Each has title, one approved sentence and quotation link. | Installation then maintenance stack, actions remain in normal flow; no accordion hides the only service choice. | Links carry service=installation and service=maintenance. Together with section 2 this provides exactly six distinct service choices. No claims of 24/7 response, free visits, certifications, coverage or maintenance guarantees. Full service descriptions/anchors arrive in Phase 2. |
| 5. Final quotation/contact CTA | Navy; one confident H2, one sentence and quotation/general-contact actions with ample space. Thin champagne seam, no second hero or form embedded here. | Stacked actions full width when needed; short copy. Footer follows normally, never pinned over the CTA. | Quotation → locale/contact?type=quotation; Contact → locale/contact?type=general. Phone/WhatsApp may appear only as verified optional actions elsewhere in the shared Contact/footer pattern. Phase 1 synthetic-only notice remains visible wherever the prototype requests input. |

The three featured solution IDs are a proposed prominence choice, not a ranking of company capability. School/administrative/restaurant remain separate stable IDs; do not rename them into a new “commercial” service or remove restaurant to simplify the homepage. Icons are generic architectural cues and do not imply safety certification or wheelchair suitability.

The inline project inset preserves spec FR-005 and the PRD P0-F002 project-preview flow while keeping five editorial sections. A minimal approved thumbnail is optional; an explicit project-preparation message is sufficient for Phase 1. Do not suppress the status merely to make the layout cleaner. A public release still needs ≥3 real approved projects and ≥6 approved images on Projects under P0-F004/DEP-09.

### 4.3 Route and context preservation

| Page | Arabic | English | Phase 1 presentation |
|---|---|---|---|
| Home | /ar/ | /en/ | Initial five-section foundation |
| About | /ar/about | /en/about | Localized preparation + contact path |
| Services | /ar/services | /en/services | Localized preparation + contact path; full six anchored categories later |
| Projects | /ar/projects | /en/projects | Honest preparation; no stock-as-project evidence |
| Why KEN | /ar/why-ken | /en/why-ken | Localized preparation + contact path |
| Contact | /ar/contact | /en/contact | General/quotation synthetic prototype |
| Privacy utility | /ar/privacy | /en/privacy | Reviewed preview notice status; legal approval before real intake |

Root / resolves to Arabic. Navigation retains all six page items; privacy is a utility. The homepage secondary CTA's anchor is a regular document anchor, with no scroll hijack or mandatory smooth scrolling. Form context uses only validated type/service query values, never personal data. Language switching preserves the paired page and safe context according to contracts/ui-localization.md; no personal drafts are persisted or promised across locale navigation. Phase 2 completes the eight preparation documents into meaningful marketing pages; design brevity does not waive those routes.

## 5. Responsive and resilient behavior

| Width / situation | Design behavior and acceptance |
|---|---|
| 360 / 390px | 20px gutters; one-column content; wrapping H1/CTAs; no horizontal overflow; 48–52px controls; portrait still with reserved ratio; no door sequence or pointer parallax |
| 768px | 32px gutters; stacked hero or compact split only if both languages fit; three solution cards may stay stacked or form a two-column grid without an orphan overflow; service rows can be two columns where readable |
| 1024px | 48px gutters; controlled split hero; three solutions when minimum readable card width fits; header disclosure if six labels/actions do not fit; still no mandatory animation |
| 1440px | 1248px centered container; generous whitespace; split hero; three solutions/benefits; two service rows; proposed later fine-pointer effect may be eligible after its separate gates |
| 200% zoom / 320px reflow equivalent | Text reflows, columns collapse, actions grow; no fixed text heights, hidden labels or clipped Arabic diacritics. Hero height follows content; menu/focus remain visible |
| RTL / LTR | Mirror logical layout and directional link arrows, not photographs, phone/reference strings or symmetric door mechanics. Isolate phone, IDs and numbers in LTR spans; preserve natural DOM order |
| Reduced motion | Static final/open still or Phase 1 surface from first paint; no parallax, camera, door movement, autoplay or delayed fades; state changes remain understandable without transitions |
| No JS / font or media error | SSG title/copy/links/status remain readable. Media space retained; system fonts render. Form explains unavailable verified submission; do not present a false working submit |

No fixed height is a content cap. Test Arabic shaping/line-height with longest reviewed strings, accessibility text-spacing overrides and native screen readers. Small touch devices use the still even if they advertise a fast GPU. High DPR alone is not a reason to send a larger asset than the derivative budget permits.

## 6. Components and conversion UX

| Pattern | Proposed visual and interaction specification |
|---|---|
| Header/menu/language | One shared six-item route map; visible active page label/underline; clear language names; nonmodal menu with aria-expanded, excluded hidden links, Escape and trigger restoration; translation/reading order reviewed independently |
| Primary / secondary actions | Gold fill with navy label for primary on navy; navy fill on ivory where stronger hierarchy is needed. Secondary ivory text/outline on navy or graphite text/outline on ivory. Real links navigate, real buttons act. Default/hover/focus/disabled/pending specified without motion dependence |
| Solution/service card | Semantic H3, approved text or explicit preparation status, reserved image, single clearly labeled category action. No hover-only description or redundant nested clickable controls; visible keyboard focus; same logical order both locales |
| Why KEN/project status | Three approved concise themes or visible preparation text. Project inset caption/status + safe Projects link; no synthetic counters, invented clients, star reviews or borrowed certifications |
| Contact panel | Ivory form on navy/ivory architecture; one-column mobile, at most two columns for short fields on desktop; full-width message, verification, privacy and feedback. Bilingual labels always visible; optional details clearly marked |
| Empty/preparation/error | Calm localized heading/sentence and working on-site contact/home path. Public-facing copy explains availability; internal DEP/task/provider details belong only in review evidence |
| Privacy / legal | Comfortable single reading column, clear headings, matching-locale link from both form modes and footer; no condensed low-contrast legal typography |
| Modal, future only | If later lightbox/modal approved, Escape, focus trap/background inertness and restoration are mandatory. Phase 1 builds no unused modal or gallery feature |

Contact preserves the existing shared POST /api/v1/inquiries contract and preparation boundary. Required: name, valid normalized phone, message, inquiry type, privacy acknowledgement; email/city/service and quotation building details remain optional. All six service selections are editable/clearable. No instant quotation or account appears.

Idle/editing → validation → submitting → durable received confirmation or recoverable failure. Privacy acknowledgement is unchecked and links the current locale notice. Send remains disabled until fields/privacy/fresh verification/configuration are ready, and during pending/cooldown. The existing enabled “Check form” action remains visible in the action region; it and invalid single-line Enter trigger the same localized corrections/first-invalid focus. Textarea Enter stays a newline. Premium minimalism must not hide that action, token help, disabled reason, field errors or error summary.

Confirmation moves focus to a readable panel with safe bidi-isolated reference after durable storage only. Do not claim that email arrived, an operator replied or a visit is scheduled. Failure keeps input in page memory with retry/cooldown/challenge guidance. Unknown acceptance preserves its original submission identity/content/notice for retry even after notice rollover; changed retained content receives explicit conflict/new-action guidance. New/definitely unaccepted drafts require the current notice. These remediation behaviors remain authoritative; no design rewrite changes them.

Phone/WhatsApp need verified numbers and deliberate activation; missing channels have no actionable placeholder link. Unapproved privacy/infrastructure allows protected synthetic testing only. Do not collect analytics for cinematic playback or pointer motion in Phase 1, or log pointer trajectories/personal inputs in later design diagnostics.

## 7. Signature door-opening storyboard — later proposal only

### 7.1 Art direction and camera

A front-facing pair of brushed champagne-bronze panels sits inside a deep navy architectural portal. Warm fixed light grazes the grain; reflections respond slowly to the door edges and small camera displacement, never sparkle. Opening reveals a composed ivory/graphite cabin or architectural interior licensed as editorial imagery. Keep labels/CTAs in the separate HTML copy area at every frame; the “reveal” reveals only decorative scenery, not the website content.

Camera proposal for a real 3D study: vertical architectural lines, approximately 35–40 degree vertical field of view, centered near the door seam; ≤2% forward dolly of initial camera-to-door distance. No orbit, roll, zoom-through-cabin or user-controlled camera. A CSS/media version approximates this with up to 1.02 background scale; realistic moving reflections cannot be guaranteed by CSS alone. Crop and motion are symmetrical, so the physical doors are not reversed between Arabic and English.

### 7.2 Timeline

Times are proposed from an explicit localized Play activation after the scene is ready; no navigation-time loading delay and no automatic replay. Total sequence: 2.6 seconds. No audio track.

| Time | Frame / doors | Camera / light | Content / controls |
|---|---|---|---|
| Before activation | Rights-cleared closed-door poster (or static final still for fallback); all text already visible | Fixed frame and architectural lighting | Quotation/Explore usable; Play available only on eligible approved later variant |
| 0–0.30s | Closed seam holds briefly; no flashing or loading curtain | Camera still; gentle existing highlights, no sweep | Stop control visible; user may navigate/scroll immediately |
| 0.30–1.90s | Doors translate horizontally into side pockets, each roughly one panel width plus a small recess; final clear opening follows portal geometry | ≤2% dolly develops gradually; warm interior illumination revealed by geometry, not a brightness burst | Copy/CTA layer remains fixed and readable; no focus change |
| 1.90–2.30s | Doors decelerate into final position without bounce or overshoot | Dolly settles; reflections become still | Stop remains operable; no scrolling synchronization |
| 2.30–2.60s | Final open architectural frame | Static final pose | Playback completes; explicit Replay and motion preference control available |
| After 2.60s | No loop | Fine-pointer depth only if separately enabled and eligible; otherwise idle rendering stops | Normal page scroll/navigation; Replay never tied to form submission |

Suggested opening easing: cubic-bezier(0.22, 1, 0.36, 1), subject to physical plausibility review. No overshoot, elastic response or full-screen overlay. Play/replay may reset only the decorative scene to its start; Stop settles immediately to the final still rather than trapping half-open imagery over content. Asset loading/preparation is independent of this clock.

### 7.3 Interaction state contract

| State / event | Required later behavior |
|---|---|
| Static/not eligible | Poster only; no video/WebGL/module transfer. Phase 1 and mobile default here. Content/nav/forms work independently |
| Eligible idle | ≥1024px, fine pointer/hover, no reduced motion, no known data-saving request and approved later enhancement flag; poster persists. Use an accessible Play button; do not auto-start or loop |
| Preparing after Play | Keep poster and useful CTAs. Localized pending state on Play; cancel/Stop available. Media/module timeout proposal 3s → still plus concise localized unavailable feedback, no blank canvas |
| Playing | Stop remains keyboard/touch accessible. Scene confined to media frame; no pointer capture over scroll, no focus grab, no content/CTA occlusion |
| Stop / scroll hero out / route change / tab hidden | Stop motion immediately; settle to still when appropriate; release listeners/render loop and later WebGL resources. No restart on tab return or scroll re-entry |
| Completed | Retain open still; explicit Replay only. Pointer movement may add depth under the separate motion preference; keyboard users need no equivalent decorative gesture |
| Reduced-motion preference changes | Immediately disable door/camera/parallax, use final still and prevent further effect downloads. Remove/disable playback appropriately with understandable localized state; never override system reduction |
| Pointer leaves / focus approaches CTA | Ease scene back to neutral (or immediate neutral under reduction); do not move text/buttons. No hover-only action |
| Enhancement/media/context failure | Keep or restore still at identical dimensions, remove broken playback action with localized feedback; navigation and inquiry remain independent. No automatic retry loop |
| Locale switch | Paired route preserved by existing contract; movie is not automatically restarted. Controls/feedback use the selected language |

Pointer depth is a later decorative proposal: maximum ±1 degree yaw/pitch and ±6 CSS px displacement within the frame, with 180–250ms damping. Apply only inside the media region, with requestAnimationFrame updates and no React state update for every pointer event. Stop updates when idle/out of view. Provide a persistent-in-session “Motion off” control near playback when pointer effect is offered; no continuous ambient motion or data collection. Keyboard focus, primary actions and document geometry never move.

Mobile/tablet/coarse pointer: optimized final/open still by default, with no parallax, gyro/device-orientation access or video/3D download. A later separate media opt-in can be considered only with its own device/byte evidence; it is not part of this recommendation. Reduced motion, unavailable WebGL, save-data where exposed, blocked scripts and slow-loading failure all select the same static presentation. Eligibility checks choose the effect; they do not remove initial SSG content.

Provide Stop for the proposed animation even though its one-shot duration is under five seconds, and Motion off for pointer depth. No flashing effects. Controls remain ≥44px with visible focus and localized accessible names. Decorative canvas/video is excluded from the accessibility tree; surrounding HTML carries all meaningful content. [W3C motion-control guidance](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html).

## 8. Feasibility and recommended delivery path

The following estimates are design constraints and engineering hypotheses, not measured bundle sizes or frame-rate results. No packages are selected or installed by this document.

| Approach | Fidelity and tradeoff | SSG/accessibility/performance integration | Recommendation |
|---|---|---|---|
| Static image / CSS surface | Editorial photo can preserve luxury reflections; honest CSS surface works without supplied media. No real opening movement | Initial HTML, reserved image ratio, eager responsive hero or zero-media fallback; no added runtime | Required Phase 1 fallback; primary release baseline regardless of later effects |
| CSS 3D layered doors | Two textured planes/edge strips translate apart; perspective and a cabin still create plausible shallow depth. Reflections are baked/approximated, not physically accurate; flattening/clipping must be checked | HTML copy stays outside transform tree; native transforms/opacity; no new dependency. Test browser compositor costs, layers and unsupported fallback | First later interactive prototype if approved; avoid presenting it as photorealistic 3D |
| Optimized rendered media | Pre-rendered short sequence offers the strongest predictable lighting/reflections without real-time renderer; limited live depth | Poster in SSG; explicit playback fetches silent WebM/MP4 only later. Handle rejection/decode failure; reserve frame; no blocking video or automatic download | Preferred later cinematic production candidate when realism is paramount; desktop-only opt-in; mobile still |
| Lazy React Three Fiber / Three.js | Real geometry, material/environment lighting and camera response can create dynamic reflections, at the cost of runtime, scene assets, GPU memory and context-loss risk | Client-only isolated chunk after explicit Play/eligibility; no renderer import into initial shell/SSG. Error boundary/context fallback to still; demand rendering and resource disposal; HTML stays outside canvas | Conditional later experiment only; separate approved decision and schedule impact, compatibility/CSP/asset proof and all gates required |

CSS 3D transforms arrange flat elements with perspective; they do not create physical material reflection simulation. Grouping properties can flatten a preserve-3d subtree, so separate clipping/opacity wrappers from the transformed scene and validate the actual browser result. [CSSWG transform model](https://www.w3.org/TR/css-transforms-2/).

For optimized media, use a silent file with no audio track, playsinline and no autoplay; request/decode after Play, preserve the poster if playback is refused. A crossfade to a matching final still may be used only in the later non-reduced variant. Keep pointer depth optional on the outer scene frame rather than claiming a video supplies a fully interactive camera. [Browser media guidance](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Autoplay).

For a future R3F proof, start with one scene, two door meshes plus simple portal/cabin geometry, baked soft lighting and one small environment map. Avoid real-time shadow maps, postprocessing, SSAO/bloom, particles and multiple canvases. Propose DPR capped at 1.5, then lower to 1 if measured costs demand it; frameloop demand with explicit invalidation only during motion, stop at rest/out of view, dispose on route change. Verify compatibility with the then-pinned React/rendering stack before choosing versions. R3F documents demand rendering and Canvas fallback/error handling; these support an experiment, not evidence of passing KEN's mobile budgets. [R3F performance](https://r3f.docs.pmnd.rs/advanced/scaling-performance), [R3F Canvas fallback](https://r3f.docs.pmnd.rs/api/canvas).

**Decision:** ship the static architectural treatment in Phase 1. In separately approved Phase 3/P1-F003 work, compare CSS depth with a short pre-rendered-media proof using the same storyboard and poster. Choose media if measured realism outweighs its opt-in bytes; choose CSS if the approved visual target accepts simulated reflections. Advance to R3F only when an approved requirement needs interactive material/camera behavior that those proofs cannot deliver. None of these later paths may delay or degrade secure inquiry/navigation or silently change the foundation task scope.

## 9. Performance constraints and measurement

The existing quality-strategy.md profile, budgets and agreement gate remain authoritative. The new type/media design must fit them; this document grants no budget increase.

| Initial compressed/actual-transfer budget | Home | Contact | Privacy/preparation |
|---|---:|---:|---:|
| First-party shared + route JS, gzip | ≤150 KiB | ≤180 KiB | ≤150 KiB |
| Route-used CSS, gzip | ≤30 KiB | ≤30 KiB | ≤30 KiB |
| Selected-locale WOFF2, actual bytes | ≤120 KiB | ≤120 KiB | ≤120 KiB |
| Mobile above-fold selected imagery | ≤200 KiB | ≤80 KiB | ≤80 KiB |
| Initial first-party total, including HTML/data/fonts/media | ≤550 KiB | ≤450 KiB | ≤450 KiB |

The individual maxima cannot all be spent if their sum breaks the total. Count a cold route's shared chunks once and all actually requested locale/mixed-script fonts. No media/fonts have been measured here. Use responsive AVIF/WebP with JPEG fallback, width/height/aspect-ratio reservation, high fetch priority only for the selected critical hero, lazy below-fold images and no preload of cinematic assets. Avoid duplicate poster and video downloads before an explicit later request.

Acceptance remains Lighthouse mobile performance ≥90 and accessibility ≥95 per required template/locale, lab LCP≤2.5s, CLS≤0.10 and interaction≤200ms, with H1/primary CTA usable within two seconds where practicable. Profile proposal: 390×844, DPR1, 4× CPU slowdown, 150ms RTT, 1600Kbps down/750Kbps up, cold cache, no warm worker, five runs per Home/Contact locale. QA/Product Owner freeze actual tool/hardware/throttling settings before acceptance. Turnstile is separately reported and included in hosted speed measurements. Lab results are not field p75, TBT is not INP, and no field sample/pass is inferred.

**Later proof-only proposed caps:** CSS cinematic addition ≤12 KiB gzip JS+CSS and ≤250 KiB additional texture transfer; one requested rendered clip ≤1.5 MiB; R3F addition ≤300 KiB gzip runtime and ≤1 MiB combined compressed geometry/textures/environment. These are separate opt-in experiment rejection limits, not Phase 1 budgets, demonstrated feasibility or approved allowances. Set final budgets under DEP-12 before any later implementation; if a cap is impractical, simplify or retain the static treatment rather than silently raise it.

Later effect asset requests must be absent on Phase 1, mobile, reduced-motion and failed-eligibility traces. On an approved desktop variant, keep the static initial-route budget unchanged; start optional transfer after explicit Play and stop deferred work on navigation/cancel. Measure cold initial load and active playback separately, including parse/compile/decode/upload cost, memory, interaction delays, context loss and offscreen behavior. Proposal for a later proof: nominal 60fps, investigate sustained frames >33ms, zero effect-attributed main-thread tasks >50ms, no additional CLS and no >200ms critical interaction. These are investigation/acceptance candidates requiring QA agreement, not claimed results or substitutes for release baselines.

## 10. Approval and acceptance criteria

### 10.1 Phase 1 design gate

| Evidence to approve | Owner role / existing anchors | Pass criterion / current status |
|---|---|---|
| Five-section wireframes with integrated six choices and project inset | Designer/KEN/Product Owner; T082/T085/T090, DEP-02 | Paired desktop/mobile review; FR-005 satisfied; prominence choices accepted. Proposed, not approved |
| Palette and component states | Designer/QA/KEN; T015/T079/T089/T090 | Rendered contrast/focus/disabled/error states pass; no gold-on-ivory essential text/control; tested five widths. Calculated pairings only |
| Font provenance and shaping | Designer/Content/QA; T084/T089/T090, DEP-02/12 | Exact license/binary/subset record, no broken joining/diacritics, fallback/zoom/slow-font review and ≤120 KiB or documented approved exception. Source license research only |
| Hero/editorial/project rights | KEN/Content/Designer; T083/T085/T091, DEP-09 | Supplied rights and classification; explicit illustrative/preparation wording; no fabricated project evidence. Assets pending |
| Bilingual copy and preparation states | Native editors/Legal/KEN; T059/T091, DEP-03 | Every visible string/alt/metadata reviewed; benefit themes approved or preparation; privacy fixtures remain synthetic. Pending |
| Accessibility and usability | QA/Product Owner; T080/T088/T089/T100/T104/T105 | Keyboard/NVDA/VoiceOver, reduced motion/media failure, responsive/reflow and ≥10 representative users; existing completion/trust thresholds. Not executed |
| Performance | Frontend/QA/Product Owner; T020/T088/T101–T103, DEP-12 | Agreed profile, complete cold route budget evidence and speed/interaction baselines; no advanced effect bytes. Not measured |
| Exact candidate acceptance | Product Owner/QA/KEN; T092/T108/T117 | Revision-linked decision and applicable external gates genuinely closed; no production/data/launch authorization implied. Pending |

### 10.2 Separate later cinematic gate

Before later effect implementation, record the chosen approach, approved storyboard/material reference, rights, effort/schedule impact and scope/architecture decision under P1-F003. Assign later tasks in that feature's plan, not by expanding T087 or adding mandatory R3F to T002. Obtain Designer/KEN/Product Owner approval plus Frontend/QA feasibility evidence; identify named individuals only when actually assigned.

A later candidate passes only if initial SSG/CTA/navigation/form behavior is unchanged; mobile/reduced/no-JS/context/media-error variants are readable and static; Play/Stop/Replay/Motion off are keyboard accessible/localized; no audio/loop/scroll takeover; requested bytes fit agreed budgets; critical active-playback interactions and release performance remain within baselines; idle/out-of-view resource cleanup is demonstrated. If it fails, retain the still. Production remains behind all existing privacy/content/gallery/contact/operational/launch gates.

## 11. Existing task impact and consistency review

No tasks are added, removed, reordered, marked complete or renumbered. Clarify the relevant existing task descriptions to consume this design direction; all listed verification remains future work.

| Existing task anchors | Impact |
|---|---|
| T015/T016 | Consume new provisional palette/type/layout/state rules; semantic form controls remain intact |
| T079/T080/T081 | Verify five-section arrangement, six service choices, inline project/preparation status, accessible CTA/resilience and solid/rendered contrast |
| T082/T085 | Author/compose concise paired Home content under these wireframes, with preparation treatment for unavailable benefit/service/project facts |
| T083/T084 | Preserve media/font rights, responsive derivatives, shaping, locale font budget and honest still/system fallback; licenses require exact-file verification |
| T087 | Remains 120–180ms decorative color/opacity only; later storyboard explicitly excluded |
| T088/T089/T090/T091/T092 | Review budgets, responsive/manual accessibility, proposed direction/rights and independent native copy; no approval fabricated |
| T020/T100–T105/T108/T112/T116/T117 | Existing budget/device/usability/approval/scope/handoff/acceptance gates apply; no new mandatory cinematic implementation |

Plan/research supersede their earlier provisional colors and Noto/Inter/Cormorant proposal. quality-strategy.md adds design-specific review cases under unchanged budgets. dependencies.md records this candidate under existing DEP-02/03/09/12 rather than creating new approval IDs. tasks.md references the direction in its input and relevant existing descriptions. The historical analysis-report.md stays untouched and is not represented as a new analysis result.

**Scope conflicts resolved:** three featured cards do not replace six service choices; five editorial sections do not remove the honest project-preview requirement; proposed benefit language does not establish company facts; requested type does not authorize exceeding font budgets; realistic 3D/camera/parallax does not become Phase 1 mandatory work. The remaining dependencies are explicit approval/asset/measurement gates, not invented passes.

**Review readiness:** design decisions, fallbacks, phase boundaries and task mapping are documented for a fresh non-destructive speckit-analyze run including this artifact. This documentation task does not run that workflow, implement the website, install dependencies, deploy, commit, push or modify the PRD/constitution. Stop after documentation validation; application work requires a later explicit request.

## 12. Documentation validation record — 2026-10-13

Verified after writing: 117 unique task IDs T001–T117 remain unchecked; original dependency strings and 45 parallel markers are unchanged. Only T015/T079/T081/T082/T084/T085/T087/T090 task descriptions were clarified. Local Markdown links resolve, fences are balanced and no unintended trailing whitespace was found. Whole-workspace before/after SHA-256 comparison shows only plan.md, tasks.md, quality-strategy.md, research.md and dependencies.md modified, plus this new file; every other pre-existing file is byte-preserved, including spec.md, analysis-report.md and the remediation contracts. Protected PRD/constitution hashes and branch HEAD remain unchanged.

Source font licensing/metadata and technical references were browsed; solid palette ratios were calculated. These checks establish documentation integrity only. Exact font/media binaries, browser rendering, actual performance and accessibility still need their existing implementation/review gates. No application test/build, package install, provisioning, deployment, commit/push or fresh speckit-analyze run occurred. The earlier shell reader had intermittent setup-refresh errors; local filesystem verification completed through the Node tool. No pass was inferred from failed shell calls.
