---
title: P2P Labs — Digital Design System
aliases:
  - DESIGN.md
  - P2P Labs design
company: P2P Labs
document_type: brand
date: 2026-09-02
status: source-of-truth-for-ui
related:
  - "[[P2P Labs]]"
  - "[[P2P-Labs-Brand]]"
---

# P2P Labs - Digital Design System

> Creator energy with enterprise clarity. A bright, modular creator-tech system built to connect people, partners, technology, and growth.

**Theme:** light-first with intentional deep-navy moments  
**Source of truth:** `P2P - Labs Brands Philosophy Logo`  
**Brand:** P2P Labs  
**Category:** Creator-economy technology, software, and shared SaaS infrastructure

P2P Labs should feel modern, connected, energetic, scalable, and trusted. The visual system combines spacious white layouts and disciplined product UI with vivid creator-tech accents. It is bold without becoming noisy, playful without becoming childish, and credible without becoming conventionally corporate.

The experience must never look like a generic dark SaaS template. Use the brand's color, geometry, data, motion, and creator-focused storytelling to make every page recognizably P2P Labs.

---

## 1. Brand Foundation

### Brand direction

P2P Labs is a tech-first software house and platform company building shared SaaS infrastructure for the creator economy.

### Brand philosophy

| Element | Meaning |
| --- | --- |
| **P** | People - creators |
| **P** | Partners - brands and agencies |
| **2** | Peer-to-peer collaboration |
| **Labs** | Technology and infrastructure |

### Core brand lines

- **Create. Connect. Commerce. Together.**
- **Infrastructure for creators. Built for scale.**
- **The operating system for the creator economy.**

Use one lead line per composition. Do not stack all three as competing headlines.

### Strategic pillars

| Pillar | Meaning | Visual behavior |
| --- | --- | --- |
| **Build** | Powering the tools creators and brands need to grow. | Modular systems, product UI, structured grids |
| **Connect** | Enabling seamless collaboration and global reach. | Linked paths, nodes, paired elements, shared motion |
| **Scale** | Data-driven infrastructure designed for performance and scale. | Expanding grids, charts, progressive sequences |
| **Empower** | Giving creators and partners freedom to own their growth. | Human outcomes, clear actions, confident messaging |

### Brand attributes

- **Creator-Tech:** built for the new era of creators.
- **Modern:** clean, minimal, and future-ready.
- **Confident:** bold presence with clear purpose.
- **Connected:** designed for collaboration.
- **Scalable:** systemized to grow with the ecosystem.
- **Trusted:** precise, readable, and credible at enterprise level.

---

## 2. Design Principles

### 2.1 Clarity first

Every screen must communicate one primary idea and one primary action. Hierarchy, labels, spacing, and navigation should help users decide quickly.

### 2.2 Modular and flexible

Use a consistent grid and reusable components. Composition may be asymmetric, but alignment must remain deliberate. Avoid repeating the same card grid in every section.

### 2.3 Conversion focused

Every important screen should guide users toward a meaningful next step. Primary actions are vivid purple; lime is a growth signal, not a universal CTA color.

### 2.4 Scalable by design

The system must work across marketing sites, dashboards, mobile interfaces, campaigns, social content, and future P2P products without losing its identity.

### 2.5 Consistent everywhere

Use the same tokens, component logic, icon language, interaction feedback, and accessibility standards across web, mobile, and product UI.

---

## 3. Color System

### Primary palette

| Name | Value | Token | Role |
| --- | --- | --- | --- |
| Deep Navy | `#0B0F2B` | `--color-navy` | Primary text, navigation, dark sections, trusted product surfaces |
| Vivid Purple | `#652DFF` | `--color-purple` | Primary brand color, CTAs, active states, key highlights |
| Lime Green | `#A6FF1A` | `--color-lime` | Growth, success, momentum, positive accents |
| White | `#FFFFFF` | `--color-white` | Main page background and inverse text |
| Neutral 100 | `#F3F4F8` | `--color-neutral-100` | Cards, soft sections, input surfaces, subtle UI separation |

### Secondary and supporting palette

