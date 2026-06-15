# Supra Origin AI — Implementation Plan

## Project Overview

| Field | Detail |
|---|---|
| **Company** | Supra Origin AI Private Limited |
| **Website** | https://www.supraorigin.com |
| **Type** | B2B Technology Services — Static HTML/CSS/JS Website |
| **Repository** | https://github.com/aug31ajay/supra.git |
| **Deployment** | GitHub Actions → SSH → cPanel public_html |
| **Email** | thesupraoriginai@gmail.com |
| **Phone (RFID / Attendance)** | +91-89543-32272 — Call + WhatsApp (India RFID & Attendance only) |
| **Phone (All Clients)** | +91-89543-32282 — Call + WhatsApp (India local + International clients) |
| **Business Hours** | Mon–Sat, 9:00 AM – 6:00 PM IST |
| **Social** | Instagram: @supraoriginai · Facebook: /profile.php?id=61579569406102 |

---

## Target Audience Strategy

| Audience | Primary Page | Language / Tone |
|---|---|---|
| **International (US, UK, EU, etc.)** | `index.html` — Homepage | Global English; AI, software, cloud, digital transformation |
| **US Healthcare / Medical IT** | `medical-services.html` | Healthcare English; CPT, MIPS, HIPAA, EDI, telehealth |
| **India — RFID / Biometric Attendance** | `attendance-solutions.html` | India-market English; hardware-first; price/installation focus |
| **India — General / Local B2B** | `index.html` (contact: +91-89543-32282) | Software + AI services; pan-India delivery |

The homepage (`index.html`) leads with globally relevant services (AI, software, cloud) and surfaces industry-specific products (RFID, Medical Domain) via the Services dropdown and "India Market" / "Medical IT" chips — not in the hero or above-the-fold areas.

---

## File Structure

```
supra/
├── index.html                        # Global homepage — AI, software, cloud (international-first)
├── attendance-solutions.html         # India-focused RFID/Biometric landing page
├── medical-services.html             # US Healthcare IT — CPT, MIPS, PQRS, EDI, Telehealth, EHR
├── robots.txt                        # Allow all; points to sitemap
├── sitemap.xml                       # 3 URLs (lastmod updated on every deploy)
├── .cpanel.yml                       # Legacy deploy config
├── .github/
│   └── workflows/
│       └── deploy.yml                # GitHub Actions SSH deploy (port 22999)
├── feature/
│   └── implementation-plan.md        # This file — single authoritative implementation plan
├── Images/
│   ├── Banner.jpeg                   # RFID/attendance hero (attendance page + gallery)
│   ├── webposter1.jpeg               # OG image for homepage; banner slider slide 1
│   ├── Webposter2.jpeg               # Slider / promo image 2; gallery
│   ├── Webposter3.jpeg               # Slider / promo image 3; gallery
│   ├── rfid-card.png                 # Product: RFID ID card (attendance teaser + gallery)
│   ├── rfid-reader.png               # Product: RFID reader (attendance teaser + gallery)
│   └── biometric-device.png          # Product: Biometric device (attendance teaser + gallery)
└── logo/
    ├── logo-transparent-png.png      # Primary logo — navbar + footer (both pages)
    ├── logo-transparent-svg.svg      # SVG variant (available, not currently linked in HTML)
    ├── logo-transparent-pdf.pdf      # PDF export
    ├── logo-png.png                  # On white/solid background (not linked)
    ├── logo-svg.svg                  # Solid background SVG
    └── logo-pdf.pdf                  # Solid background PDF / brand kit only
```

