# Adhoc — Frontend Handoff README (v2 — actualizado mayo 2026)

> Este README fue sincronizado con los HTML de referencia en mayo 2026.
> Los HTML en /reference/ siguen siendo la fuente de verdad visual.
> Ante conflicto, los HTML ganan.

**Proyecto:** Rediseño web Ad Hoc (partner #1 de Odoo en Latinoamérica)  
**Stack:** Astro (static output) + HTML/CSS/JS vanilla dentro de componentes  
**Objetivo de negocio:** Generar demos agendadas ("Solicitar una demo") como única conversión primaria  
**Audiencia:** Juan — dueño de PyME B2B (distribución, servicios, manufactura, educación) que hoy gestiona con Excel

---

## Contexto del proyecto

Este repositorio contiene el frontend completo del sitio rediseñado de Ad Hoc. El diseño fue validado y prototipado en HTML estático antes del handoff. La migración a Astro es el primer paso de este handoff: los archivos `.html` existentes son la fuente de verdad visual; la tarea es convertirlos a componentes Astro manteniendo fidelidad exacta al diseño.

**Archivos HTML de referencia (en la raíz del proyecto original):**
- `adhoc-homepage.html` → página principal
- `adhoc-pricing.html` → página de precios
- `adhoc-mega-nav.html` → componente de navegación
- `adhoc-cotizador.html` → flujo del cotizador (modal/overlay, no página)
- `adhoc-feature-tabs.html` → componente de tabs de features (sección de homepage)
- `adhoc-design-system.html` → referencia visual del design system

Estos archivos **no se eliminan**. Son la referencia de diseño durante toda la implementación.

---

## Stack y justificación

| Decisión | Elección | Razón |
|---|---|---|
| Framework | **Astro** | Output HTML estático, componentes reutilizables, sin backend requerido |
| Estilos | **CSS custom properties + CSS módulos por componente** | Design tokens nativos sin dependencia de Tailwind |
| JS | **Vanilla JS** (Alpine.js opcional para interactividad ligera) | Sin overhead de framework JS para un sitio mayormente estático |
| Fonts | Archivos locales en `/public/fonts/` | Licencia comercial — no se sirven desde CDN |
| Deploy | **Vercel o Netlify** (estático) | Output `dist/` listo para deploy sin configuración adicional |

> **Nota sobre Alpine.js:** Si algún componente requiere estado reactivo liviano (mega-nav, cotizador), Alpine.js es la opción preferida sobre React/Vue para mantener la simplicidad del stack.

---

## Estructura del repositorio

```
adhoc-web/
├── public/
│   ├── fonts/
│   │   ├── NewKansas-Medium.otf
│   │   ├── NewKansas-SemiBold.otf
│   │   ├── NewKansas-Bold.otf
│   │   ├── NewKansas-RegularItalic.otf
│   │   ├── ApercuPro-Regular.ttf
│   │   ├── ApercuPro-Medium.ttf
│   │   ├── ApercuPro-Bold.ttf
│   │   └── ApercuPro-Italic.ttf
│   ├── logos/
│   │   ├── logo-primary.svg
│   │   ├── logo-inverse.svg
│   │   └── isotipo.svg
│   ├── icons/
│   │   └── odoo/          ← íconos SVG de módulos Odoo (24 módulos)
│   └── images/
│       └── backgrounds/
│           ├── mesh-lavender-1.jpg
│           ├── mesh-lavender-2.jpg
│           ├── mesh-lavender-3.jpg
│           └── mesh-lavender-4.jpg
│
├── src/
│   ├── styles/
│   │   ├── tokens.css         ← ÚNICA fuente de verdad de design tokens
│   │   ├── typography.css     ← @font-face + clases tipográficas
│   │   ├── reset.css          ← reset minimalista
│   │   └── global.css         ← importa todo lo anterior
│   │
│   ├── components/
│   │   ├── MegaNav.astro        ← navegación principal (se repite en todas las páginas)
│   │   ├── Cotizador.astro      ← flujo multi-step (modal, trigger desde CTA)
│   │   ├── Footer.astro
│   │   ├── Button.astro         ← componente de botón con variantes
│   │   ├── Tag.astro            ← chip/tag lavanda estilo Notion
│   │   ├── Card.astro           ← card con squircle y surface inversion
│   │   ├── AppIcon.astro        ← tile de módulo Odoo (squircle 28px)
│   │   ├── HeroDashboard.astro  ← mockup de dashboard Odoo (usado solo en Hero de Home)
│   │   └── Wave.astro           ← transición SVG entre secciones (usado en Integraciones)
│   │
│   ├── layouts/
│   │   └── Base.astro         ← layout base: <head>, MegaNav, Footer, Cotizador
│   │
│   └── pages/
│       ├── index.astro           ← Home
│       ├── pricing.astro         ← Pricing
│       └── industrias/
│           ├── manufactura.astro
│           ├── comercializadora.astro
│           ├── servicios.astro
│           └── educacion.astro
│
├── reference/                 ← prototipos HTML originales (no tocar)
│   ├── adhoc-homepage.html
│   ├── adhoc-pricing.html
│   ├── adhoc-mega-nav.html
│   ├── adhoc-cotizador.html
│   ├── adhoc-feature-tabs.html
│   └── adhoc-design-system.html
│
├── astro.config.mjs
├── package.json
└── README.md
```

---

## Design System — Tokens CSS

**Este archivo (`tokens.css`) es la única fuente de verdad. Nunca hardcodear valores.**

```css
/* src/styles/tokens.css */

:root {
  /* ─── Superficies ─── */
  --color-canvas: #E9E5DF;
  --color-surface: #FFFFFF;
  --color-ink: #000000;
  --color-text-secondary: #4A4A4A;

  /* ─── Violeta — SOLO BOTONES ─── */
  --color-primary: #7C6CD8;
  --color-primary-hover: #6B5CC4;
  --color-primary-focus: #7C6CD8;

  /* ─── Lavanda — SOLO TAGS ─── */
  --color-lavender: #BCAFEF;
  --color-lavender-fill: #EDE9FB;   /* fill de tag (~15% opacity) */

  /* ─── Acentos — SOLO íconos e ilustraciones ─── */
  --color-coral: #FF7348;
  --color-mustard: #FEA912;

  /* ─── Bordes (grises únicamente) ─── */
  --border-subtle: #EBEBEB;         /* cards, dividers, contenedores */
  --border-medium: #D4CFC6;         /* inputs, modales, elementos con más definición */

  /* ─── Border radius ─── */
  --radius-button: 12px;            /* botones — squircle fijo */
  --radius-input: 8px;              /* inputs */
  --radius-tag: 6px;                /* tags/chips */
  --radius-icon-tile: 28px;         /* app-icon tiles Odoo */
  /* cards: squircle proporcional — ver sección Cards */

  /* ─── Spacing ─── */
  --space-xxs: 4px;
  --space-xs: 8px;
  --space-sm: 12px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;
  --space-4xl: 96px;

  /* ─── Elevación: DEPRECATED en v2 ─── */
  /* No usar box-shadow en ningún elemento */
}
```

---

## Reglas de diseño críticas

Estas reglas no son negociables. Cualquier implementación que las viole debe corregirse antes de hacer PR.

### 1. Violeta — exclusivamente botones

`#7C6CD8` aparece **únicamente** en:
- `button-primary`: fill de fondo
- `button-ghost`: color de texto

**No usar violeta para:** links, estados activos, focus rings, borders, tags, íconos, hover states, nav highlights.

### 2. Coral y mostaza — exclusivamente ilustraciones e íconos

`#FF7348` y `#FEA912` **no aparecen en UI**. Solo dentro de archivos SVG de ilustraciones e íconos.

Específicamente **prohibido** usarlos en: cards, fondos de sección, hover states, badges, borders, botones, estados activos, cualquier elemento interactivo.

### 3. Sin shadows

`box-shadow` no se usa en ningún elemento del sitio. La jerarquía visual se comunica únicamente mediante contraste de superficies y bordes sutiles.

### 4. Sin borders de color

Todos los borders usan exclusivamente los tokens grises:
- `var(--border-subtle)` → `#EBEBEB` — cards, contenedores, dividers
- `var(--border-medium)` → `#D4CFC6` — inputs, modales

Nunca usar violeta, coral, mostaza o lavanda como border color.

### 5. Surface Inversion Rule

Canvas y Surface siempre contrastan entre sí. En cada sección:

| Fondo de sección | Superficie de card |
|---|---|
| `#FFFFFF` (blanco) | `#E9E5DF` (canvas/beige) |
| `#E9E5DF` (canvas/beige) | `#FFFFFF` (blanco) |

Nunca usar el mismo color para fondo y card dentro de la misma sección. Aplica a web, social y presentaciones.

### 6. Botones — squircle fijo 12px

```css
.btn {
  border-radius: var(--radius-button); /* 12px */
  /* NO usar border-radius: 999px */
  /* NO usar border-radius: 9999px */
}
```

### 7. Cards — squircle proporcional

```css
.card {
  border-radius: clamp(16px, 5vw, 32px);
  /* Para cards pequeñas (<160px): border-radius: 20px */
  /* Para cards grandes (>280px): border-radius: 32px */
  /* Nunca usar border-radius fijo igual en todas las cards */
}
```

### 8. Tags — estilo Notion

```css
.tag {
  background: var(--color-lavender-fill); /* #EDE9FB */
  color: var(--color-lavender);           /* #BCAFEF */
  border-radius: var(--radius-tag);       /* 6px */
  /* NO usar pill (999px) */
  /* NO usar borders de color */
  /* NO usar coral, mostaza, o violeta */
}
```

---

## Tipografía

### @font-face (en `typography.css`)

```css
/* New Kansas */
@font-face {
  font-family: 'New Kansas';
  src: url('/fonts/NewKansas-Medium.otf') format('opentype');
  font-weight: 500;
  font-display: swap;
}
@font-face {
  font-family: 'New Kansas';
  src: url('/fonts/NewKansas-SemiBold.otf') format('opentype');
  font-weight: 600;
  font-display: swap;
}
@font-face {
  font-family: 'New Kansas';
  src: url('/fonts/NewKansas-Bold.otf') format('opentype');
  font-weight: 700;
  font-display: swap;
}
@font-face {
  font-family: 'New Kansas';
  src: url('/fonts/NewKansas-RegularItalic.otf') format('opentype');
  font-weight: 400;
  font-style: italic;
  font-display: swap;
}

/* Apercu Pro */
@font-face {
  font-family: 'Apercu Pro';
  src: url('/fonts/ApercuPro-Regular.ttf') format('truetype');
  font-weight: 400;
  font-display: swap;
}
@font-face {
  font-family: 'Apercu Pro';
  src: url('/fonts/ApercuPro-Medium.ttf') format('truetype');
  font-weight: 500;
  font-display: swap;
}
@font-face {
  font-family: 'Apercu Pro';
  src: url('/fonts/ApercuPro-Bold.ttf') format('truetype');
  font-weight: 700;
  font-display: swap;
}
@font-face {
  font-family: 'Apercu Pro';
  src: url('/fonts/ApercuPro-Italic.ttf') format('truetype');
  font-weight: 400;
  font-style: italic;
  font-display: swap;
}
```

### Fallbacks

```css
--font-display: 'New Kansas', Georgia, 'Times New Roman', serif;
--font-body: 'Apercu Pro', 'Inter', -apple-system, 'Segoe UI', sans-serif;
```

### Reglas de uso

| Familia | Usar para | No usar para |
|---|---|---|
| New Kansas | H1, H2, H3, display headlines, taglines | Body copy, labels, botones, UI |
| Apercu Pro | Body, H4, H5, botones, labels, nav, inputs, captions | Headlines principales |

---

## Componentes

### MegaNav

**Archivo:** `src/components/MegaNav.astro`  
**Referencia:** `reference/adhoc-mega-nav.html`

Estructura de navegación:

```
Soluciones (dropdown) | Precios | Casos | Recursos
```

Solo "Soluciones" tiene mega-panel. Los otros tres son links estáticos.

**Estructura interna del dropdown de Soluciones:**

| Columna 1 | Columna 2 | Columna 3 |
|---|---|---|
| Por industria | Por tamaño | Featured card |
| Educación | En crecimiento | Caso de éxito con resultado cuantificado |
| Distribución | En escala | |
| Servicios | Enterprise | |
| Manufactura | | |

**CTA en nav:** `button-primary` violeta, texto "Solicitar demo"  
**Botón secundario:** "Ingresar" (link estático, sin estilo primario)

**Especificaciones de interacción:**
- Desktop: hover sobre "Soluciones" → abre mega-panel con animación opacity + translateY, ~200ms ease-out
- Mobile: bottom sheet, trigger por hamburger
- Links activos: ink (`#000000`), weight 500. Sin highlight de color
- Nav border: `border-bottom: 1px solid var(--border-subtle)`
- Sin background de color en el nav

**Importante:** MegaNav se importa en `Base.astro`. No duplicar en páginas individuales.

---

### Cotizador

**Archivo:** `src/components/Cotizador.astro`  
**Referencia:** `reference/adhoc-cotizador.html`  
**Trigger:** click en "Solicitar una demo" desde nav o cualquier CTA

Modal/overlay multi-step. 4 data-steps: 3 preguntas + pantalla de resultado.

**Flujo:**

```
Paso 1 (Pregunta 1 de 3): ¿En qué rubro opera tu empresa?
  → Radio cards con auto-avance al seleccionar
  → Opciones: Manufactura / Distribución / Servicios / Educación

Paso 2 (Pregunta 2 de 3): ¿Qué herramienta usás hoy?
  → Radio cards con auto-avance al seleccionar
  → Opciones: Excel / Sistema propio que quedó chico /
              Varios sistemas desconectados / Nada formal

Paso 3 (Pregunta 3 de 3): ¿Cuántos usuarios necesitarían acceso?
  → Radio cards con auto-avance al seleccionar
  → Rangos: 1–5 / 6–30 / 31–60 / 60+

Paso 4 (Resultado): Plan recomendado + CTAs
  → "Agendar llamada" + "Hablar con un asesor"
```

**Reglas de interacción:**
- Todos los pasos usan radio cards con auto-avance
- Sin botón "Continuar" — la selección avanza sola
- Progress indicator: texto "Pregunta X de 3" (no barra visual)
- Escape o click fuera → cierra el modal
- Back button dentro del modal para volver al paso anterior
- Sin recarga de página — JS puro en el cliente

**Diseño del modal:**
- Overlay: `rgba(0,0,0,0.4)`
- Card: fondo blanco, `border-radius: clamp(20px, 3vw, 32px)`, sin shadow, `border: 1px solid var(--border-subtle)`
- Ancho máximo: 560px, centrado vertical y horizontal
- Padding: 40px desktop / 24px mobile

---

### Feature Tabs

**Archivo:** `src/components/FeatureTabs.astro`  
**Referencia:** `reference/adhoc-feature-tabs.html`

> **Nota técnica:** El HTML de referencia implementa este componente en React (JSX con Babel). Esto es deuda técnica del prototipo. La implementación en Astro usa **vanilla JS**, consistente con el stack del proyecto. No usar React ni Alpine para este componente.

**Tabs (6 en total):**
1. Automatizar operaciones
2. Integrar áreas
3. Escalar con control
4. Ganar visibilidad
5. Control financiero
6. Digitalizar el negocio

**Comportamiento:**
- Tab activo: fondo del card cambia a color único por feature (violeta, coral, mostaza, lavanda, negro, canvas)
- Tab label activo: color ink (`var(--ink)`) en todos los casos
- Transición: `opacity 200ms ease`
- Vanilla JS — sin React, sin Alpine

---

### Páginas

#### Home (`src/pages/index.astro`)

**Referencia:** `reference/adhoc-homepage.html`

Estructura de secciones en orden:

```
 1. Hero              — canvas  — headline, 2 CTAs, trust strip + logos,
                                  HeroDashboard.astro sangrado en la parte inferior

 2. Rubros + Métricas — surface — UNA SOLA <section> con sec--sticky-base
                                  Rubros arriba (sticky tabs desktop / cards mobile)
                                  Métricas debajo (4 números), mismo fondo, sin separador
                                  POSICIÓN: sticky — es tapada por Features al scrollear

 3. Features          — ink     — 6 tabs, color de card único por feature
                                  EFECTO ENTRADA: border-radius 32px 32px 0 0
                                  Z-INDEX: 2 sobre Rubros+Métricas sticky

 4. Casos             — surface — card featured (RE/MAX) + 6 mini cards + ticker animado

 5. Proceso           — canvas  — 3 cards: Diagnóstico, Implementación, Optimización continua
                                  POSICIÓN: sticky — es tapada por Integraciones al scrollear

 6. Integraciones     — ink     — Wave.astro + AppIcons (pendiente)
                                  EFECTO ENTRADA: border-radius 32px 32px 0 0
                                  Z-INDEX: 2 sobre Proceso sticky

 7. FAQ               — surface — 5 preguntas, accordion con height transition

 8. Contact form      — canvas  — formulario: nombre, email, empresa + checklist

 9. Footer
```

**Efecto de entrada — secciones ink (3 y 6):**

Las secciones ink se "tapan" sobre la sección anterior mediante scroll:
- La sección ink tiene `border-radius: 32px 32px 0 0` y `z-index: 2`
- La sección que la precede tiene `position: sticky; top: 0; z-index: 1`
- Ambos pares están envueltos en `<div class="ink-stack">` para aislar el contexto sticky

```html
<div class="ink-stack">
  <section class="sec sec--surface sec--sticky-base">...</section>  <!-- precede, sticky -->
  <section class="sec sec--ink sec--ink-enter">...</section>         <!-- ink, entra encima -->
</div>
```

**Regla de alternancia de superficies:**

El esquema final de la Home es:

```
canvas → surface → ink → surface → canvas → ink → surface → canvas
 Hero   Rub+Mét  Feat  Casos    Proceso   Integ    FAQ     Contact
```

Las secciones ink no participan de la alternancia canvas/surface — son la excepción intencional y documentada.

**Secciones eliminadas respecto al prototipo HTML:**
- ROI Calculator — eliminada por completo
- Why Adhoc — eliminada por completo
- Final CTA violeta — eliminada por completo

**Rubros — implementación (dentro de sección 2):**

Desktop:
- Layout: `grid` 30% / 70%
- Izquierda: sticky (top: nav height), tabs solo texto por rubro
  - `font-family: var(--font-display)`, `font-size: ~30px`
  - Estado activo: `color: var(--color-ink)`, `opacity: 1`
  - Estado inactivo: `color: var(--color-ink)`, `opacity: 0.6`
  - Sin fill de fondo, sin íconos, sin box-shadow
- Derecha: bloques apilados, cada uno con `id` único
- JS: `IntersectionObserver` sobre los bloques → actualiza tab activo
- Click en tab → `scrollIntoView` smooth con offset por el nav

Mobile:
- Sin grid de columnas
- Sin tabs sticky
- Cards de cada rubro apiladas verticalmente, en orden (Educación → Distribución → Servicios → Manufactura)

---

#### Pricing (`src/pages/pricing.astro`)

**Referencia:** `reference/adhoc-pricing.html`

> **Nota:** El Hero y Trust bar del Pricing están desactivados en el HTML de referencia (`display:none`). La página arranca directamente en el Pricing Selector. No implementar el Hero.

Estructura activa (7 secciones):

```
1. Pricing Selector  — tabs Start / Growth ⭐ / Enterprise
2. Comparison Matrix — tabla completa de features
3. ROI section
4. Why Adhoc         — value stacking, qué incluye cada plan
5. Casos por segmento
6. FAQ               — objeciones de precio y proceso
7. Final CTA         — "Agendar diagnóstico sin costo"
```

**Sticky Bottom Bar:**  
Aparece durante el scroll con dos CTAs: "Ver planes" y "Agendar diagnóstico". Implementar como elemento fixed, no parte del flujo de secciones.

**Planes:**
- `Start` — empresas 1–4 usuarios
- `Growth` ⭐ Más elegido — empresas 5–30 usuarios
- `Enterprise` — empresas 30+ usuarios

**Copy de planes:** orientado a outcomes, no a features técnicas.  
✅ "Operación centralizada en una sola plataforma"  
❌ "Multicompañía habilitada"

---

#### Industry Landing Pages (`src/pages/industrias/[vertical].astro`)

**Las cuatro páginas son idénticas en estructura** — solo cambia el contenido. Usar un único template con rutas dinámicas.

Estructura de cada página:

```
1. Hero (específico para el vertical)
2. Video / VSL
3. Cotizador embebido (no modal — versión inline)
4. Integraciones Odoo relevantes para el vertical
5. FAQ específico del vertical
6. CTA final con formulario
```

**Verticales:**
- `manufactura` — foco en producción, lista de materiales, trazabilidad
- `comercializadora` — foco en inventario, ventas B2B, facturación
- `servicios` — foco en proyectos, facturación recurrente, CRM
- `educacion` — foco en matrícula, facturación, comunicaciones

---

## Setup inicial

```bash
# 1. Crear proyecto Astro
npm create astro@latest adhoc-web
cd adhoc-web

# 2. Instalar dependencias (Alpine.js para interactividad)
npm install alpinejs

# Opcional: si se necesita TypeScript estricto, elegir strict en el wizard de Astro

# 3. Copiar assets
# Mover los archivos de la carpeta Fonts/ → public/fonts/
# Mover logos → public/logos/
# Mover íconos Odoo → public/icons/odoo/
# Mover backgrounds → public/images/backgrounds/

# 4. Mover HTMLs de referencia
mkdir reference
# Copiar todos los .html originales a /reference/

# 5. Crear estructura de src/
mkdir -p src/styles src/components src/layouts src/pages/industrias

# 6. Dev server
npm run dev
# → http://localhost:4321
```

---

## Orden de implementación recomendado

Seguir este orden evita rehacer trabajo. Cada paso debe estar en PR separado y revisado antes de continuar.

```
1. tokens.css + typography.css + reset.css
   → Toda la base de design tokens. Sin esto, nada más puede empezar.

2. Base.astro (layout base)
   → Shell HTML, import de estilos globales, slots para content

3. MegaNav.astro
   → Un solo dropdown (Soluciones) + 3 links estáticos + mobile bottom sheet

4. Componentes atómicos: Button, Tag, Card, AppIcon
   → Bloques reutilizables que usan el resto de las páginas

5. Home (index.astro)
   → 11 secciones según estructura actualizada (ver sección Home)

6. Cotizador.astro (modal)
   → Radio cards en todos los pasos, se integra en Base.astro

7. FeatureTabs.astro
   → Vanilla JS, no React

8. Pricing (pricing.astro)
   → Arrancar en Pricing Selector (sin Hero), sticky bottom bar

9. Industry pages ([vertical].astro)
   → Template único, contenido parametrizado por vertical

10. Footer.astro
    → Puede hacerse en paralelo con cualquier paso anterior

11. QA cross-browser + responsive
    → Chrome, Safari, Firefox. Mobile 375px, tablet 768px, desktop 1280px+
```

---

## QA Checklist

Antes de cada PR, verificar:

**Design System**
- [ ] Ningún color hardcodeado — solo tokens CSS (`var(--...)`)
- [ ] Violeta aparece únicamente en `button-primary` (fill) y `button-ghost` (texto)
- [ ] Coral y mostaza no aparecen en ningún elemento de UI
- [ ] No hay `box-shadow` en ningún elemento
- [ ] No hay borders de color (solo `var(--border-subtle)` o `var(--border-medium)`)
- [ ] Botones tienen `border-radius: var(--radius-button)` (12px) — no pill
- [ ] Cards tienen border-radius proporcional (squircle, clamp o equivalente)
- [ ] Tags tienen fill `#EDE9FB`, texto `#BCAFEF`, radius 6px
- [ ] Surface Inversion Rule respetada en todas las secciones

**Tipografía**
- [ ] Headlines H1–H3 en New Kansas
- [ ] Body, labels, botones en Apercu Pro
- [ ] `font-display: swap` en todos los `@font-face`

**Componentes**
- [ ] MegaNav funciona en desktop (hover) y mobile (bottom sheet)
- [ ] Cotizador: 3 pasos, auto-avance en radio cards, Enter/Continuar en inputs
- [ ] Cotizador: cierra con Escape y click fuera del modal
- [ ] CTAs "Solicitar una demo" en todas las páginas triggean el cotizador

**Performance**
- [ ] Imágenes con `loading="lazy"` excepto above-the-fold
- [ ] SVGs de logos e íconos inline o como `<img>` (no background-image CSS)
- [ ] Fonts solo los pesos que se usan en esa página

**Accesibilidad**
- [ ] Todos los `<img>` tienen `alt`
- [ ] Botones y links tienen texto descriptivo (no solo "ver más")
- [ ] Focus visible en todos los elementos interactivos
- [ ] Contraste AA: texto sobre canvas (`#000` sobre `#E9E5DF`) ✅

---

## Copy y tono

Todo el copy del sitio está en **español argentino con voseo**. Si el equipo de dev necesita escribir o modificar copy:

- ✅ "Agendá una demo" / "Conocé más" / "Te acompañamos"
- ❌ "Agenda una demo" / "Conoce más" / "Le acompañamos"
- Tono: cálido, directo, nunca corporativo-robótico
- Sin términos de jerga técnica ERP en el copy de marketing

---

## Assets disponibles

| Asset | Ubicación | Formato |
|---|---|---|
| Logo principal | `public/logos/logo-primary.svg` | SVG (preferido) |
| Logo inverso | `public/logos/logo-inverse.svg` | SVG |
| Isotipo solo | `public/logos/isotipo.svg` | SVG |
| New Kansas (5 pesos) | `public/fonts/NewKansas-*.otf` | OTF |
| Apercu Pro (4 pesos) | `public/fonts/ApercuPro-*.ttf` | TTF |
| Íconos Odoo (24 módulos) | `public/icons/odoo/*.svg` | SVG |
| Backgrounds mesh lavanda | `public/images/backgrounds/mesh-lavender-*.jpg` | JPG |

**Importante sobre los fonts:** son licencias comerciales de Ad Hoc. No subir a CDNs públicos ni incluir en bundles públicos. Servir únicamente desde el dominio de Ad Hoc.

---

## Contacto del proyecto

**Diseño y UX:** Facundo Mantegazza — contacto@uxkid.com  
**Archivos de referencia:** HTML estáticos en `/reference/` del repo  
**Brand Kit completo:** Google Drive > Proyecto ADHOC > "Adhoc Brand Kit — v2 (Tech Premium)"  
**Cualquier duda de diseño:** consultar primero el Brand Kit v2, luego los HTML de referencia, luego al diseñador

> Ante cualquier conflicto entre este README y los archivos HTML de referencia, **los HTML de referencia ganan**. Son la fuente de verdad visual.