| Name | Value | Token | Recommended use |
| --- | --- | --- | --- |
| Deep Purple | `#2C0F63` | `--color-deep-purple` | Dark brand panels, gradient depth |
| Aqua Teal | `#00D4C1` | `--color-aqua` | Connection, collaboration, secondary data series |
| Electric Blue | `#382BFF` | `--color-electric-blue` | Technology, links, charts, product states |
| Vivid Pink | `#FF4DA6` | `--color-pink` | Creator energy, promotional emphasis, data series |
| Sun Yellow | `#FFC83D` | `--color-yellow` | Warm highlights, attention, data series |
| Soft Lavender | `#9A8CFF` | `--color-lavender` | Subtle brand surfaces and inactive decorative states |
| State Gray | `#1B1F2E` | `--color-state-gray` | Secondary dark surface and muted dark UI |
| Light Neutral | `#F3F4F9` | `--color-light-neutral` | Alternative soft background and section separation |

### Brand gradients

| Name | CSS | Use |
| --- | --- | --- |
| Purple to Lime | `linear-gradient(135deg, #652DFF 0%, #A6FF1A 100%)` | Signature brand moments, icon fields, restrained hero accents |
| Purple to Pink to Yellow | `linear-gradient(135deg, #652DFF 0%, #FF4DA6 62%, #FFC83D 100%)` | Creator-energy campaigns, social visuals, expressive highlights |
| Deep Creator-Tech | `linear-gradient(135deg, #2C0F63 0%, #0B0F2B 100%)` | Dark sections, dashboard sidebars, ambient depth |

### Semantic color rules

- Use **Deep Navy** for body copy and headings on light backgrounds.
- Use **Vivid Purple** for the primary action and key brand moments.
- Use **Lime Green** to signal success, growth, and positive momentum. Pair lime with Deep Navy text.
- Use **Aqua, Blue, Pink, and Yellow** for data differentiation, illustrations, or controlled supporting accents.
- Keep most page area White or Neutral 100. Color should create hierarchy, not fill every surface.
- Never use lime as paragraph text on white.
- Never place white text on lime.
- Never rely on gradient text for essential information.
- Product validation errors may use an accessible semantic red; this is a functional UI exception, not a brand accent.

### Recommended color balance

- **60-70%** White and light neutrals
- **20-30%** Deep Navy and structured dark surfaces
- **5-10%** Vivid Purple, Lime, and supporting accents

This ratio is directional, not a rigid quota. Preserve whitespace and contrast first.

---

## 4. Typography

The brand guideline contains two related systems. Use the expressive brand fonts for high-impact marketing moments and the product hierarchy for functional interfaces.

### Brand and campaign typography

| Role | Family | Weight | Use |
| --- | --- | --- | --- |
| Expressive display | `Software Tester 7` | Regular / Bold | Rare campaign words, branded numerals, short visual statements |
| Brand body | `Montserrat` | Regular / Bold | Marketing copy, social compositions, brand collateral |

`Software Tester 7` is an accent face, not the default website heading font. Use it only when the licensed webfont asset is available. Never imitate it with stretched or outlined text.

### Product and website hierarchy

| Role | Family | Weight | Size / line height | Token |
| --- | --- | --- | --- | --- |
| H1 | Inter | 700 | `36px / 44px` | `--text-h1` |
| H2 | Inter | 600 | `28px / 36px` | `--text-h2` |
| H3 | Inter | 600 | `22px / 30px` | `--text-h3` |
| H4 | Inter | 500 | `18px / 26px` | `--text-h4` |
| Body | Satoshi | 400 | `16px / 24px` | `--text-body` |
| Small | Satoshi | 400 | `14px / 20px` | `--text-small` |
| UI label | Inter | 500 | `12px / 16px` | `--text-label` |

### Marketing display extension

For large website heroes, extend the approved Inter hierarchy responsively:

- Desktop display: `clamp(56px, 6vw, 88px)`, line-height `0.96-1.02`
- Tablet display: `48-64px`, line-height `1.00-1.06`
- Mobile display: `38-48px`, line-height `1.04-1.10`
- Keep hero copy to roughly 8-12 words when possible.
- Use sentence case by default. Reserve all caps for small labels, tags, and navigation metadata.

### Font stack

```css
--font-display: "Software Tester 7", "Lastica", "Inter", sans-serif;
--font-heading: "Inter", "Montserrat", system-ui, sans-serif;
--font-body: "Satoshi", "Montserrat", system-ui, sans-serif;
```

### Typography rules

- Use Deep Navy for primary text on light surfaces.
- Keep body copy between `45ch` and `68ch` for comfortable reading.
- Use bold type to create hierarchy, not to emphasize every sentence.
- Do not use more than three weights in one composition.
- Avoid center-aligned paragraphs longer than two short lines.
- Maintain strong contrast and generous spacing for accessibility and clarity.

---

## 5. Grid, Spacing, and Shape