**Note:** Logo rendered circular in navbar via `border-radius: 50%` — keep in mind if a rectangular variant is ever needed.

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| Markup | HTML5 | Semantic tags, Schema.org structured data inline |
| Styling | CSS3 | Inline per file; CSS custom properties, Flexbox, Grid, clamp() |
| Scripting | Vanilla JavaScript | Inline at bottom of each HTML file |
| Icons | Font Awesome 6.5.0 | CDN (cdnjs.cloudflare.com) |
| Fonts | Google Fonts — Inter | Weights 300–900; preconnect links in `<head>` |
| Analytics | Google Analytics 4 | ID: `G-2SQW40RNQ8` (both pages — fixed June 2026) |
| Form Backend | Web3Forms API | Key: `4b0e582e-ec70-4079-9610-a190fe5c5033`; delivers to Gmail |
| Chat / CTA | WhatsApp API | Two numbers — see Contact Strategy below |
| Hosting | cPanel | Domain: supraorigin.com; user: `pndmddgq` |
| CI/CD | GitHub Actions | `deploy.yml` on push to `main` |

---

## CSS Design System (shared across both pages)

### Color Tokens (CSS Custom Properties)
```css
--bg-base:    #f0f5ff   /* Page background */
--bg-raised:  #e8effd   /* Alternate section background */
--bg-card:    #ffffff   /* Card backgrounds */
--purple:     #2563eb   /* Primary brand blue */
--cyan:       #0ea5e9   /* Accent / secondary */
--gradient:   linear-gradient(135deg, #2563eb 0%, #0ea5e9 100%)
--gradient2:  linear-gradient(135deg, #1e40af 0%, #2563eb 55%, #0ea5e9 100%)
--text:       #0f172a   /* Main body text */
--muted:      #64748b   /* Secondary / helper text */
--border:     rgba(37,99,235,0.12)
```

### Spacing & Shape
- `--nav-h: 68px` · `--topbar-h: 40px` (index.html only)
- Radius: `--radius-sm: 10px` · `--radius-md: 16px` · `--radius-lg: 22px`
- Transition: `--transition: 0.3s ease`
- Shadow scale: `--shadow-sm` / `--shadow-md` / `--shadow-lg`

### Responsive Breakpoints
| Breakpoint | Behaviour |
|---|---|
| `≤ 968px` | Hero splits to single column; right visual panel hidden |
| `≤ 900px` | About / Contact / attendance grids stack; footer collapses to 2-column |
| `≤ 768px` | Hamburger menu activates; form rows go single column |
| `≤ 640px` | Topbar text hidden; gallery/products reflow |
| `≤ 520px` | Footer single column; industry grid 2-col |

### Animation Inventory
| Name | Element | Notes |
|---|---|---|
| `fadeUp` | Hero text, badges | 0.9s, staggered with 0.3s delay |
| `fade-in-up` | All sections | Triggered by IntersectionObserver on scroll |
| `rise` | Particles | 45–50 elements, randomised size/speed/delay |
| `ping` | Badge dot, online badge | Pulsing ring effect |
| `spinRing` | Hero visual rings | 3 rings, 17s / 26s / 44s; one reversed |
| `orbPulse` | Hero orb | Box-shadow breathing, 3s loop |
| `floatA/B` | Floating cards | -10px / -7px translateY, 3.5–4.6s |
| `count-up` | Stat numbers | JS-driven; triggers once on viewport entry |
| `waPulse` | Floating WhatsApp button | Box-shadow pulse, 2.8s loop |

---

## Contact & WhatsApp Strategy

### Phone Number Roles
| Number | Role | Usage |
|---|---|---|
| **+91-89543-32272** | RFID & Attendance Enquiries | Call + WhatsApp button on `attendance-solutions.html` only |
| **+91-89543-32282** | All Other Clients (India + International) | Call + WhatsApp button on `index.html`; also in footer of both pages as global number |

### WhatsApp Deep Links
```
RFID/Attendance (attendance-solutions.html):
https://wa.me/918954332272?text=Hi%2C%20I%27m%20interested%20in%20your%20RFID%20%2F%20Biometric%20Attendance%20solutions.

All Clients / International (index.html):
https://wa.me/918954332282?text=Hi%2C%20I%27m%20interested%20in%20Supra%20Origin%20AI%27s%20services.%20Please%20get%20in%20touch.
```

