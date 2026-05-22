\---  
version: v2-tech-premium  
name: Adhoc  
description: \>  
  Design system for Adhoc — Partner \#1 de Odoo a nivel mundial. ERP  
  consultancy for Argentine SMBs. v2 refines the system toward tech-premium:  
  flat surfaces, no shadows, no color strokes, subtle grey borders, squircle  
  buttons, and violet reserved exclusively for buttons.  
\---

\# Adhoc Brand Kit — v2 (Tech Premium)

\---

\#\# CHANGELOG v1 → v2

\- Violet (\`\#7C6CD8\`) is now \*\*exclusively used for buttons\*\*. No longer used for links, active states, focus rings, tags, or icon fills.  
\- Coral and Mustard are \*\*accent-only\*\*: restricted to icons and illustrations. Never used for cards, backgrounds, hover states, strokes, or active states.  
\- \*\*No shadows\*\* anywhere in the system. \`elevation\` tokens are deprecated.  
\- \*\*No color strokes\*\*. All borders use grey tokens only — two levels: subtle and strong-subtle.  
\- \*\*Buttons are squircle\*\* with a fixed \`border-radius: 12px\`. Not pill-shaped.  
\- \*\*Cards are squircle\*\* with a proportional \`border-radius: 22%\` of the element's smaller dimension (Apple-style).  
\- \*\*Surface inversion rule\*\*: when the page background is \`\#FFFFFF\` (white), cards use \`\#E9E5DF\` (canvas/beige) as their surface. When the page background is \`\#E9E5DF\`, cards use \`\#FFFFFF\` as their surface. This applies across web, social, and presentations.  
\- Tags/pills: lavender text on a very-light lavender fill (low-opacity Notion style). No colored outlines.  
\- Ghost button: ink text, not violet text.

\---

\#\# Colors

\#\#\# Core neutrals

\- \*\*Ink — \`\#000000\`\*\* Negro. Body text, headings, illustration linework, logo wordmark on light backgrounds. Pure black; do not soften.  
\- \*\*Canvas — \`\#E9E5DF\`\*\* Beige. Default page background OR card surface, depending on context (see Surface Inversion Rule below). Warm, paper-like.  
\- \*\*Surface — \`\#FFFFFF\`\*\* White. Default card surface OR page background, depending on context. Never used simultaneously as both background and card on the same section.  
\- \*\*Text Secondary — \`\#4A4A4A\`\*\* For supporting body copy, captions, and secondary labels.

\#\#\# Surface Inversion Rule

The system operates in two modes that can coexist on the same page across different sections:

| Page/Section Background | Card Surface |  
|---|---|  
| \`\#FFFFFF\` (white) | \`\#E9E5DF\` (canvas/beige) |  
| \`\#E9E5DF\` (canvas/beige) | \`\#FFFFFF\` (white) |

\*\*Rule\*\*: canvas and white always contrast each other — one is always the ground, the other is always the figure. Never use the same color for both background and card in the same section. This applies to web, social placas, and presentations.

\#\#\# Brand — violet (buttons only)

Violet is the brand's primary color but its usage is now strictly limited to buttons.

\- \*\*Primary — \`\#7C6CD8\` Violeta.\*\* Used ONLY on buttons: \`button-primary\` fill and \`button-ghost\` text. Do not use for links, active states, focus indicators, tags, icon fills, or any surface. Pantone 2726 C.  
\- \*\*Primary-container — \`\#BCAFEF\` Lavanda.\*\* Used ONLY as the text color on tags/chips, and as a tint base for the tag fill (see Tags section). Not used for cards, backgrounds, or interactive states. Pantone 2716 C.  
\- \*\*Tag fill — \`\#EDE9FB\`\*\* A very light lavender (\~15% opacity of \`\#BCAFEF\` on white). Used exclusively as the background fill of tags/chips. Not a standalone brand color — derived from lavender for the tag component only.

\#\#\# Accents (illustrations and icons only)

Coral and mustard are accent colors. Their usage is strictly limited to illustration fills and icon colorization. They must never appear in: cards, backgrounds, hover states, active states, borders/strokes, CTA buttons, badges, or any interactive element.

\- \*\*Secondary — \`\#FF7348\` Coral.\*\* Illustration fills, icon accents only. Pantone 7417 C.  
\- \*\*Tertiary — \`\#FEA912\` Mostaza.\*\* Illustration fills, icon accents only. Pantone 137 C.

\#\#\# Borders (two levels, grey only)

No color strokes anywhere. All borders use neutral grey.

\- \*\*Border Subtle — \`\#EBEBEB\`\*\* Default border for cards, containers, and dividers. Almost imperceptible — creates structure without visual weight.  
\- \*\*Border Medium — \`\#D4CFC6\`\*\* For inputs, modals, and elements that need slightly more definition. Still restrained — not a strong line.

Do not use brand colors (violet, coral, mustard, lavender) as border or stroke colors anywhere in the system.

\#\#\# Feedback tokens (brand palette reuse)

\- \`success\` → \`\#7C6CD8\` (violet)  
\- \`warning\` → \`\#FEA912\` (mustard)  
\- \`error\` → \`\#FF7348\` (coral)  
\- \`info\` → \`\#BCAFEF\` (lavender)

Feedback tokens appear only in system messages, form validation states, and alerts — not in marketing or decorative contexts.

\#\#\# Dark mode (reserved)

Dark mode tokens exist for forward compatibility. Not active in v2.

\- \`dark-canvas: \#1A1A1A\`  
\- \`dark-surface: \#262626\`  
\- \`dark-on-canvas: \#E9E5DF\`

\---

\#\# Typography

Two families, deliberately contrasted: \*\*New Kansas\*\* (serif display, editorial) and \*\*Apercu Pro\*\* (humanist sans, UI).

\#\#\# New Kansas — editorial display

Contemporary serif with strong character. Used for: H1–H3 on web and docs, big headlines on social placas, section openers in presentations, brand statements and taglines. Default weight: Medium (500). Do not use below 18px.

\#\#\# Apercu Pro — humanist sans

Geometric-humanist hybrid. Used for: all body copy, UI elements (buttons, inputs, labels, navigation, tooltips), microcopy, captions, H4 and H5, all-caps overlines. Default weight: Regular (400) for body, Medium (500) for labels/buttons, Bold (700) for H4/H5.

\#\#\# Type tokens

\*\*Display\*\*  
\- \`display-xl\`: New Kansas, 4.5rem, weight 500, line-height 1.05, letter-spacing \-0.02em  
\- \`display-lg\`: New Kansas, 3.5rem, weight 500, line-height 1.1, letter-spacing \-0.015em  
\- \`display-md\`: New Kansas, 2.5rem, weight 500, line-height 1.15, letter-spacing \-0.01em

\*\*Headings\*\*  
\- \`h1\`: New Kansas, 3rem, weight 500, line-height 1.15  
\- \`h2\`: New Kansas, 2.25rem, weight 500, line-height 1.2  
\- \`h3\`: New Kansas, 1.75rem, weight 500, line-height 1.25  
\- \`h4\`: Apercu Pro, 1.375rem, weight 700, line-height 1.3  
\- \`h5\`: Apercu Pro, 1.125rem, weight 700, line-height 1.35

\*\*Body\*\*  
\- \`body-lg\`: Apercu Pro, 1.125rem, weight 400, line-height 1.55  
\- \`body-md\`: Apercu Pro, 1rem, weight 400, line-height 1.55  
\- \`body-sm\`: Apercu Pro, 0.875rem, weight 400, line-height 1.5  
\- \`body-md-bold\`: Apercu Pro, 1rem, weight 700, line-height 1.55

\*\*UI\*\*  
\- \`label-md\`: Apercu Pro, 0.875rem, weight 500, line-height 1.4  
\- \`label-sm\`: Apercu Pro, 0.75rem, weight 500, line-height 1.4, letter-spacing 0.02em  
\- \`button\`: Apercu Pro, 1rem, weight 500, line-height 1  
\- \`caption\`: Apercu Pro, 0.75rem, weight 400, line-height 1.4  
\- \`overline\`: Apercu Pro, 0.75rem, weight 500, line-height 1.3, letter-spacing 0.08em

\#\#\# Fallbacks

\- New Kansas unavailable → \`Georgia, "Times New Roman", serif\`  
\- Apercu Pro unavailable → \`"Inter", \-apple-system, "Segoe UI", sans-serif\`

\---

\#\# Spacing

Based on 4px, with 8px as the primary unit.

| Token | Value | Typical use |  
|---|---|---|  
| \`xxs\` | 4px | — |  
| \`xs\` | 8px | — |  
| \`sm\` | 12px | — |  
| \`md\` | 16px | Component internals |  
| \`lg\` | 24px | Component internals |  
| \`xl\` | 32px | Section separation |  
| \`2xl\` | 48px | Section separation |  
| \`3xl\` | 64px | Page rhythm |  
| \`4xl\` | 96px | Page rhythm |

\---

\#\# Shape (Border Radius)

| Token | Value | Usage |  
|---|---|---|  
| \`radius-none\` | 0px | Never |  
| \`radius-xs\` | 4px | — |  
| \`radius-sm\` | 8px | Small internal elements |  
| \`radius-md\` | 12px | \*\*Buttons\*\* (fixed squircle) |  
| \`radius-lg\` | 20px | Standard cards (alternative) |  
| \`radius-xl\` | 28px | App-icon tiles |  
| \`radius-squircle\` | 22% | \*\*Cards\*\* (Apple-style proportional radius) |

\#\#\# Shape rules

\- \*\*Buttons\*\* — fixed \`border-radius: 12px\`. Squircle. Not pill-shaped. Applies to all button variants.  
\- \*\*Cards\*\* — proportional squircle: \`border-radius\` set to approximately 22% of the card's smaller dimension. Implemented as \`border-radius: clamp(16px, 2.75vw, 32px)\` or as a fixed \`24–28px\` depending on card size. For small cards (\~120px), use \`24px\`. For large cards (\>280px), use \`32px\`.  
\- \*\*App-icon tiles\*\* — fixed \`border-radius: 28px\` (squircle for 96×96 icons).  
\- \*\*Inputs\*\* — \`border-radius: 8px\`.  
\- \*\*Tags/chips\*\* — \`border-radius: 6px\`. Slightly rounded rectangle, not pill.  
\- \*\*Sharp corners\*\* — never. No right-angle corners anywhere.

\---

\#\# Elevation (Deprecated in v2)

\*\*Shadows are not used in v2.\*\* The tech-premium aesthetic is achieved through surface contrast (canvas vs. white), subtle borders, and clean typography — not depth. All \`elevation\` tokens from v1 are deprecated.

Do not apply \`box-shadow\` to any element. If layering is needed (modals, popovers), communicate hierarchy through background color contrast and border-subtle only.

\---

\#\# Components

\#\#\# Buttons

Squircle (\`border-radius: 12px\`), always. Four variants with clear hierarchy. Violet appears only on \`button-primary\` (fill) and \`button-ghost\` (text).

\*\*button-primary\*\*  
\- Background: \`\#7C6CD8\` (violet)  
\- Text: \`\#FFFFFF\`  
\- Border: none  
\- Border-radius: 12px  
\- Padding: 12px 24px  
\- Font: \`button\` (Apercu Pro, 1rem, weight 500\)  
\- Hover: background \`\#6B5CC4\`  
\- Focus: outline 2px \`\#7C6CD8\`, offset 2px

\*\*button-secondary\*\*  
\- Background: \`\#000000\` (ink)  
\- Text: \`\#FFFFFF\`  
\- Border: none  
\- Border-radius: 12px  
\- Padding: 12px 24px  
\- Font: \`button\`  
\- Hover: background \`\#222222\`  
\- Note: coral is no longer used as a button fill in v2. The secondary CTA uses ink fill for a clean, tech-premium look.

\*\*button-outline\*\*  
\- Background: transparent  
\- Text: \`\#000000\` (ink)  
\- Border: 1px solid \`\#EBEBEB\` (border-subtle)  
\- Border-radius: 12px  
\- Padding: 12px 24px  
\- Font: \`button\`  
\- Hover: background \`\#F5F5F5\`

\*\*button-ghost\*\*  
\- Background: transparent  
\- Text: \`\#7C6CD8\` (violet)  
\- Border: none  
\- Border-radius: 12px  
\- Padding: 12px 24px  
\- Font: \`button\`  
\- Hover: background \`\#F3F1FD\` (very light lavender tint)

\*\*Interaction rules\*\*  
\- No shadows on any button state (hover, focus, active).  
\- Focus state: 2px outline, not inset border-shadow.  
\- Coral and mustard are never used as button fills.  
\- Only one violet-fill button per screen. Ghost (violet text) can coexist with it.

\---

\#\#\# Cards

Cards are the primary content container. Squircle shape, no shadow, thin neutral border only.

\*\*card-default\*\*  
\- Background: follows Surface Inversion Rule (white on canvas background; canvas on white background)  
\- Border: 1px solid \`\#EBEBEB\` (border-subtle)  
\- Border-radius: proportional squircle (\~22% of smaller dimension; typical fixed value 24–32px)  
\- Padding: 24px  
\- Shadow: none

\*\*card-strong-border\*\*  
\- Same as card-default but border: 1px solid \`\#D4CFC6\` (border-medium)  
\- Use when more definition is needed (e.g. inside dense grids)

\*\*Rules for cards\*\*  
\- No colored borders. No coral, violet, mustard, or lavender strokes.  
\- No shadows.  
\- No filled cards with brand accent colors (coral-filled, mustard-filled cards are retired in v2).  
\- Surface color always contrasts the page background per the Surface Inversion Rule.  
\- Cards on white pages → beige fill. Cards on beige pages → white fill.

\---

\#\#\# Tags & Chips

Tags are categorical markers ("Caso de éxito", "Manufactura", "Workshop") and small interactive chips.

\*\*tag-default\*\*  
\- Background: \`\#EDE9FB\` (very light lavender, \~15% opacity lavender on white)  
\- Text: \`\#BCAFEF\` (lavender)  
\- Border: none  
\- Border-radius: 6px  
\- Padding: 5px 12px  
\- Font: \`label-sm\` (Apercu Pro, 0.75rem, weight 500\)

\*\*Rules for tags\*\*  
\- Never use coral, mustard, or full-weight violet as tag colors.  
\- No pill shape (999px radius) for tags in v2 — use 6px radius instead.  
\- Do not use colored borders/outlines on tags.  
\- The "Notion-style" low-opacity lavender fill is the single tag style for UI contexts.  
\- In social placas, the editorial pill shape (pill radius) may still be used for large display tags as a visual device — but the lavender fill rule still applies.

\---

\#\#\# Inputs

\*\*input-default\*\*  
\- Background: white (or canvas, per inversion rule)  
\- Text: \`\#000000\` (ink)  
\- Placeholder: \`\#4A4A4A\` (text-secondary)  
\- Border: 1px solid \`\#D4CFC6\` (border-medium) — inputs need slightly more definition than cards  
\- Border-radius: 8px  
\- Padding: 12px 14px  
\- Font: \`body-md\`  
\- Focus state: border-color \`\#7C6CD8\` (violet), no shadow

\---

\#\#\# App-icon tiles (Odoo modules)

\- Background: follows Surface Inversion Rule (adapts to page context)  
\- Border: 1px solid \`\#EBEBEB\`  
\- Border-radius: 28px (fixed squircle for 96×96 icons)  
\- Padding: 16px  
\- Size: 96×96px  
\- Shadow: none  
\- Icon inside: bicolor violet/lavender illustration with black accent mark (SVG from \`assets/icons/odoo/\`)

\---

\#\#\# Navigation

\- Background: transparent  
\- Text: \`\#000000\` (ink)  
\- Active/hover: text remains ink, no color change — use weight or underline for active state  
\- Font: \`label-md\`  
\- Do not use violet for nav active states

\---

\#\# Layout

\#\#\# Grid & breakpoints

\- \*\*Web content\*\*: 12-column grid, max content width 1200px, gutters 24–32px.  
\- \*\*Social placas\*\*: 1:1 (1080×1080), 4:5 (1080×1350), 9:16 (1080×1920). Safe zone: 72px all sides for stories.  
\- \*\*Presentations\*\*: 16:9, 1920×1080. Margins minimum 64px from edge.

\#\#\# Page rhythm

The page alternates between white and canvas sections. Each alternation creates natural contrast without needing dividers, colored bands, or decorative separators. The mustard wave divider from v1 is optional — use it only for social and editorial contexts, not as a default web pattern.

\---

\#\# Illustrations & Icons

\*\*Illustrations\*\*: hand-drawn line style, imperfect contours, flat fills using coral and mustard as primary accent colors. Violet and lavender can appear as secondary fills within illustrations. Faces are simple, expressive. No gradients. No 3D renders.

\*\*Accent usage in illustrations\*\*: coral and mustard may appear freely in illustration fills. This is their primary sanctioned use in v2.

\*\*Iconography\*\*: if no Adhoc asset exists, match the stroke style — 2px rounded-cap line in ink, with a single flat fill from coral or mustard. Violet and lavender are secondary options for icon fills.

\---

\#\# Photography

Real team members, expressive gestures, against solid color backdrops from the palette (mustard, coral, lavender). People in Adhoc t-shirts on brand backdrops. Office shots: warm, natural light, plants, real people working.

\---

\#\# Do's and Don'ts (v2)

\#\#\# Do

\- Use Canvas (\`\#E9E5DF\`) and White (\`\#FFFFFF\`) as the two surface levels, always contrasting each other.  
\- Use violet (\`\#7C6CD8\`) exclusively for buttons (fill on primary, text on ghost).  
\- Use squircle shape (12px fixed radius) on all buttons.  
\- Use proportional squircle (\~22%) on all cards.  
\- Use only grey borders: \`\#EBEBEB\` (subtle) or \`\#D4CFC6\` (medium).  
\- Use the low-opacity lavender fill (\`\#EDE9FB\`) with lavender text (\`\#BCAFEF\`) for all tags.  
\- Use coral and mustard only inside illustrations and icons.  
\- Use New Kansas for headlines, Apercu Pro for body and UI.  
\- Write copy in Argentine Spanish with voseo, warm tone.

\#\#\# Don't

\- Don't use violet for links, active states, focus rings, tag fills, nav highlights, or icon fills.  
\- Don't use coral or mustard for cards, backgrounds, hover states, button fills, strokes, badges, or active indicators.  
\- Don't use colored borders or strokes — grey only.  
\- Don't add shadows to any element.  
\- Don't use pill-shaped buttons (999px radius). Buttons are 12px radius.  
\- Don't use the same surface color for both background and card in the same section.  
\- Don't use gradient text, neon glows, or glassmorphism.  
\- Don't use sharp corners anywhere.  
\- Don't introduce hues outside the six-color palette.  
\- Don't use New Kansas for body copy.  
\- Don't recolor the logo.

\---

\#\# Assets

\#\#\# Fonts

| File | Family | Weight | Use |  
|---|---|---|---|  
| \`assets/fonts/NewKansas-Medium.otf\` | New Kansas | 500 | Default display weight — headlines, hero type |  
| \`assets/fonts/NewKansas-SemiBold.otf\` | New Kansas | 600 | Emphatic display |  
| \`assets/fonts/NewKansas-Bold.otf\` | New Kansas | 700 | Poster-scale display |  
| \`assets/fonts/NewKansas-RegularItalic.otf\` | New Kansas | 400 italic | Editorial accent |  
| \`assets/fonts/ApercuPro-Regular.ttf\` | Apercu Pro | 400 | Default body weight |  
| \`assets/fonts/ApercuPro-Medium.ttf\` | Apercu Pro | 500 | Buttons, labels, UI |  
| \`assets/fonts/ApercuPro-Bold.ttf\` | Apercu Pro | 700 | Emphasis, H4–H5 |  
| \`assets/fonts/ApercuPro-Italic.ttf\` | Apercu Pro | 400 italic | Inline emphasis |

\#\#\# Logo files

| File | Use when |  
|---|---|  
| \`assets/logo/logo-primary.svg\` | Wordmark \+ isotype on light or beige backgrounds |  
| \`assets/logo/logo-inverse.svg\` | Wordmark \+ isotype on dark or saturated backgrounds |  
| \`assets/logo/isotipo.svg\` | Standalone mark — favicon, profile avatar, watermark |

\#\#\# Backgrounds

| File | Use |  
|---|---|  
| \`assets/backgrounds/mesh-lavender-1.jpg\` to \`-4.jpg\` | Soft lavender mesh on cream. Valid for hero sections and social placas. Not for web card backgrounds. |

\#\#\# Icons — Odoo modules

\`assets/icons/odoo/\` — 24 modules: \`ai\`, \`articulos\`, \`compras\`, \`conversaciones\`, \`crm\`, \`documentos\`, \`email-marketing\`, \`empleados\`, \`estudio\`, \`firma\`, \`horarios\`, \`inventario\`, \`manufactura\`, \`planeacion\`, \`proyectos\`, \`punto-venta\`, \`redes-sociales\`, \`servicios\`, \`soporte\`, \`suscripciones\`, \`tablero\`, \`ventas\`, \`vacaciones\`, \`website\`.

Each icon is bicolor violet/lavender with black accent mark. Render in \`app-icon\` tile (squircle, 28px radius, no shadow, subtle border).

\---

\#\# Agent Notes (v2)

Rules for AI coding assistants and conversational AIs consuming this file:

\- \*\*Violet is buttons-only.\*\* Any use of \`\#7C6CD8\` outside of \`button-primary\` fill or \`button-ghost\` text is a violation.  
\- \*\*No shadows.\*\* \`box-shadow\` is not used anywhere. If you generate a shadow, remove it.  
\- \*\*No color borders.\*\* Any border using a brand color (violet, coral, mustard, lavender) is a violation. Use \`\#EBEBEB\` or \`\#D4CFC6\` only.  
\- \*\*Buttons are \`border-radius: 12px\`.\*\* Not 999px. Not 20px. 12px.  
\- \*\*Cards are proportional squircle.\*\* Use \`border-radius: clamp(16px, 22%, 32px)\` or a fixed value between 24–32px depending on card size.  
\- \*\*Surface inversion is mandatory.\*\* Before placing a card, check the section background. Canvas background → white card. White background → canvas card.  
\- \*\*Tags are \`\#EDE9FB\` fill, \`\#BCAFEF\` text, \`border-radius: 6px\`.\*\* Not pills. Not colored outlines.  
\- \*\*Coral and mustard appear only in illustrations and icons.\*\* Never in UI.  
\- \*\*Language is Argentine Spanish with voseo.\*\* Warm tone, never corporate.  
\- \*\*Study examples before generating.\*\* Files in \`examples/\` are the ground-truth for visual output.  