### Grid

- Desktop: 12 columns, maximum content width `1280px`, `24-32px` gutters.
- Tablet: 8 columns, `24px` outer margins.
- Mobile: 4 columns, `16-20px` outer margins.
- Full-bleed color and media are allowed, but content should return to the grid.
- Use asymmetric spans to create energy: common desktop splits are `5/7`, `7/5`, and `4/8`.

### 8pt spacing scale

| Name | Value | Token |
| --- | --- | --- |
| 1 | `8px` | `--space-1` |
| 2 | `16px` | `--space-2` |
| 3 | `24px` | `--space-3` |
| 4 | `32px` | `--space-4` |
| 5 | `40px` | `--space-5` |
| 6 | `48px` | `--space-6` |
| 8 | `64px` | `--space-8` |
| 10 | `80px` | `--space-10` |
| 12 | `96px` | `--space-12` |

Use `4px` only for optical micro-adjustments inside compact controls.

### Radius vocabulary

| Role | Value |
| --- | --- |
| Small controls and tags | `8px` |
| Inputs and compact cards | `12px` |
| Standard cards and panels | `16px` |
| Feature panels and media frames | `24px` |
| Pills and avatars | `9999px` |

Rounded corners should feel polished and modern, not bubbly. Avoid placing rounded cards inside rounded cards unless hierarchy requires it.

### Borders and elevation

- Default border: `1px solid rgba(11, 15, 43, 0.10)`.
- Strong border: `1px solid rgba(101, 45, 255, 0.28)`.
- Use soft ambient elevation on floating cards only: `0 16px 48px rgba(11, 15, 43, 0.10)`.
- Prefer background separation, borders, and spacing over heavy shadows.
- Do not apply neon glows to body content or every card.

---

## 6. Logo System

### Approved forms

- Primary logo
- Stacked lockup
- Horizontal lockup
- Icon / submark
- Approved monochrome submarks where supplied

### Usage

- Use approved source assets only.
- Maintain generous clear space around the full lockup.
- Use the logo on high-contrast white, light-neutral, deep-navy, or approved brand-gradient backgrounds.
- Scale proportionally without distortion.
- Preserve original color, gradient, spacing, and element order.
- Use the icon/submark for favicon, compact navigation, app icon, or small avatar contexts.

### Never

- Alter logo colors or gradients.
- Stretch, skew, crop, rotate, or redraw the logo.
- Add outlines, strokes, shadows, bevels, or glow effects.
- Rearrange the symbol, `P2P`, or `LABS` elements.
- Place the logo on busy imagery or low-contrast backgrounds.
- Substitute a P2P Network logo for the P2P Labs corporate mark.

---

## 7. Visual Identity Elements

### Layout system

Use a modular grid, consistent spacing, clear alignment, and varied section composition. Alternate between open editorial layouts, product demonstrations, data-led sections, and a small number of structured cards.

### Pattern and texture

- Dot matrices representing people, data, and connection
- Thin concentric lines representing network effects and momentum
- Modular grid fragments
- Connected nodes and directional paths
- Use at low opacity so texture adds depth without reducing legibility.

### Geometric language

- Derive angular folds, linked paths, and modular blocks from the P2P submark.
- Use geometry to connect content or guide attention, not as random decoration.
- Combine sharp directional forms with controlled rounded UI surfaces.

### Gradient and depth

- Use soft gradient fields for hero atmosphere and featured moments.
- Keep gradients anchored to the approved palette.
- Add depth with layered opacity, restrained blur, and subtle 3D objects.
- Avoid uncontrolled rainbow blobs and generic glassmorphism.

### Iconography

- Line icons with a consistent `2px` stroke.
- Rounded caps and joins.
- Simple geometry with one clear metaphor per icon.
- Use Deep Navy or Vivid Purple by default; supporting colors can indicate category or state.
- 3D icons are reserved for hero visuals, product storytelling, and campaign moments.

### Imagery

- Feature real creators, collaborators, products, and work whenever authentic assets exist.
- People should feel capable, contemporary, and active - never like generic corporate stock models.
- Product imagery may combine interface screens, 3D creator-tech objects, brand geometry, and data.
- Use clean cutouts, directional lighting, and controlled purple/navy environments for expressive scenes.
- Do not invent client logos, partnerships, results, or testimonials.

---

## 8. Core Components

### Navigation

