# Adhoc — Frontend Handoff README

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
│   │   ├── MegaNav.astro      ← navegación principal (se repite en todas las páginas)
│   │   ├── Cotizador.astro    ← flujo multi-step (modal, trigger desde CTA)
│   │   ├── Footer.astro
│   │   ├── Button.astro       ← componente de botón con variantes
│   │   ├── Tag.astro          ← chip/tag lavanda estilo Notion
│   │   ├── Card.astro         ← card con squircle y surface inversion
│   │   └── AppIcon.astro      ← tile de módulo Odoo (squircle 28px)
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

Estructura de la navegación principal, estilo Notion. Cuatro ítems principales con mega-panel:

```
Soluciones | Industrias | Recursos | Nosotros
```

**Especificaciones de interacción:**
- Desktop: hover sobre ítem → abre panel debajo con animación (opacity + translateY, ~200ms ease-out)
- Mobile: bottom sheet con los mismos ítems, trigger por hamburger
- Panel de Industrias: filtra por vertical (Manufactura, Comercializadora, Servicios, Educación), tamaño de empresa (1–4, 5–30, 30–50, 50+), y caso de uso
- Color del nav: sin background de color. Fondo blanco o canvas según la sección. Sin border-bottom de color — usar `border-bottom: 1px solid var(--border-subtle)` 
- Links activos: ink (`#000000`), weight 500. Sin highlight de color
- CTA en nav: `button-primary` (violeta, 12px radius)

**Importante:** el MegaNav es un componente Astro que se importa en `Base.astro` y aparece en todas las páginas. No duplicar.

---

### Cotizador (Customer Journey)

**Archivo:** `src/components/Cotizador.astro`  
**Referencia:** `reference/adhoc-cotizador.html`  
**Trigger:** click en el CTA principal "Solicitar una demo" (en nav y en cualquier sección de la página)

El cotizador es un **modal/overlay multi-step** estilo Typeform. No es una página separada.

**Flujo de 3 pasos (uno por pantalla):**

```
Paso 1: ¿En qué rubro opera tu empresa?
  → Radio cards con auto-avance al seleccionar
  → Opciones: Manufactura / Comercializadora / Servicios / Educación

Paso 2: ¿Qué herramienta usás hoy para gestionar tu empresa?
  → Radio cards con auto-avance al seleccionar
  → Opciones: Excel / Sistema actual (ERP) / Varios sistemas desconectados / Nada formal

Paso 3: ¿Cuántos usuarios necesitarían acceso?
  → Dropdown o selector numérico
  → Avance con botón "Continuar" o tecla Enter

Resultado: Plan recomendado + dos CTAs:
  → "Agendar llamada" (abre Calendly o similar)
  → "Hablar con un asesor" (WhatsApp o formulario)
```

**Reglas de interacción:**
- Radio cards → auto-avanzan al seleccionar (sin botón "Continuar")
- Dropdown/text inputs → requieren "Continuar" o Enter para avanzar
- Progress indicator sutil en la parte superior (no número de paso, barra de progreso thin)
- Escape o click fuera → cierra el modal
- El modal no recarga la página — es JS puro en el cliente
- Back button dentro del modal para volver al paso anterior

**Diseño del modal:**
- Background: overlay `rgba(0,0,0,0.4)` sobre la página
- Card del modal: fondo blanco, `border-radius: clamp(20px, 3vw, 32px)`, sin shadow, border `1px solid var(--border-subtle)`
- Ancho máximo: 560px, centrado vertical y horizontal
- Padding interno: 40px desktop, 24px mobile

---

### Páginas

#### Home (`src/pages/index.astro`)

**Referencia:** `reference/adhoc-homepage.html`

Estructura de secciones en orden:

```
1. Hero
2. Logos de clientes (proof strip)
3. Pain section ("¿Te pasa esto?")
4. Industry selector (Wispr Flow-style: fondo oscuro, pill tabs + copy panels)
5. Feature carousel (Headspace-style: 6 tabs con color, visual Odoo, copy)
6. Why Adhoc (4 cards: Partner #1, +600 desarrollos, especialización, soporte)
7. ROI section
8. Casos de éxito (mini case studies)
9. FAQ (accordion)
10. Final CTA
```

**Regla de alternancia de superficies:**
Las secciones alternan entre fondo canvas y fondo blanco. La primera sección (Hero) define el punto de partida — generalmente canvas beige. Cada sección siguiente invierte. No romper esta alternancia sin motivo.

**Industry Selector (sección 4):**
- Fondo oscuro (`#1A1A1A` o similar), no beige
- Pill tabs para cada vertical: Manufactura / Comercializadora / Servicios / Educación
- Al seleccionar un tab, el copy panel a la derecha cambia con animación suave (fade o slide)
- Referencia visual: Wispr Flow homepage

**Feature Carousel (sección 5):**
- 6 tabs, cada uno con un color de acento (usar variantes de la paleta), un visual de UI Odoo, y copy de beneficio
- Referencia visual: Headspace feature tabs

---

#### Pricing (`src/pages/pricing.astro`)

**Referencia:** `reference/adhoc-pricing.html`

Estructura:

```
1. Hero (value-first, no arranca con precios)
2. Trust bar (logos + Partner #1)
3. Selector de plan (Start / Growth / Enterprise) — tabs, no tabla
4. Split layout: izquierda value stack, derecha precio + CTA
5. Comparison matrix (tabla completa de features)
6. ROI section
7. Why Adhoc (qué está incluido en todos los planes)
8. Mini casos por segmento
9. FAQ (accordion — objeciones de precio y proceso)
10. Final CTA ("Agendar diagnóstico sin costo")
```

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
   → Componente completo con mega-panel y mobile bottom sheet

4. Componentes atómicos: Button, Tag, Card, AppIcon
   → Bloques reutilizables que usan el resto de las páginas

5. Home (index.astro)
   → La página más compleja, con industry selector y feature carousel

6. Cotizador.astro (modal)
   → Flujo multi-step, se integra en Base.astro y se activa desde cualquier CTA

7. Pricing (pricing.astro)
   → Selector de plan, comparison matrix, FAQ

8. Industry pages ([vertical].astro)
   → Template único, contenido parametrizado por vertical

9. Footer.astro
   → Puede hacerse en paralelo con cualquier paso anterior

10. QA cross-browser + responsive
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
