---
name: "lyj-skill"
description: "Build production-ready fullstack websites with i18n, responsive design, and reusable components. Invoke when user wants to create a website from scratch or add pages to an existing site."
---

# Lyj Skill — Fullstack Website Builder

A structured skill for building fullstack websites from scratch, with heavy emphasis on frontend quality, multi-language support, and visual consistency. Backend support is lightweight and serves frontend needs.

## Workflow (MANDATORY)

Every website project follows this sequence. Do NOT skip steps. Do NOT start coding before the plan is confirmed.

### Step 1: Receive the Idea

User describes the website in natural language (usually imprecise). Acknowledge briefly and move to probing.

### Step 2: Multi-Round Probing (Loop Until Saturation)

**CRITICAL RULES — Use the `AskUserQuestion` tool:**
- Every question MUST be multiple-choice (2–4 options), so the user can click to select.
- Ask 1–4 questions per round. Keep each round focused and digestible.
- **Keep probing until the specification is "saturated"** — you can clearly answer all dimensions below.
- When in doubt, ask one more round rather than guessing.

Probe these dimensions across rounds:

| Dimension | What to Cover |
|-----------|---------------|
| **Languages** | Which languages? (zh/en/ja...). Default languages if unspecified. |
| **Pages** | What pages does the site need? (home, about, contact, blog, etc.) Page hierarchy? |
| **Data** | How is data sourced? Mock JSON, external API, lightweight backend, user's choice? |
| **CTA Actions** | What should each CTA button do? Submit form? Navigate? Open modal? If unclear, ask. |
| **Tech Stack** | Framework preference? If none, auto-select based on project needs. |
| **Special Requests** | Any page that should NOT have logo/navbar? Any extra features? |

NOTE: Do NOT probe Visual Style in this round. It is handled in Step 2b below.

### Step 2b: Design System Selection (REQUIRED — Do NOT Skip)

After basic probing is saturated, run the UI/UX Pro Max search engine to get design recommendations. The user should CHOOSE from top recommendations — never auto-select silently.

#### 2b.1 Run the Search Engine

```bash
python3 .trae/ui-ux-pro-max/scripts/search.py "<user's product description>" --design-system -n 5
```

This searches 5 domains in parallel: product type, style, color, landing/pattern, typography.

#### 2b.2 Present Top 5 Recommendations

Use `AskUserQuestion` to let user pick. **Every option MUST include a description explaining what it is in plain language** — the user may not know design terminology.

Present in rounds:

**Round A — UI Style (choose 1 from Top 5):**

Each option format: `"Style Name"` as label, `"一句话解释风格特点 + 适用场景"` as description.

Example:
```
○ Glassmorphism
  毛玻璃半透明效果，适合现代 SaaS、金融面板、高端科技产品

○ Minimalism & Swiss Style  
  极简白底黑字、大留白、网格布局，适合企业官网、文档站、专业工具

○ Soft UI Evolution
  柔和阴影、温暖高级感，适合美容、健康、高端服务

○ Claymorphism
  软 3D、厚边框、像橡皮泥，适合儿童应用、教育产品、创意工具

○ Flat Design
  无阴影、纯色块、干净利落，适合初创 MVP、后台管理、移动应用
```

**Round B — Color Palette (choose 1 from Top 5):**

Each option: color name + hex code as label, mood and fit as description.

Example:
```
○ Ocean Blue #2563EB / #F8FAFC
  沉稳专业蓝色系，适合 SaaS、金融、企业服务

○ Warm Clay #C67B5C / #F5F0E1
  温暖陶土色系，适合美容、手工品牌、咖啡馆
```

**Round C — Font Pairing (choose 1 from Top 5):**

Each option: font names as label, mood and best-for as description.

Example:
```
○ Inter + Lora
  现代无衬线标题 + 优雅衬线正文，适合企业官网和博客

○ DM Sans + Merriweather
  几何感强 + 高可读性衬线，适合 SaaS 和阅读型产品
```

**Round D — Charts (ONLY if dashboard/data-vis pages exist, choose 1 from Top 5):**

Each option: chart type + library as label, use-case as description.

If user says "I don't know what charts to use" or "I don't need charts", skip this round.

#### 2b.3 After All Selections

Summarize the user's picks before moving to Step 3:

```
Your Design System:
🎨 Style: Glassmorphism
🌈 Colors: Ocean Blue #2563EB / #F8FAFC
🔤 Fonts: Inter (headings) + Lora (body)
📊 Charts: N/A

Proceeding to delivery plan...
```

### Step 3: Propose the Delivery Plan

Once saturated, present a structured plan:

- **Tech stack** — frameworks, libraries, i18n solution
- **Design system** — the user-selected style, colors, fonts, charts from Step 2b
- **Page list** — every page with its route and purpose
- **Component tree** — shared components (navbar, footer, etc.) and page-specific ones
- **Data model** — how data flows (mock/API/db)
- **Route structure** — URL scheme for all languages