- Light default: white or translucent white surface, Deep Navy links.
- Dark variant: Deep Navy surface, white links.
- Active and hover states use Vivid Purple.
- Keep the primary navigation concise; group product complexity inside a clear menu when needed.
- Sticky navigation may introduce a subtle blur and border after scroll.
- Mobile navigation must use a direct, accessible drawer with large touch targets.

### Primary button

- Background: Vivid Purple.
- Text: White, Inter 600.
- Height: `48px` standard; `44px` compact.
- Horizontal padding: `20-24px`.
- Radius: `12px` or full pill when the surrounding system uses pills.
- Hover: slightly darker purple or `translateY(-1px)` with restrained shadow.
- Focus: visible `3px` lavender/purple focus ring.
- Disabled: reduced contrast while preserving readable text.

### Secondary button

- White or transparent background.
- `1px` Vivid Purple border.
- Vivid Purple label.
- Hover with a very soft purple tint; never switch to lime text.

### Ghost and text actions

- Deep Navy or Vivid Purple label.
- Pair with a simple directional arrow when useful.
- Underline or background tint appears on hover and keyboard focus.
- Do not hide essential actions behind icon-only controls.

### Icon button

- Minimum touch target: `44x44px`.
- Use a `2px` rounded-stroke icon.
- Circular purple icon buttons are allowed as emphasis but should not outnumber text actions.

### Input field

- White background on neutral sections; Neutral 100 background on white sections.
- Deep Navy input text and readable muted placeholder.
- `1px` navy-alpha border, `12px` radius, minimum `48px` height.
- Focus state: Vivid Purple border and subtle ring.
- Error state: clear text explanation plus icon; never communicate errors by color alone.

### Card

- White or Neutral 100 surface.
- `16px` standard radius and `24-32px` padding.
- One heading, one clear content purpose, and optional action.
- Use a border or soft elevation, not both at maximum strength.
- Avoid turning every sentence into a card.

### Feature panel

- Large editorial surface using `24px` radius.
- May use Deep Navy, Deep Purple, a brand gradient, product UI, or authentic creator imagery.
- Keep copy concise and preserve a clear focal point.

### KPI and data card

- Lead with the metric, then label, period, and comparison.
- Positive movement uses Lime with Deep Navy text or icon support.
- Charts use Purple as the primary series, then Aqua, Blue, Pink, and Yellow.
- Never use color as the only distinction between data series; add labels, patterns, or markers.

### Badges and tags

- Purple / lavender: featured or platform state.
- Lime / navy: positive or growth state.
- Pink: promotional or creator category.
- Yellow / navy: attention or limited state.
- Use short labels and maintain accessible contrast.

### Tabs, toggles, and switches

- Active state uses Vivid Purple.
- Inactive state uses neutral surface and navy-gray label.
- Include clear keyboard focus and sufficient hit areas.
- Motion should confirm state change in `160-220ms`.

### Footer

- Use a Deep Navy or white surface depending on page rhythm.
- Include the approved logo, concise brand line, essential navigation, legal links, and contact path.
- A restrained brand-gradient accent may close the composition.

---

## 9. Motion and Interaction

Motion should express connection, momentum, and scale. It must feel smooth and intentional rather than decorative.

### Motion tokens

| Token | Value | Use |
| --- | --- | --- |
| `--duration-fast` | `160ms` | Hover, focus, toggle feedback |
| `--duration-base` | `280ms` | Cards, menus, small entrances |
| `--duration-slow` | `520ms` | Hero layers and section reveals |
| `--ease-brand` | `cubic-bezier(0.22, 1, 0.36, 1)` | Primary easing |

### Choreography

- Page load: stagger headline, supporting copy, and CTA with short opacity/transform reveals.
- Hero: subtle parallax or connected-path motion derived from the logo geometry.
- Scroll: reveal content in reading order; do not animate every small element independently.
- Cards: `1-3px` lift, soft border change, or media zoom.
- Numbers: count up once when the metric enters the viewport.
- Navigation: smooth background, border, and active-state transition.
- Use one signature interaction per important page. Supporting motion should remain quiet.

### Performance and accessibility

- Prefer `transform` and `opacity` animations.
- Avoid scroll hijacking, blocking loaders, and large continuous blur effects.
- Simplify parallax and 3D movement on mobile.
- Respect `prefers-reduced-motion` and show content immediately when motion is reduced.

---

## 10. Responsive Behavior

### Desktop - 1440px reference

- Use the full 12-column grid and deliberate asymmetry.
- Allow one large hero statement or product visual to dominate.
- Preserve generous section spacing of `80-120px`.