### Contact Display Per Page
**index.html** (global):
- Primary: +91-89543-32282 (all inquiries — click-to-call + WhatsApp)
- Secondary (small text): +91-89543-32272 (RFID/Attendance enquiries only)

**attendance-solutions.html**:
- Primary: +91-89543-32272 (attendance enquiries — call + WhatsApp)
- Secondary (small text): +91-89543-32282 (general / other queries)

---

## JavaScript Features

| Feature | Function/IIFE | Notes |
|---|---|---|
| Animated particles | `spawnParticles()` IIFE | 45–50 particles, randomised size (1–4px), speed (9–25s), delay (0–12s), opacity |
| Scroll reveal | `IntersectionObserver` | Threshold 0.12, rootMargin -50px bottom; stagger 90ms per element |
| Navbar scroll effect | `scroll` event | > 60px → `.scrolled` class + active link colour |
| Mobile menu | `toggleNav()` | Toggles `.open` on `#navLinks`; closes on any link click |
| FAQ accordion | `toggleFaq(el)` | Closes all open items before opening selected |
| Banner slider | `initBanner()` IIFE | 4500ms auto, pause on hover, touch swipe, dot + arrow controls |
| Image lightbox | IIFE in `<body>` | Group mode (`data-lb-group`), keyboard nav (Esc/←/→), touch swipe >50px, backdrop-click close |
| Number counters | `initCounters()` IIFE | `data-target` attr; 1400ms duration; 16ms tick; triggers once on viewport entry |
| Contact form | `handleSubmit(event)` | Async POST to Web3Forms; loading state; success/error banners; GA4 `form_submit` event |
| Scroll-to-top | `scrollToTop()` | `window.scrollTo({ top:0, behavior:'smooth' })` |
| Top bar dismiss | `dismissTopBar()` | Hides bar, shifts navbar, resets `--topbar-h` CSS variable to 0px |
| GA4 tracking | `trackEvent()` wrapper | Fires on: CTA clicks, WhatsApp link clicks, phone clicks, attendance page visits, form submit |
| Solution dropdown reveal | `handleSolutionChange()` | attendance-solutions.html only; shows/hides "Other" text field with smooth animation |

**No structural JS changes needed for new sections**: `#attendance-teaser` and `#insights` are static and use existing IntersectionObserver for scroll-reveal.

---

## GA4 Events Reference

| Event Name | Trigger | Label |
|---|---|---|
| `form_submit` | Contact form submit | page context |
| `whatsapp_click` | Any WhatsApp CTA | `hero_cta`, `teaser_whatsapp`, `contact_section`, `floating_button`, `prefooter_cta` |
| `cta_click` | `.btn-primary`, `.btn-glow`, `.ctap-btn-primary` | button text (first 40 chars) |
| `attendance_page_visit` | Click → attendance-solutions.html | `teaser_section`, `services_card`, `insights_section` |
| `phone_click` | Click on any `tel:` link | number clicked |

---

## Page: `index.html` — Section Inventory (Current State)

| # | Section ID | Description | Status |
|---|---|---|---|
| 1 | `#top-bar` | Announcement bar | Updated to global copy |
| 2 | `#navbar` | Navigation | CTA updated to "Get a Free Quote" |
| 3 | `#home` | Hero | RFID thumbnails removed; global copy + WhatsApp 32282 CTAs |
| 4 | `#stats-bar` | Key stats strip | Unchanged |
| 5 | `#banner-slider` | Image slider (3 slides) | Unchanged |
| 6 | `#about` | About | Existing global copy retained |
| 7 | `#services` | Services (9 cards) | 2 new "India Market" badge cards added (RFID + Biometric) |
| 8 | `#technologies` | Tech stack grid | Unchanged |
| 9 | `#industries` | Industries served | Unchanged |
| 10 | — | `#global-reach` strip REMOVED — false "Trusted by Clients Across" claim not appropriate for a startup | **REMOVED** |
| 11 | `#why-us` | Why Choose Us (6 cards) | Last card updated to "Global-Ready Delivery" |
| 12 | `#insights` | Article teasers (3 cards) | **NEW** — SEO keyword density section |
| 13 | `#faq` | FAQ (6 items) | Replaced India-only Q&As with global + India mix |
| 14 | `#contact` | Contact form | Both numbers shown without routing labels; WhatsApp 32282 |
| — | `#cta-prefooter` | Pre-footer CTA strip | WhatsApp updated to 32282 |
| — | Footer | 4-column footer | Both numbers listed; no routing labels |
| — | `#wa-float` | Floating WhatsApp button | Updated to 32282 |