**Do NOT start coding. Wait for user confirmation.**

### Step 4: Confirm**

- User reviews the plan.
- Adjust if needed.
- Only proceed when user says "ok" / "可以" / "开始" / similar.

### Step 5: Code

Implement following the Core Requirements below, guided by `karpathy-guidelines`:
- Think before coding — surface assumptions
- Simplicity first — minimum code
- Surgical changes — touch only what's needed
- Goal-driven — verify each step

#### TDD Guidance (Selective)

Not all website code needs tests. Apply TDD where it adds value:

| Code Type | Test It? | How |
|-----------|----------|-----|
| **API routes / server logic** | ✅ REQUIRED | Write failing test → implement → verify pass |
| **Form validation** | ✅ REQUIRED | Test valid + invalid + edge cases |
| **State management / hooks** | ✅ REQUIRED | Test state transitions |
| **Data processing / utils** | ✅ REQUIRED | Input → output assertions |
| **CSS / layout code** | ❌ SKIP | Visual verification instead |
| **Animation code** | ❌ SKIP | Manual visual check |
| **Markup / JSX structure** | ❌ SKIP | Covered by visual consistency audit |

**For code that REQUIRES tests:**
1. Write the test FIRST — watch it fail
2. Write minimal code to make it pass
3. Refactor only after green
4. Run full suite — no regressions

## Core Requirements (Non-Negotiable)

### 1. Multi-Language (i18n) — 100% Coverage

- Every text on every page MUST exist in all declared language versions.
- Auto-select i18n library (`next-intl`, `react-i18next`, etc.) based on project tech stack.
- Navigation bar, CTAs, headings, labels — all core interaction surfaces MUST stay in sync with the active locale.
- Switching locales MUST NOT leave residual content from the previous language.
- All page elements react to locale changes synchronously.

### 2. Visual Consistency Across All Pages

Every page in the site MUST share identical specifications for these five elements:

- **Page title format** — same structure, same hierarchy (H1/H2/H3 rules)
- **Layout logic** — same grid system, same spacing scale, same alignment patterns
- **Brand color system** — same palette usage across pages
- **Font families** — same typeface per content role (headings / body / code)
- **Font sizes** — same scale applied uniformly

Same-level content across the site MUST use identical visual presentation standards.

### 3. CTA Buttons Must Have Real Functionality

- Every CTA button MUST trigger a meaningful action.
- If the exact business logic behind a CTA is unclear, **ask the user immediately** — never wire up a dummy or placeholder action.
- Invalid or non-business-logic triggers are forbidden.

### 4. Logo + Navbar Are Global by Default

- Logo and navigation bar are global shared components.
- They MUST appear on every page unless the user explicitly requests their removal from a specific page.
- These components live in the shared component library (see below).

### 5. Responsive Across All Devices

- Desktop, tablet (768px–1024px), and mobile (<768px) — all three breakpoints MUST look polished.
- Layout, element proportions, and interaction logic MUST adapt to each device context.
- No horizontal overflow, no clipped content, no unreadable text at any viewport.

### 6. When in Doubt, Ask First

- Any uncertainty about requirements, logic, or design intent MUST be surfaced to the user before implementation.
- Mirroring `karpathy-guidelines` principle 1: don't assume, don't hide confusion.
- This applies to all development phases.

## Default Standards (Unless User Overrides)

| Area | Default |
|------|---------|
| **Accessibility (a11y)** | On — ARIA labels, keyboard navigation, screen reader compatibility |
| **Data approach** | User specifies per project (mock data / API / database / other) |
| **Visual style** | User describes per project — no hardcoded defaults for colors, fonts, or spacing |
| **Theme (dark/light)** | On hold — only enable if user requests |

## Out of Scope

The skill does NOT cover these areas by default (only include if user explicitly requests):

- SEO (hreflang, meta tags, Open Graph, sitemap)
- Image/icon sourcing and optimization standards
- Loading / empty / error state patterns
- Form validation rules
- Browser compatibility baselines (IE, etc.)

## Shared Component Library

Reusable components are stored in a global shared directory so they can be used across projects. The directory path is determined by the skill at first use (suggested: `~/.trae/shared-components/`).

Components that should be built and accumulated over time:

- `Navbar` — responsive, locale-aware, logo-included
- `Footer` — standardized site footer
- `CTAButton` — configurable action button
- `LanguageSwitcher` — locale toggle
- `PageShell` — page wrapper with consistent layout

New projects should check the shared library first before creating duplicate components.

## Tech Stack Selection

- No preset tech stack preference — AI selects based on project requirements.
- i18n library is auto-selected to match the chosen framework.
- Backend is kept lightweight, built only to serve frontend data needs.