### Tablet - 768px reference

- Recompose into 8 columns.
- Reduce decorative layers and pinned interactions.
- Keep primary actions visible without forcing a desktop composition.

### Mobile - 390px reference

- Recompose into 4 columns; do not merely stack desktop sections.
- Reduce display scale, section padding, and simultaneous motion.
- Use full-width primary actions when it improves completion.
- Keep all touch targets at least `44x44px`.
- Replace hover-dependent discovery with visible labels and tap states.
- Prevent horizontal overflow from gradients, charts, and decorative geometry.

---

## 11. Accessibility

- Target WCAG AA contrast for text and functional controls.
- Use Deep Navy for text on White, Neutral 100, Lime, and Yellow surfaces.
- Use White text on Vivid Purple, Deep Purple, State Gray, and Deep Navy when contrast is sufficient.
- Provide visible keyboard focus for every interactive element.
- Preserve logical heading order and semantic landmarks.
- Add descriptive alt text for meaningful imagery; decorative geometry uses empty alt text.
- Forms require persistent labels, clear errors, and success confirmation.
- Charts require text summaries and non-color differentiation.
- Never place essential copy over a busy gradient without a stabilizing surface.

---

## 12. Do's and Don'ts

### Do

- Lead with spacious white or light-neutral layouts.
- Use Deep Navy to establish trust and Vivid Purple to establish brand.
- Use Lime selectively for growth and positive momentum.
- Build on a 12-column modular grid and 8pt spacing system.
- Combine creator-focused storytelling with enterprise-grade clarity.
- Use authentic product screens, data, and creator outcomes.
- Derive patterns and motion from connection, flow, and the P2P logo geometry.
- Keep one clear CTA hierarchy per section.
- Use approved logo lockups and preserve their proportions.

### Don't

- Do not use a warm-brown darkroom aesthetic; it conflicts with the bright creator-tech brand.
- Do not make the entire site dark purple or navy.
- Do not use random gradient blobs without structural purpose.
- Do not apply glassmorphism to every surface.
- Do not place all content inside rounded cards.
- Do not use Lime as the default button or paragraph color.
- Do not use the expressive display font for long copy or core product UI.
- Do not over-animate the interface or hijack scrolling.
- Do not use P2P Network's cyan/blue/pink/orange palette as the corporate P2P Labs palette.
- Do not invent achievements, clients, integrations, statistics, or partnerships.

---

## 13. Surfaces

| Level | Surface | Value | Purpose |
| --- | --- | --- | --- |
| 0 | Page | `#FFFFFF` | Default spacious canvas |
| 1 | Soft section | `#F3F4F8` | Section rhythm, form areas, grouped content |
| 2 | Card | `#FFFFFF` + navy-alpha border | Focused content and product UI |
| 3 | Brand panel | `#652DFF` | CTA, feature, and active brand moment |
| 4 | Deep panel | `#0B0F2B` | Trust, product depth, footer, dark section |
| 5 | Expressive field | Approved gradient | Hero art, campaign, signature moment |

---

## 14. Implementation Tokens

### CSS custom properties

```css
:root {
  /* Brand colors */
  --color-navy: #0b0f2b;
  --color-purple: #652dff;
  --color-lime: #a6ff1a;
  --color-white: #ffffff;
  --color-neutral-100: #f3f4f8;

  /* Supporting colors */
  --color-deep-purple: #2c0f63;
  --color-aqua: #00d4c1;
  --color-electric-blue: #382bff;
  --color-pink: #ff4da6;
  --color-yellow: #ffc83d;
  --color-lavender: #9a8cff;
  --color-state-gray: #1b1f2e;
  --color-light-neutral: #f3f4f9;

  /* Semantic UI extensions */
  --color-border: rgb(11 15 43 / 10%);
  --color-border-brand: rgb(101 45 255 / 28%);
  --color-muted-text: rgb(11 15 43 / 64%);
  --color-error: #d92d20;

  /* Gradients */
  --gradient-purple-lime: linear-gradient(135deg, #652dff 0%, #a6ff1a 100%);
  --gradient-creator: linear-gradient(135deg, #652dff 0%, #ff4da6 62%, #ffc83d 100%);
  --gradient-deep: linear-gradient(135deg, #2c0f63 0%, #0b0f2b 100%);

  /* Typography */
  --font-display: "Software Tester 7", "Lastica", "Inter", sans-serif;
  --font-heading: "Inter", "Montserrat", system-ui, sans-serif;
  --font-body: "Satoshi", "Montserrat", system-ui, sans-serif;

  --text-h1: 36px;
  --leading-h1: 44px;
  --text-h2: 28px;
  --leading-h2: 36px;
  --text-h3: 22px;
  --leading-h3: 30px;
  --text-h4: 18px;
  --leading-h4: 26px;
  --text-body: 16px;
  --leading-body: 24px;
  --text-small: 14px;
  --leading-small: 20px;
  --text-label: 12px;
  --leading-label: 16px;

  /* 8pt spacing */
  --space-1: 8px;
  --space-2: 16px;
  --space-3: 24px;
  --space-4: 32px;
  --space-5: 40px;
  --space-6: 48px;
  --space-8: 64px;
  --space-10: 80px;
  --space-12: 96px;

  /* Shape */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
  --radius-full: 9999px;

  /* Motion */
  --duration-fast: 160ms;
  --duration-base: 280ms;
  --duration-slow: 520ms;
  --ease-brand: cubic-bezier(0.22, 1, 0.36, 1);

  /* Elevation */
  --shadow-card: 0 16px 48px rgb(11 15 43 / 10%);
}
```

