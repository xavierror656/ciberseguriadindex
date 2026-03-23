# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **cybersecurity course** for the manufacturing industry, delivered for INDEX Ciudad Juárez. It is a content/documentation project written entirely in Markdown.

- **Duration:** 16 hours across 4 sessions (4 hours each)
- **Dates:** March 24–27, 2026
- **Audience:** IT staff, engineers, quality, administration, and management at manufacturing companies (maquiladoras)

## Structure

The course is organized into 4 days, each with:
- A thematic block (1 hour) covering theory, standards, and metrics
- Two hands-on labs (1 hour each) using free platforms
- A practical exercise or capstone activity (1 hour)

| Day | Theme | Key Topics |
|-----|-------|------------|
| 1 | AI Threats & Social Engineering | Deepfakes, CEO fraud, AI-generated phishing (no grammar errors), voice cloning |
| 2 | Identity Management & Zero Trust | Zero Trust ("never trust, always verify"), MFA (biometrics, YubiKey), PAM |
| 3 | Data Security, Cloud & Hybrid Work | Cloud config (OneDrive/SharePoint), BYOD, VPN, MDM, LFPDPPP privacy compliance |
| 4 | Incident Response, Ransomware & Digital Hygiene | NIST SP 800-61 phases, ransomware decision tree, password managers, software updates, reporting channels |

## Standards and Frameworks Referenced

- **MITRE ATT&CK** — tactic/technique mapping for each attack scenario
- **CIS Critical Security Controls** — Controls 3, 5, 8, 9, 13, 14, 17
- **NIST Cybersecurity Framework** — Identify, Protect, Detect, Respond, Recover
- **NIST SP 800-61** — Incident Response lifecycle (Day 4)
- **ISO 27001** — A.5, A.6, A.9 access and identity controls
- **LFPDPPP** — Mexican personal data protection law (Day 3); includes INAI, ARCO rights, breach notification

## Lab Platforms Used

All platforms are free:
- **TryHackMe** — phishing analysis (Day 1)
- **OverTheWire Bandit** — Linux credential/access security (Day 2)
- **OWASP Juice Shop** — web vulnerabilities: SQLi, XSS, session hijacking (Day 3)
- **Blue Team Labs** — log analysis and threat detection (Day 4)

## Key Security Metrics Tracked

| Metric | Target |
|--------|--------|
| Phishing Click Rate | <5% |
| Security Awareness Coverage | >90% |
| MFA Coverage (admins) | 100% |
| Privileged Account Ratio | <5% |
| Patch Compliance Rate | <72 hours |
| Asset Inventory Coverage | 100% |
| Data Exposure Index | 0 critical files public |
| MTTD | <24 hours |
| MTTR | <4 hours |
| RTO | <8 hours |

## File Naming

Each day's content lives in a single Markdown file:

- `dia1-amenazas-ia-ingenieria-social.md`
- `dia2-identidad-zero-trust.md`
- `dia3-datos-nube-redes-industriales.md`
- `dia4-respuesta-incidentes-ransomware.md`

## Document Conventions

Each day file follows this structure:

1. `## Bloque 1` — Theory block (1 hr): concepts, real-world examples, MITRE/NIST mapping
2. `## Lab 1` — Hands-on lab (1 hr): platform setup, step-by-step instructions, expected outcome
3. `## Lab 2` — Hands-on lab (1 hr): same structure as Lab 1
4. `## Actividad Final` — Capstone or practical exercise (1 hr)

Each lab section must include:
- Platform name and free access URL
- Step-by-step instructions in Spanish
- A measurable expected outcome (e.g., "80% de tasa de detección")

Tables are used heavily for: attack variant comparisons, system/risk mappings, metric targets, and framework control references.

## Presentation Design System

All slides must follow the **Skilling Center Tecmilenio** brand. Full details in `source/TEMPLATE_GUIDE.md`.

**Quick reference:**
- Fonts: Calibri Light (titles), Calibri (body)
- Primary colors: `#00534C` (dark teal), `#00879B` (teal), `#40C6BD` (turquoise accent), `#FFFFFF` (background)
- Alert/risk color: `#ED7D31` (orange)
- Table headers: `#00534C` bg + white text; alternating rows `#B1DFDC` / `#FFFFFF`
- Source images and logos: `source/template_assets/`

### Slide Files

| File | Status | Port |
|------|--------|------|
| `slides-dia1.md` | ✅ Complete — 42 slides | `npx slidev slides-dia1.md` → :3030 |
| `slides-dia2.md` | ✅ Complete — 47 slides | `npx slidev slides-dia2.md --port 3032` |
| `slides-dia3.md` | ⏳ Pending |  |
| `slides-dia4.md` | ⏳ Pending |  |

### Slide Architecture (applied to Día 1 and Día 2)

Every day slide deck follows this structure:

1. **Cover** — `layout: cover`, background `/images/juarez-skyline.jpg`, teal right-panel with logo
2. **Quote** — motivational opening quote
3. **Poll** — audience activation poll
4. **Agenda** — `layout: two-cols` recap + day agenda
5. **Termómetro de riesgo** — `layout: center`, 3-column Rojo/Amarillo/Verde diagnostic
6. **Section: Bloque 1** — `layout: section` with background image
7. ...content slides...
8. **Cierre Bloque 1** — 3 summary cards + closing question
9. **Poll** — pre-lab confidence check
10. **Section: Lab** — timer grid (⏱ 45 min) + 4 roles
11. ...lab content slides...
12. **Micro-receso** — `layout: center`, 5-min active reflection pause
13. **Section: Ejercicio** — `background: /images/tecmilenio-teamwork.jpeg`
14. ...exercise slides...
15. **Gallery Walk** — instructions, rubric, success criteria
16. **Conclusiones** — `layout: two-cols-header`
17. **Recursos** — tools table
18. **Tarjeta de bolsillo** — 3-column printable cheat sheet
19. **End** — `layout: end`, reflection question