### Navigation Links Order
Home · About · **Services (dropdown)** · Technologies · Industries · Why Us · FAQ · **"Get a Free Quote"** CTA pill

**Services Dropdown Groups:**
- AI & Technology: Artificial Intelligence, Machine Learning, Custom Software, Web Applications, Mobile Apps, Cloud Solutions, Data Analytics
- Industry Solutions: Medical Domain → `medical-services.html` | RFID Attendance → `attendance-solutions.html`

**Nav changes (June 2026):** Standalone "Attendance" link removed from top level; Services link is now a grouped dropdown (desktop: CSS hover; mobile: JS `.dd-open` class toggle + `max-height` animation). Medical IT hero chip added to hero section.

---

## Page: `attendance-solutions.html` — Section Inventory

| Section | Description | Status |
|---|---|---|
| Hero (`#hero`) | Dark navy; badge; H1; sub-text; 2 CTAs; 3 stat counters | Unchanged content |
| Benefits (`#benefits`) | 6 benefit cards | Unchanged |
| Services (`#services`) | 4 cards — RFID, Biometric, Software, Installation | Unchanged |
| Why Choose Us (`#why-us`) | 6 cards with icon + title + text | Unchanged |
| Gallery (`#gallery`) | 3-column; 6 images; click opens lightbox | Unchanged |
| Process (`#process`) | 6-step horizontal timeline | Unchanged |
| CTA Banner (`#cta`) | Dark bg, WhatsApp CTA | WhatsApp message updated |
| FAQ (`#faq`) | 6 items, accordion | Unchanged |
| Contact (`#contact`) | 2-column; primary 32272; secondary 32282 | Phone labels updated |
| Footer | 3-column; both numbers labelled | Labels added |
| `#wa-float` | Floating WhatsApp button | Message standardised to attendance pre-fill |

### Attendance Contact Form Fields
- Full Name (required), Organisation, Phone (required), Email
- **Solution Required** dropdown: RFID ID Cards Only / Biometric Attendance Device / Attendance Management Software / Complete System / Annual Maintenance Contract / Other
- "Other" selection reveals a "Please Specify" field via `handleSolutionChange()`
- Message / Requirements textarea
- Form subject: `"New Attendance Solution Enquiry — Supra Origin AI"`

---

## Page: `medical-services.html` — Section Inventory

