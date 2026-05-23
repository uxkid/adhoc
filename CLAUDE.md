# ADHOC — Instrucciones para Claude Code

## Quién soy y cómo trabajamos
Soy diseñador UX/UI, no desarrollador. Tomé todas las decisiones
de diseño. Tu rol es implementarlas con fidelidad exacta.
Si algo no está claro, preguntame antes de inventar.

---

## Fuentes de verdad (en orden de prioridad)

1. /reference/*.html     → fuente de verdad VISUAL
2. Este CLAUDE.md        → reglas de trabajo
3. README.md             → arquitectura y estructura actualizada

Ante cualquier conflicto entre documentos: los HTML ganan.
Ante cualquier duda de diseño: preguntame a mí.

---

## Stack (no cambiar sin consultarme)

- Framework: Astro (output estático)
- Estilos: CSS custom properties — tokens en src/styles/tokens.css
- JS: Vanilla JS. Alpine.js solo si hay estado reactivo complejo
- Sin Tailwind. Sin React. Sin frameworks CSS externos
- Deploy: Vercel

---

## Reglas absolutas de diseño

Estas reglas no se negocian. Si algo las viola, corregilo
antes de continuar.

COLORES
- Nunca hardcodear colores. Solo var(--)
- Violeta (#7C6CD8): permitido en button-primary, button-ghost y card-violet únicamente.
  Prohibido en cualquier otro elemento de UI.
- Coral (#FF7348): permitido en btn--conversion, tag--cor y card-coral únicamente.
  Prohibido en cualquier otro elemento de UI.
- Mostaza (#FEA912): permitido en tag--mus y card-mustard únicamente.
  Prohibido en cualquier otro elemento de UI.
- Excepción documentada: Final CTA (sección 10 de Home) tiene
  fondo violeta. Es intencional. No corregir.

BORDES Y SOMBRAS
- Sin box-shadow en ningún elemento del sitio
- Borders solo con var(--border-subtle) o var(--border-medium)
- Nunca usar violeta, coral o mostaza como color de border
  (excepción: tag--out-vio usa border con --color-primary — único caso permitido)

BORDER RADIUS
- Botones: var(--radius-button) — 12px fijo. Nunca pill (999px)
- Cards: clamp(16px, 5vw, 32px) — squircle proporcional
- Tags: var(--radius-tag) — 6px fijo

SUPERFICIES
- Las secciones alternan canvas (#E9E5DF) y surface (#FFFFFF)
- Nunca usar el mismo color para fondo de sección y card
  dentro de la misma sección
- Excepción documentada: Final CTA usa violeta como fondo

---

## Reglas absolutas de implementación

ANTES DE CREAR CUALQUIER COMPONENTE
1. Abrí el HTML correspondiente en /reference/
2. Identificá la estructura exacta
3. Reproducila con fidelidad pixel-perfect
4. Si algo no está claro, preguntame

TOKENS
- src/styles/tokens.css es la única fuente de verdad de valores
- Nunca crear variables CSS nuevas sin consultarme
- Nunca usar valores numéricos directos en estilos

ARCHIVOS
- No modificar nada en /reference/ — son solo lectura
- Componentes en /src/components/ con PascalCase
- Páginas en /src/pages/ según la estructura del README

JAVASCRIPT
- Vanilla JS por defecto
- Alpine.js solo si hay estado reactivo que vanilla no puede
  manejar limpiamente — consultame antes
- Feature Tabs: vanilla JS obligatorio (el prototipo usa React,
  eso es deuda técnica, no seguirlo)

---

## Decisiones ya tomadas (no reabrir)

- MegaNav: 1 dropdown (Soluciones) + 3 links estáticos
- Cotizador: radio cards con auto-avance en los 3 pasos
- Feature Tabs: vanilla JS, no React
- Pricing: arranca en Pricing Selector, sin Hero
- Why Adhoc: sección eliminada de Home
- Final CTA: fondo violeta, excepción intencional y documentada
- MegaNav CTA principal: violeta + "Solicitar una demo". El HTML de referencia tenía coral + "Diagnóstico gratuito" — ese era el prototipo. El CLAUDE.md es la decisión final. No revertir a coral.
- Button variante coral: se llama btn--conversion, no secondary.
  Solo para CTAs de marketing de alta conversión (hero, landings,
  final CTA de sección). Nunca en nav, cards, formularios ni UI interna.
- Tag variantes: lav (default), vio, cor, mus, dark, canvas, out-vio.
  out-cor eliminada — el borde coral no cumple WCAG 1.4.11 (2.70:1 < 3:1).
- tag--vio es la única excepción AA del sistema (4.99:1).
  No usar para texto de más de 3 palabras.
- Card.astro = contenedor puro (slot). Variantes: auto, white, canvas,
  violet, lavender, coral, mustard. Sin accent cards (border-top de color).
  Sin box-shadow. Las cards complejas de cada sección son componentes propios.
  card-violet tiene la misma excepción AA que tag--vio (4.99:1).

---

## Orden de implementación

Seguir este orden estrictamente.
No empezar un paso sin terminar el anterior.

1. tokens.css + typography.css + reset.css
2. Base.astro
3. MegaNav.astro
4. Button, Tag, Card, AppIcon
5. Home (index.astro)
6. Cotizador.astro
7. FeatureTabs.astro
8. Pricing (pricing.astro)
9. Industry pages
10. Footer.astro
11. QA

---

## Cómo manejar cambios durante el desarrollo

Si durante una sesión tomamos una decisión que cambia
algo del diseño o la estructura:
1. Implementás el cambio
2. Al final de la sesión actualizás el README para
   reflejar el nuevo estado
3. Me avisás qué actualizaste para que yo lo revise

---

## Cómo pedirme ayuda

Si necesitás contexto visual que no encontrás en los HTML:
"No encuentro referencia de [X] en los archivos. 
¿Me podés describir cómo debería verse?"

Si encontrás un conflicto entre documentos:
"El README dice X pero el HTML muestra Y. 
¿Cuál es correcto para este caso?"

Si una decisión técnica tiene múltiples opciones válidas:
"Para implementar [X] tengo dos opciones: [A] o [B].
¿Cuál preferís?"