### CSS and Styling

- Global styles: `style.css` (auto-loaded by Slidev — do NOT use `css:` in headmatter)
- Custom utility classes: `.tip-teal`, `.tip-warn`, `.tip-danger`
- Accent bar: `::before` pseudo-element on `.slidev-layout` (hidden on cover/section/quote/end)
- Section overlay: `::after` with `rgba(0,50,46,0.72)` to darken background images

### Icon Rules

- Use Carbon Icons (`carbon-*`) — verify name exists before using
- On light background: use `-600` or `-700` variants (NOT `-400` — those are for dark themes)
- Known working: `carbon-email`, `carbon-security`, `carbon-alarm`, `carbon-time`, `carbon-report`, `carbon-checkmark`, `carbon-warning-alt-filled`, `carbon-warning-filled`, `carbon-information`
- Known broken: `carbon-shield` (use `carbon-security`), `carbon-document-multiple` (use `carbon-report`)

### Cover Slide Pattern

```markdown
---
theme: default
...
colorSchema: light
layout: cover
background: /images/juarez-skyline.jpg
addons:
  - slidev-addon-qrcode
  - slidev-component-poll
  - slidev-addon-rabbit
  - window-mockup
  - slidev-addon-rough-mermaid
rabbit:
  slideNum: true
defaults:
  layout: default
---

<img src="/images/tecmilenio-logo.png" class="absolute top-6 left-8 h-10 z-10" />

<div class="absolute right-0 top-0 bottom-0 w-[42%] bg-[#00879B]/92 flex flex-col justify-center pl-8 pr-6 z-10 overflow-hidden">
  <h1 class="text-white text-2xl font-light leading-tight mb-3 pb-3" style="border-bottom: 2px solid #40C6BD; border-color: #40C6BD !important;">
    [Title line 1]<br/>[Title line 2]<br/>[Title line 3]
  </h1>
  <h2 class="text-[#B1DFDC] text-base font-light mb-5">
    Día N — [Subtitle]
  </h2>
  <p class="text-white/90 text-sm font-semibold">INDEX Ciudad Juárez</p>
  <p class="text-white/60 text-xs mt-1">DD de marzo de 2026 · Sesión N de 4</p>
</div>
```

### Public Images Available

All images are in `public/images/`:
- `juarez-skyline.jpg` — Ciudad Juárez Golden Zone panorama (cover background, CC BY-SA 3.0)
- `tecmilenio-logo.png` — Skilling Center logo (for cover + content slides)
- `tecmilenio-teamwork.jpeg` — Ejercicio section backgrounds
- `tecmilenio-laptop.png`, `tecmilenio-videocall.jpeg` — Lab section backgrounds
- `workers-maquiladora.jpg`, `manufacturing-plant.jpg` — content slides
- `log-analysis.jpg`, `server-network.jpg` — Lab 3/4 Day 2 backgrounds

## Content Guidelines

- All materials are written in Spanish for a Mexican industrial audience
- Examples must reference maquiladora-specific scenarios (ERP fraud, supplier email spoofing, OT/IT network segmentation, high employee turnover)
- Labs must use only free platforms — no paid tools
- Each lab must include a measurable expected outcome
- MITRE ATT&CK technique IDs (e.g., T1566.001) should be cited when describing attack scenarios

## Deployment

### GitHub Actions — GitHub Pages

Workflow: `.github/workflows/deploy.yml` — triggers on push to `main`.

**Build commands use `--base ./`** (relative paths) so assets work on GitHub Pages subdirectories, custom domains, and local serving alike. Never use absolute base (`/` or `/<repo>/`) for these builds.

```bash
npx slidev build slides-dia1.md --out dist/dia1 --base ./
```

The workflow builds all 4 days into `dist/dia1/`–`dist/dia4/`, copies `index.html` to `dist/`, and adds `dist/.nojekyll` before uploading to Pages.

### Landing page

`index.html` at project root — Tecmilenio-branded hub linking to `dia1/`–`dia4/`. Uses relative links (no leading `/`). Copied to `dist/` by the workflow.

### Local build test

```bash
npm run build:dia1        # outputs to dist/dia1 with --base ./
npx serve dist/dia1       # verify assets load at localhost:3000
```

### Ignored files

`.gitignore` covers: `node_modules/`, `dist/`, `exports/`, `.slidev/`, `.vite/`, `.env*`, OS/editor artifacts.

## Pedagogical Pattern (applied to all days)

Every day includes these learning design elements:

| Element | Purpose | Placement |
|---------|---------|-----------|
| Termómetro de riesgo | Diagnostic self-assessment | Before Bloque 1 |
| Poll de apertura | Audience activation | Before each lab |
| Cierre de bloque | 3-card summary + bridge question | After theory, before lab |
| Timer + Roles grid | Lab structure (45 min, 4 roles) | Section slide of each lab |
| Micro-receso activo | Processing pause + peer share | After Lab 2, before Ejercicio |
| Roles en ejercicio | Collaborative accountability | Exercise slide |
| Gallery Walk | Peer review + rubric | After exercise activity |
| Tarjeta de bolsillo | Printable 3-column cheat sheet | Before end slide |