| # | Section ID | Description | Status |
|---|---|---|---|
| 1 | `#navbar` | Same Services dropdown as index.html (index.html# hrefs); Medical Domain marked `.dd-active` | ✅ Created |
| 2 | `#hero` | Dark green gradient; HIPAA badge; H1 "Medical Domain Technology Expertise"; sub-text; 2 CTAs; 4 stat counters; visual card panel (desktop) | ✅ Created |
| 3 | `#services` | 8 service cards — CPT Coding, MIPS, PQRS, Appointment Scheduling, Telehealth, EDI 270/271, EDI 837/835, EHR Integration | ✅ Created |
| — | `#hipaa-banner` | Dark green compliance strip — HIPAA, HL7/FHIR, ICD-10/CPT, Secure Cloud | ✅ Created |
| 4 | `#why-us` | 6 advantage cards — HIPAA-First, US Healthcare Knowledge, HL7/FHIR, AI Coding, India-Based, End-to-End | ✅ Created |
| 5 | `#tech-stack` | 10 tech cells — HL7 FHIR, HIPAA, ICD-10/CPT, EDI X12, Azure Health APIs, WebRTC/Twilio, Python/AI, .NET Core, React, SQL | ✅ Created |
| 6 | `#process` | 6-step process — Discovery, Architecture, Development, HIPAA Audit, Deployment, Support | ✅ Created |
| 7 | `#faq` | 6 FAQs — US healthcare experience, HIPAA compliance, EHR integration, EDI transactions, telehealth platforms, MIPS explained | ✅ Created |
| 8 | `#contact` | 2-column; both numbers; WhatsApp 32282; Web3Forms (subject: "New Medical Domain Enquiry") | ✅ Created |
| — | Footer | 3-column dark footer with social links; links to index.html + attendance-solutions.html | ✅ Created |
| — | `#wa-float` | Floating WhatsApp — 32282 with medical pre-fill message | ✅ Created |

### Medical Page Design Language
- **Primary color**: `--green: #059669` / `--green-lt: #10b981` (overrides blue on this page)
- **Gradient**: `linear-gradient(135deg, #059669, #0ea5e9)` — green to cyan
- **Hero background**: `linear-gradient(160deg, #071c12, #0a2818, #061510, #020d08)` — dark green/forest
- **Schema.org**: `ProfessionalService` + `FAQPage` (6 Qs)
- **WhatsApp**: 32282 with medical-specific pre-fill
- **Form subject**: `"New Medical Domain Enquiry — Supra Origin AI"`

---

## SEO Reference

### Target Keywords

#### International / Global (index.html)
| Keyword | Priority |
|---|---|
| AI solutions company India | High |
| custom software development India | High |
| hire AI developers India | High |
| software development company India for US clients | High |
| offshore software development AI | High |
| web app development company India | Medium |
| machine learning solutions for business | Medium |
| cloud software development India | Medium |
| Python AI development company | Medium |
| digital transformation services India | Medium |

#### Healthcare / Medical IT (medical-services.html)
| Keyword | Priority |
|---|---|
| medical IT solutions India | High |
| CPT coding software India | High |
| MIPS reporting software | High |
| PQRS automation | High |
| telehealth platform development India | High |
| EDI 270 eligibility verification software | High |
| EDI 837 claims software | High |
| EHR integration services India | High |
| HIPAA compliant software development | High |
| healthcare software development India | Medium |
| appointment scheduling software medical | Medium |
| HL7 FHIR integration services | Medium |

#### India / Local (attendance-solutions.html)
| Keyword | Priority |
|---|---|
| RFID attendance system India | High |
| biometric attendance device supplier | High |
| RFID smart ID card India | High |
| attendance management software India | High |
| RFID card printing India | High |
| bulk RFID cards manufacturer India | High |
| school attendance system RFID | Medium |
| corporate biometric attendance | Medium |

#### Brand Keywords (both pages)
| Keyword | Priority |
|---|---|
| Supra Origin AI | Critical |
| SupraOrigin | Critical |
| supraorigin.com | Critical |
| Supra Origin attendance | High |
| Supra Origin RFID | High |

### Technical SEO — Current State
| Item | index.html | attendance-solutions.html |
|---|---|---|
| Item | index.html | attendance-solutions.html | medical-services.html |
|---|---|---|---|
| `<title>` | AI Solutions, Custom Software & Digital Transformation | RFID Attendance System & Biometric Devices | Medical Domain IT Solutions — CPT, MIPS, Telehealth, EDI |
| `<meta description>` | Global AI, software, cloud, free consultation | RFID cards, biometric devices, pan-India, +91-89543-32272 | CPT coding, MIPS, PQRS, telehealth, EDI 270/837, EHR integration |
| Canonical | ✅ | ✅ | ✅ |
| Open Graph | ✅ Updated | ✅ | ✅ |
| Twitter Card | ✅ Updated | ✅ | ✅ |
| Favicon | ✅ | ✅ | ✅ |
| Theme-color | ✅ | ✅ | ✅ |
| hreflang tags | ✅ (en, en-us, en-in, x-default) | — | — |
| sitemap.xml | ✅ weekly | ✅ monthly | ✅ monthly (added 2026-06-15) |
| Schema: Organization | ✅ | — | — |
| Schema: LocalBusiness | ✅ | ✅ | — |
| Schema: ProfessionalService | — | — | ✅ |
| Schema: FAQPage | ✅ | ✅ | ✅ (6 Qs) |
| GA4 Tracking | ✅ G-2SQW40RNQ8 | ✅ G-2SQW40RNQ8 | ✅ G-2SQW40RNQ8 |
| `<html lang="en">` | ✅ | ✅ | ✅ |

### Off-Page SEO — Action Items
| Action | Priority | Notes |
|---|---|---|
| Submit to Google Search Console | Critical | Add property for supraorigin.com; submit sitemap |
| Submit to Bing Webmaster Tools | High | Free; significant traffic from US |
| Create Google Business Profile | High | Boosts local India searches; free |
| List on Clutch.co | High | US clients use Clutch to find India dev firms |
| List on GoodFirms | High | Similar to Clutch; strong SEO domain authority |
| List on IndiaMART (attendance) | High | India B2B — RFID hardware buyers |
| Create LinkedIn Company Page | Medium | Add to Schema.org `sameAs`; post case studies |
| Submit to Justdial / Sulekha | Medium | India local discovery |

---

## Schema.org Reference

### index.html — Organization
```json
{
  "@type": "Organization",
  "name": "Supra Origin AI Private Limited",
  "alternateName": "Supra Origin AI",
  "url": "https://www.supraorigin.com",
  "logo": "https://www.supraorigin.com/logo/logo-transparent-png.png",
  "email": "thesupraoriginai@gmail.com",
  "telephone": ["+91-89543-32282", "+91-89543-32272"],
  "areaServed": ["IN", "US", "GB", "AU", "CA", "SG"],
  "description": "AI solutions, custom software development, cloud services, and smart attendance systems for businesses globally and across India.",
  "foundingLocation": "India",
  "sameAs": ["https://www.instagram.com/supraoriginai", "https://www.facebook.com/profile.php?id=61579569406102"]
}
```

### index.html — LocalBusiness
```json
{
  "@type": "LocalBusiness",
  "telephone": "+91-89543-32282",
  "openingHours": "Mo-Sa 09:00-18:00",
  "areaServed": ["IN", "US", "GB", "AU"],
  "hasOfferCatalog": {
    "itemListElement": [
      "AI Solutions & Automation", "Custom Software Development",
      "Web & Mobile Application Development", "Cloud Solutions (Azure & AWS)",
      "RFID Attendance Systems (India)", "Biometric Attendance Devices (India)"
    ]
  }
}
```

### attendance-solutions.html — LocalBusiness
```json
{
  "@type": "LocalBusiness",
  "telephone": "+91-89543-32272",
  "openingHours": "Mo-Sa 09:00-18:00",
  "areaServed": {"@type": "Country", "name": "India"}
}
```

---

## Assets Inventory

### Images (`Images/`)
| File | Usage |
|---|---|
| `Banner.jpeg` | OG image for attendance page; attendance gallery |
| `webposter1.jpeg` | OG image for homepage; hero main image; banner slider slide 1 |
| `Webposter2.jpeg` | Banner slider slide 2; gallery |
| `Webposter3.jpeg` | Banner slider slide 3; gallery |
| `rfid-card.png` | Attendance teaser section (homepage); attendance page gallery |
| `rfid-reader.png` | Attendance teaser section (homepage); attendance page gallery |
| `biometric-device.png` | Attendance teaser section (homepage); attendance page gallery |

**Note:** `rfid-card.png` and `biometric-device.png` were removed from the homepage hero mini-row and replaced with abstract AI/software icon visuals to improve international positioning.

### Logo (`logo/`)
| File | Usage |
|---|---|
| `logo-transparent-png.png` | Navbar + footer (both pages) — primary logo in use; also used as favicon |
| `logo-transparent-svg.svg` | Available, not currently linked in HTML |
| `logo-png.png` | Solid bg variant — not currently linked |
| `logo-svg.svg` / `logo-pdf.pdf` / `logo-transparent-pdf.pdf` | Brand kit only |

---

## Deployment Pipeline

```
Developer pushes to GitHub main branch
            ↓
GitHub Actions: deploy.yml triggers
            ↓
appleboy/ssh-action@v1.0.3
  host:       ${{ secrets.SSH_HOST }}
  username:   ${{ secrets.SSH_USERNAME }}
  key:        ${{ secrets.SSH_PRIVATE_KEY }}
  passphrase: ${{ secrets.SSH_PASSPHRASE }}
  port:       22999
            ↓
SSH commands on server:
  cd /home/pndmddgq/repositories/supraorigin
  git pull origin main
  cp -R * /home/pndmddgq/public_html/
  rm -f /home/pndmddgq/public_html/.cpanel.yml
  rm -f /home/pndmddgq/public_html/README.md
  rm -rf /home/pndmddgq/public_html/feature/
  rm -rf /home/pndmddgq/public_html/.claude/
            ↓
Live at https://www.supraorigin.com
```

**GitHub Secrets required**: `SSH_HOST`, `SSH_USERNAME`, `SSH_PRIVATE_KEY`, `SSH_PASSPHRASE`

**Files excluded from production**: `.git/`, `.github/`, `.claude/`, `feature/`, `README.md`, `.cpanel.yml`

---

## Known Bugs & Status

| # | Issue | File | Severity | Status |
|---|---|---|---|---|
| 1 | GA4 ID placeholder `G-XXXXXXXXXX` | `attendance-solutions.html` | High | ✅ Fixed June 2026 |
| 2 | No favicon defined | Both pages | Medium | ✅ Fixed June 2026 |
| 3 | `openingHours` inconsistency (Mo-Fr vs Mo-Sa) | Both pages (Schema.org) | Low | ✅ Fixed — both now Mo-Sa |
| 4 | All CSS/JS inline — no caching | Both pages | Medium | ⏳ Deferred |
| 5 | No `<meta name="theme-color">` | Both pages | Low | ✅ Fixed June 2026 |
| 6 | Footer privacy/terms links are `href="#"` | Both pages | Low | ⏳ Deferred |
| 7 | `feature/` directory copies to production | `deploy.yml` | Medium | ✅ Fixed June 2026 |
| 8 | RFID hero images on global homepage | `index.html` hero | High | ✅ Fixed — replaced with abstract icons |
| 9 | Wrong WhatsApp number routing — single number | Both pages | High | ✅ Fixed — 32272/32282 split |

---

## Planned Features & Improvements (Backlog)

### Completed (June 2026)
- [x] Fix GA4 ID in `attendance-solutions.html`
- [x] Split WhatsApp numbers — 32272 on attendance page, 32282 on homepage
- [x] Update contact sections to reflect correct phone roles
- [x] Update WhatsApp pre-fill messages per page
- [x] Update homepage hero — remove RFID hardware thumbnails, global copy
- [x] Add `#attendance-teaser` section to homepage (replaced `#attendance-featured` + `#att-service-cards`)
- [x] Update homepage `<title>` and `<meta description>` for global keywords
- [x] Update Schema.org on both pages (openingHours, telephone, areaServed, hasOfferCatalog)
- [x] Add hreflang tags to homepage
- [x] Update FAQ on homepage to international+India mix
- [x] Add "India Market" badge to RFID/Biometric service cards (cards 08 & 09)
- [x] Add favicon to both pages
- [x] Fix sitemap.xml lastmod + changefreq
- [x] Fix deploy.yml — cleanup feature/ and .claude/ from production
- [x] Add `<meta name="theme-color">` to both pages
- [x] Unify `openingHours` to Mo-Sa on both pages
- [x] Add `#insights` section (3 article teaser cards) for SEO keyword density
- [x] Update top bar copy to global-friendly message
- [x] Add GA4 phone_click and attendance_page_visit tracking
- [x] Remove attendance teaser section from homepage; replace banner slider with #global-reach countries strip
- [x] Remove "international only" / "RFID attendance only" labels from contact sections
- [x] Add Services dropdown to index.html nav (CSS hover desktop / JS dd-open mobile)
- [x] Add Medical IT hero chip to homepage hero
- [x] Create `medical-services.html` — full 8-service healthcare IT page (CPT, MIPS, PQRS, Scheduling, Telehealth, EDI 270/271, EDI 837/835, EHR Integration)
- [x] Update `attendance-solutions.html` nav with same Services dropdown
- [x] Add `medical-services.html` to `sitemap.xml`

### Critical / Next Steps
- [ ] **Register site in Google Search Console** — submit sitemap.xml immediately
- [ ] **Create Google Business Profile** — free; boosts India + branded search
- [ ] **List on Clutch.co** — critical for US client acquisition; even 2–3 reviews drive inbound

### High Priority (Off-Page SEO)
- [ ] Submit to Bing Webmaster Tools
- [ ] List on GoodFirms
- [ ] List on IndiaMART (attendance product line)
- [ ] Create LinkedIn Company Page + add to Schema.org `sameAs`
- [ ] Submit to Justdial / Sulekha (India local discovery)

### Medium Priority
- [ ] Add `loading="lazy"` to all product/gallery images
- [ ] Verify all GA4 events firing — `phone_click` and `attendance_page_visit` in particular
- [ ] Fix footer Privacy Policy / Terms placeholder links (currently `href="#"`)
- [ ] Add Google Maps embed in contact section

### Low Priority / Future
- [ ] Create dedicated **Blog / Resources** section for long-term SEO
- [ ] Add dedicated **"About Us" page** with team bios
- [ ] Add **LinkedIn Company Page** URL to Schema.org `sameAs` array
- [ ] Extract shared CSS into `styles.css` and shared JS into `main.js` to eliminate duplication
- [ ] Add Bing Webmaster meta tag to both pages

---

## Notes & Decisions

- **International-first homepage** does not abandon Indian clients — it leads with globally relevant services (AI, software, cloud) and surfaces India-market products (RFID, biometric) through a clear, highlighted `#attendance-teaser` section lower on the page.
- **Two WhatsApp numbers on different pages is intentional** — it lets the team route enquiries correctly from day one without a CRM.
- **Clutch.co is critical for US client acquisition** — US-based procurement managers routinely search Clutch before engaging offshore vendors. A listing with even 2–3 reviews can drive inbound leads.
- **Google Search Console is free and essential** — submitting the sitemap will accelerate indexing. Without it, Google may take weeks to discover the attendance page.
- **hreflang tags** signal to Google that the homepage targets English-speaking users globally, not just India, preventing geo-restriction to `.in` searches only.
- **`feature/` directory leaking to production was a security risk** — implementation plan was visible at `supraorigin.com/feature/implementation-plan.md`. Fixed in `deploy.yml`.
- **No backend infrastructure change needed** — Web3Forms handles all form delivery; WhatsApp handles chat. Correct at current traffic levels.
- **All CSS and JavaScript lives inline** — intentional simplicity for static deployment with no build step. Extract to separate files once the project grows beyond 2–3 pages.
- **Attendance page contact form is richer** than homepage form — it has a `solution_required` dropdown with conditional "Other" field (`handleSolutionChange()`). Homepage form is intentionally simpler for international visitors.
- **Logo is rendered circular** in navbar via `border-radius: 50%` — keep in mind if a rectangular logo variant is ever needed.
- Deployment is fully automated: every `main` branch push goes live within seconds. Do not commit broken code directly to `main` — use a feature branch and PR.

---

*Last updated: 2026-06-15 · Updated: Removed #global-reach "Trusted by Clients Across" strip and all false country/client count claims; hero mini-stats changed to Full-Stack / Technologies / Global Delivery / Free Consult; hero sub-text, services subtitle, Why Us card, FAQ answers, footer, top bar all rewritten to honest capability statements*
