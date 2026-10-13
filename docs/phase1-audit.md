# MSITU Consults — Phase 1: Discovery & Audit

**Source audited:** `msitu_website_v2.html` (538 lines, single file, inline CSS, no JavaScript beyond one inline `onclick`). The original file is untouched.
**Preview produced:** `msitu_website_v3.html` (working version, not for publication).
**Date:** 13 October 2026

---

## 1. Website audit

### 1.1 What works and should stay
- **Brand system:** plum (#7B2D6E / #4F1C47) with green (#5A9E2F / #3D6E20) is distinctive. No other Ugandan benchmark I reviewed uses plum, so it sets MSITU apart from the usual all-green consultancy look.
- **Typography:** Lora with Outfit reads as corporate and approachable. Keep both.
- **Content depth:** eight services with specific sub-scopes (ESIS, HAZOP, QRA, ESS5), six sectors with concrete facility types, eight named projects with locations. This is more substantive than most benchmarks.
- **CSS custom properties** already exist, so tokenising the design is cheap.

### 1.2 Defects found

| # | Area | Finding | Severity |
|---|------|---------|----------|
| D1 | Functionality | The **Send Message** button only changes its own label. Nothing is submitted, yet the visitor is told "Message sent". Enquiries are silently lost. | **Critical** |
| D2 | Mobile | `.nav-links{display:none}` below 900px with no replacement. Mobile users have no navigation except the CTA. | **Critical** |
| D3 | Forms / a11y | `<label>` elements are not linked to inputs (no `for`/`id`). There's no `<form>`, no `name` attributes, no validation, no phone field and no consent checkbox. | High |
| D4 | Content accuracy | "10+ Years Experience" contradicts "Est. 2011", which is 15 years at 2026. "6+ Service Disciplines" (hero) contradicts "8+" (stats), and the site lists 8 services. | High |
| D5 | Content accuracy | World Bank and IFC are listed under **clients**. They appear elsewhere as *standards*. This implies a client relationship that may not exist. | High |
| D6 | Content accuracy | The "ISO 14001" badge sits beside "NEMA Certified" and "PPDA Registered", which implies MSITU holds ISO 14001 certification. The cert bar says "ISO 14001 *Expertise*". These conflict. | High |
| D7 | Claims | "Uganda's **Leading**" and "the ideal partner" are unverifiable superlatives. They're also weak for institutional buyers, who discount them. | Medium |
| D8 | Navigation | All service "Enquire →" links go to `#contact` without context. There are no service pages, no Insights section and no dropdowns. | Medium |
| D9 | SEO | No meta description, canonical, Open Graph or structured data. One `<h1>`, but the About card uses an `<h2>` styled inline. | Medium |
| D10 | a11y | Decorative SVGs have no `aria-hidden`. There's no `:focus-visible` style (`outline:none` on inputs), no skip link and no `prefers-reduced-motion` handling. | Medium |
| D11 | a11y / contrast | White text on `#5A9E2F` (`.btn-green`, `.nav-cta`) is about **3.3:1**, which fails WCAG AA for body-size text. `rgba(255,255,255,.45–.5)` footer text on `#2d0e28` is borderline. | Medium |
| D12 | Code | Heavy inline styles (sectors header, about card), and the hero has a duplicated inline `padding`. There are also several near-identical label/heading patterns. | Low |
| D13 | Footer | Copyright is hard-coded to © 2025. There are no Privacy or Terms links, even though the site collects personal data. | Low |
| D14 | Performance | Google Fonts are loaded without `preconnect`. Otherwise the page is light because it has no images. | Low |
| D15 | Imagery | There are no photographs. The hero is a gradient, so the site gives no visual evidence of fieldwork in Uganda. | Medium (content dependency) |

### 1.3 Responsiveness (static review of v2)
- At **<900px**, the nav disappears (D2). Grids collapse sensibly.
- At **360px**, the hero `h1` with a forced `<br>` wraps awkwardly, and the four hero stats wrap into an uneven 3+1 layout.
- No horizontal overflow, because `overflow-x:hidden` is set on the body. That setting can also *mask* overflow bugs, so v3 removes it.

---

## 2. Benchmark report

**Method:** each homepage was fetched live on 13 Oct 2026 and summarised. I did not copy any layouts, text or images.
**Limitations:**
- `sdpc.co.ug` did not resolve (DNS failure), so it is not assessed.
- `nema.go.ug` only renders through JavaScript, so the fetch returned a loading screen. The NEMA guidance below comes from general knowledge of the regulatory framework and **must be checked against NEMA's site** before publication.
- `ifc.org` was not fetched. The IFC Performance Standards (PS1–PS8) are well documented publicly.

| Site | Useful patterns | Weaknesses to avoid |
|------|-----------------|---------------------|
| **Tenvicon** | Strongest benchmark. Services dropdown, highlighted "Request Quote" header button, project cards showing **sector, client, location and year**, real field photography, a separate quote page and a working contact form. | Busy homepage (3D gallery, videos, ticker); too many sections. |
| **Eco & Partner** | Clear grouping of services and sectors with "read more" detail pages. Dedicated *Commitments* pages (SHEQ, Sustainability, Human Rights) signal governance maturity. | Placeholder images. Projects aren't shown on the homepage. Two competing menus. |
| **Nova Consult** | Four-step "How We Work" process and a team preview build trust. | Counters show "00+" placeholders. Every service card links to the same page. |
| **BIMCO** | Services dropdown, "Why choose" blocks and a sector image grid. The cookie banner has granular toggles. | Stock photography. Template placeholders in the hero slider. No project evidence on the homepage. |
| **GreenLife** | **Downloadable company profile** in the hero, plus a downloadable checklist as a lead magnet. | "0+" counters, off-brand template testimonials and a typo in the email domain. Credibility damage from unfinished content. |

**Takeaways for MSITU**
1. **Projects are the gap in the market.** Only Tenvicon shows project evidence well. MSITU already has eight named, located projects, so put them on the homepage with sector, location and service tags.
2. **Unfinished content is the most common credibility failure** (placeholder counters, template testimonials). MSITU should publish fewer claims, all verified, rather than more claims that aren't.
3. **A Request Consultation button in the header, a services dropdown and a real form** are table stakes. Only one benchmark has a working form on the homepage.
4. **Regulatory guidance is unclaimed territory.** No benchmark explains *which approval a project might need*. That is MSITU's differentiator.
5. **Downloadable profile** (GreenLife) is a cheap, useful addition once an approved PDF exists.

---

## 3. Content verification register

These items appear in v2 and are flagged in the v3 preview with the "Highlight unverified" toggle. **Each needs sign-off from MSITU before it goes public.**

| # | Claim | Where | What to confirm | v3 treatment |
|---|-------|-------|-----------------|--------------|
| V1 | Established 2011 | Hero, about, stats | Certificate of incorporation date | Kept, flagged |
| V2 | "NEMA Certified" firm | Hero, cert bar, why-us | NEMA certifies **practitioners** and registers firms. Confirm the exact status and wording, and the certificate number if it will be shown | Reworded to "NEMA-registered environmental practitioners", flagged |
| V3 | PPDA registered | Hero, cert bar | Current PPDA registration and validity | Kept, flagged |
| V4 | URA tax compliant | Hero, about | Current certificate. Consider dropping it from marketing copy because it's routine | Moved to credentials only, flagged |
| V5 | 40+ associates | Hero, about, stats | Current associate roster count | Kept, flagged |
| V6 | 15+ completed projects | Stats | Project register count (8 are named) | Kept, flagged |
| V7 | ISO 14001 | Badge and cert bar | Certified, or advisory capability only? | Shown as "ISO 14001 implementation support" (a service), flagged |
| V8 | World Bank ESS / IFC PS / Equator Principles | Multiple | Which assignments actually applied each framework | Shown under "Frameworks we apply", with a non-endorsement note |
| V9 | World Bank and IFC as **clients** | Clients strip | Were they contracting parties? | **Removed from clients** and moved to frameworks, pending confirmation |
| V10 | Kikagati Power, SBI International, Excel Construction | Clients strip | Permission to name them; which projects | Kept, flagged |
| V11 | ARUP and ROM Transportation | BRT project | Partner role: "in association with" | Shown as **project partners**, not clients |
| V12 | BRT corridor length 25km; MKKN road 95km; Gulu–Atiak 74km; Masaka site 20ha | Projects | Project records | Kept, flagged |
| V13 | All projects "Completed" | Projects | Status per project | Kept, flagged |
| V14 | RAP *implementation* on MKKN road | Projects | Scope: study only, or implementation too? | Kept, flagged |
| V15 | Phone numbers, emails, address | Contact | Current details and the preferred enquiry inbox | Kept, flagged |
| V16 | "Uganda's leading" / "ideal partner" | Hero, why-us | Superlatives | **Removed** |
| V17 | Assist in "soliciting external project funding" | Contact | Is this still offered? | Omitted from preview, ask MSITU |
| V18 | Domain `msitu.co.ug` | Footer, canonical | Live domain ownership | Used in the canonical URL, flagged |

---

## 4. Prioritised improvement backlog

| Pri | Item | Phase | Status in v3 preview |
|-----|------|-------|----------------------|
| P0 | Real form submission with honest success and failure states (D1) | 4 | **Frontend done.** Needs an endpoint. Until one is configured, the form says plainly that nothing was sent |
| P0 | Accessible mobile menu and desktop dropdowns (D2, D8) | 3 | **Done** |
| P0 | Fix contradictory and unverified claims (D4–D7) | 1 | **Done** (reworded and flagged) |
| P0 | Form labels, validation, consent, honeypot (D3) | 3 | **Done** |
| P0 | SEO metadata and Organization JSON-LD (D9) | 3 | **Done** (homepage) |
| P0 | Contrast fixes: green buttons use #3D6E20 (D11) | 2 | **Done** |
| P0 | Service detail pages (×8) | 3 | Not started. Cards link to a pre-filled enquiry for now |
| P0 | Project portfolio and case-study template | 3 | Homepage cards plus client-side filter done. Detail pages not started |
| P0 | Authentic hero and project photography (D15) | Content | **Blocked on MSITU.** v3 uses labelled illustration placeholders |
| P1 | Regulatory guidance section | 3 | Homepage teaser done. Articles not started, copy pending technical review |
| P1 | Downloadable company profile | 4 | Blocked on an approved PDF |
| P1 | Privacy policy and terms | 3 | Footer links present, pages not written |
| P1 | Analytics (consent-aware) | 6 | Not started |
| P1 | WhatsApp contact | 3 | Not started. Needs a confirmed number |
| P1 | CMS | 4 | Recommendation below |
| P2 | Interactive project map, resource search | Future | — |

---

## 5. Recommended architecture

**Decision:** keep the homepage preview as a single static HTML file for approval (Phase 2). Then migrate to **Next.js (App Router) + TypeScript**, using static generation and **one server route** for enquiries (Phase 3–4).

**Why not stay with static HTML:** the sitemap needs about 30 pages (8 services, 6 sectors, about 8 case studies, insights). Hand-maintaining a shared nav and footer across 30 HTML files is error-prone. Templated pages fed from content files are the smallest maintainable option.

**Why not something heavier:** the site has no user accounts and no transactional data. A full headless CMS or database isn't justified yet.

| Concern | Recommendation |
|---------|----------------|
| Content | Markdown/MDX files in `content/` (services, projects, articles), validated with a typed schema. Edited through Git, or **Decap CMS / TinaCMS** for non-technical staff later (P1). |
| Enquiries | Next.js Route Handler: server-side validation (zod), honeypot plus time-trap, rate limit per IP, a Cloudflare Turnstile token check, then email through a transactional provider (e.g. Resend) to the confirmed inbox. Optional storage in a managed database if MSITU wants an enquiry log. |
| Uploads | Defer. If needed, use signed upload URLs to private object storage with type and size limits, never sent through the email body. |
| Hosting | Vercel or Cloudflare Pages, with DNS on Cloudflare. HTTPS by default and security headers (CSP, HSTS, X-Content-Type-Options, Referrer-Policy) in config. |
| Styling | Keep plain CSS custom properties, or Tailwind using the same tokens. Either works. The tokens below are the source of truth. |

The IA follows the brief's sitemap. Launch order: Home → Services ×8 → Projects → Contact → About → Sectors → Insights.

---

## 6. Homepage wireframe (as built in v3)

```
[Skip link] [Review bar: preview notice · Highlight unverified toggle]   ← preview only
┌ HEADER (sticky, condenses on scroll) ─────────────────────────────────┐
│ Logo  Home About Services▾ Sectors▾ Projects Insights Contact [Request Consultation] │
│ <900px: Logo ............................................. [☰]        │
└───────────────────────────────────────────────────────────────────────┘
HERO        H1 + lede + 2 CTAs | image frame (placeholder for approved field photo)
            Credential strip: Est. 2011 · NEMA-registered practitioners · PPDA · 40+ associates
INTRO       Who we are (2 cols): overview + disciplines list → About
SERVICES    8 cards: icon · title · summary · "Enquire about this service" (pre-fills form)
WHY MSITU   6 differentiators (2×3) + 4 verified stats
SECTORS     6 tiles on deep plum: illustration · title · 3 example facility types
PROJECTS    Filter chips (All / Transport / Water & sanitation / Waste / Energy)
            Cards: sector tag · title · location · services · summary · status
APPROACH    6-step process with connecting line (horizontal ≥1024, vertical below)
COMPLIANCE  Regulatory guidance teaser: Project brief / ESIA / Audit / ESMP + disclaimer + NEMA link
CLIENTS     3 groups: Clients · Project partners · Frameworks we apply (+ non-endorsement note)
FINAL CTA   "Planning a project?…" + 2 buttons
CONTACT     Details | Form (required fields per brief, consent, honeypot, live states)
FOOTER      Description · Quick links · Services · Contact · Privacy · Terms · © {year}
```

---

## 7. Design system specification

**Colour tokens** (from the brief, with role tokens added)

| Token | Value | Use | Contrast note |
|-------|-------|-----|---------------|
| `--brand-plum` | #7B2D6E | Headings accent, links, secondary buttons | White on it is 8.5:1 ✓ |
| `--brand-plum-dark` | #4F1C47 | Header, sector band, H2 | White on it is 12:1 ✓ |
| `--brand-plum-deep` | #2D0E28 | Footer, hero | — |
| `--brand-plum-light` | #C47DB8 | Labels on dark backgrounds only | 5.0:1 on plum-dark ✓ |
| `--environment-green` | #5A9E2F | Icons, borders, large decorative elements **only** | White on it is 3.3:1 ✗ for text |
| `--environment-green-dark` | #3D6E20 | **Primary buttons**, tags text | White on it is 6.1:1 ✓ |
| `--environment-green-light` | #8AC95A | Accents on dark backgrounds | 7.5:1 on plum-deep ✓ |
| `--background-cream` | #FAF8F5 | Page background | — |
| `--background-green` | #F3F9ED | Tags, compliance band | — |
| `--text-primary` | #1A1A1A | Body | 17:1 ✓ |
| `--text-secondary` | #5E5E5E | Secondary text (darkened from #6B6B6B for margin) | 6.3:1 on cream ✓ |
| `--border-default` | #E8E0E6 | Card borders | — |

**Typography:** Lora 600 for H1/H2/H3 display and Outfit 300–600 for everything else. Fluid scale: H1 `clamp(2.2rem, 5vw, 3.6rem)`, H2 `clamp(1.7rem, 3vw, 2.4rem)`, H3 1.05rem/600 Outfit, body 1rem/1.7, small 0.85rem. Body weight is 400 (v2 used 300, which is thin at small sizes).

**Spacing:** 4px base. Section padding is `clamp(4rem, 8vw, 6rem)` vertical. Container max-width 1200px with a 1.25rem gutter (16px+ on mobile).

**Shape and elevation:** radius 12px for inputs and chips, 16px for cards, 999px for buttons. Shadow `0 1px 2px rgba(45,14,40,.06), 0 8px 24px rgba(45,14,40,.06)` on hover only.

**Motion:** 200ms ease for hover, and a 450ms fade-up reveal on scroll that runs once. Everything is disabled under `prefers-reduced-motion`.

**Components:** `btn` (primary green-dark, secondary plum outline, ghost-on-dark), `sec-label`, `card`, `tag`, `chip` (filter, `aria-pressed`), `field` (label, input, hint, error), `nav-dropdown` (button with `aria-expanded`), `mobile-drawer`.

---

## 8. Phased implementation plan

| Phase | Scope | Exit criteria | Needs from MSITU |
|-------|-------|---------------|------------------|
| **1. Audit** ✅ | This document | Reviewed | — |
| **2. Homepage design** ← *now* | `msitu_website_v3.html` preview | MSITU approves layout, tone and claims wording | Answers to verification register V1–V18 |
| 3. Frontend build | Next.js scaffold, shared layout, 8 service pages, project portfolio and case-study template, About, Contact, Privacy and Terms | All links resolve, responsive at 360–1920, Lighthouse a11y ≥95 | Service copy review, project details, photos, logo SVG |
| 4. Business functions | Enquiry route (validation, Turnstile, rate limit, email), quote workflow, profile download, CMS | A test enquiry arrives in the confirmed inbox, and a failure path is shown honestly | Enquiry inbox, email provider account, profile PDF |
| 5. QA | Keyboard, screen reader spot-check, Lighthouse, security headers, content accuracy | QA report with no open P0 issues | Final content sign-off |
| 6. Deploy | Domain, HTTPS, env vars, analytics, admin docs | Production form verified | DNS access for msitu.co.ug |