### Tailwind v4 theme

```css
@theme {
  --color-navy: #0b0f2b;
  --color-purple: #652dff;
  --color-lime: #a6ff1a;
  --color-deep-purple: #2c0f63;
  --color-aqua: #00d4c1;
  --color-electric-blue: #382bff;
  --color-pink: #ff4da6;
  --color-yellow: #ffc83d;
  --color-lavender: #9a8cff;
  --color-state-gray: #1b1f2e;
  --color-neutral-100: #f3f4f8;

  --font-display: "Software Tester 7", "Lastica", "Inter", sans-serif;
  --font-heading: "Inter", "Montserrat", system-ui, sans-serif;
  --font-body: "Satoshi", "Montserrat", system-ui, sans-serif;

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 24px;
}
```

---

## 15. Agent Prompt Guide

When generating or editing a P2P Labs website, follow this direction:

> Create a premium creator-economy technology experience for P2P Labs. Use a bright-first canvas, Deep Navy typography, Vivid Purple brand moments, and Lime only as a growth accent. Build on a modular 12-column grid with generous whitespace, strong Inter headings, readable Satoshi or Montserrat body copy, and restrained creator-tech gradients. Use authentic product UI, data, connected geometry, dot patterns, and selective 3D elements. Keep the composition modern, asymmetric, confident, and enterprise credible. Avoid generic SaaS card grids, excessive glassmorphism, an all-dark-purple canvas, random gradient blobs, childish illustration, and purposeless animation.

### Example component prompts

1. **Hero:** Bright white canvas with a 7/5 asymmetric grid. Deep Navy editorial headline, one phrase in Vivid Purple, concise body copy, one purple primary CTA, one text secondary action, and a signature connected-path visual using the Purple-to-Lime gradient. Use gentle layered motion and generous whitespace.

2. **Platform feature:** Neutral 100 background with a large 24px-radius feature panel. Pair real product UI with a short value-led headline, supporting metric or proof, and a visible next action. Purple is the primary chart series; Aqua, Blue, Pink, and Yellow support data differentiation.

3. **Creator ecosystem:** Use linked nodes, authentic creator imagery, and modular content blocks to show People + Partners + Peer-to-Peer + Labs. Keep text readable and avoid a generic logo cloud.

4. **Primary CTA:** Vivid Purple surface with white text, 48px height, 12px radius, visible focus ring, and a small directional arrow. Hover with a restrained lift and no neon glow.

5. **Dark trust section:** Deep Navy surface with white typography, Soft Lavender supporting copy, and a small Lime growth signal. Use one strong visualization or proof point rather than many floating cards.

---

## 16. Quality Gate

Before shipping, verify:

- Approved P2P Labs logo asset and lockup are used correctly.
- Corporate colors are not confused with P2P Network sub-brand colors.
- White/light surfaces remain the dominant canvas.
- Typography follows the marketing or product hierarchy intentionally.
- CTA hierarchy is obvious and Lime is used only as a growth accent.
- Desktop, tablet, and mobile layouts are deliberately recomposed.
- No horizontal overflow, text clipping, or crowded card stacks.
- Contrast, focus, touch targets, labels, errors, and reduced motion are accessible.
- Animation remains smooth and purposeful.
- Copy is concise, outcome-led, and does not invent claims.
- The finished experience feels creator-led, connected, scalable, and unmistakably P2P Labs.
