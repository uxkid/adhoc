# Adhoc Brand Kit

Kit de assets de marca de Adhoc, listo para usar con cualquier IA
que genere contenido (interfaces, placas, presentaciones, copy).

## Qué hay acá

```
adhoc-brand-kit/
├── DESIGN.md                       # Spec del sistema — el archivo principal
├── adhoc-brandbook.pdf             # Brandbook oficial (fuente de verdad)
├── README.md                       # Este archivo
│
├── assets/
│   ├── logo/                       # Logos en SVG + PNG (transparentes)
│   │   ├── logo-primary.svg        # Wordmark negro + isotipo lavanda
│   │   ├── logo-primary.png        # (fallback raster)
│   │   ├── logo-inverse.svg        # Wordmark crema + isotipo lavanda
│   │   ├── logo-inverse.png
│   │   ├── isotipo.svg             # Solo la "A" en círculo
│   │   └── isotipo.png
│   │
│   ├── fonts/                      # Tipografías oficiales
│   │   ├── NewKansas-*.otf         # Serif display — titulares
│   │   └── ApercuPro-*.ttf         # Sans humanista — body, UI
│   │
│   ├── backgrounds/
│   │   └── mesh-lavender-1..4.jpg  # Gradientes mesh lavanda
│   │
│   ├── icons/
│   │   └── odoo/                   # 24 íconos de módulos Odoo (SVG + PNG)
│   │
│   └── illustrations/              # Referencias de estilo ilustración
│       ├── brandbook-illustrations-grid.jpg
│       └── brandbook-colors-reference.jpg
│
└── examples/                       # Piezas reales como ground truth
    ├── 01-social-stickers-academy-workshop.png
    ├── 02-website-empresas-confian-partner1.png
    ├── 03-social-post-que-hacemos.png
    ├── 04-social-story-caso-de-exito.png
    ├── 05-social-story-presupuestos-empresas-servicios.png
    ├── 06-brandbook-ejemplo-web-hero.jpg
    ├── 07-brandbook-ejemplos-placas.jpg
    └── 08-brandbook-ejemplo-pantone-lavanda.jpg
```

## Cómo usar el kit con distintas IAs

El `DESIGN.md` es machine-readable (YAML front matter + markdown) y
sigue la spec oficial de Google Stitch. Cada IA lo puede leer como
contexto para generar outputs coherentes con la marca.

### Claude / ChatGPT / Gemini (chat web)

1. Subí el `DESIGN.md` junto con los archivos que la IA vaya a
   necesitar para la tarea. Ejemplos:
   - Para una landing: `DESIGN.md` + `assets/logo/logo-primary.svg`
     + 2-3 archivos de `examples/`.
   - Para una placa de redes: `DESIGN.md` + la placa de `examples/`
     del formato que querés replicar.
2. Pedí lo que quieras, mencionando "seguí el DESIGN.md adjunto".

### Claude con conector de Google Drive

1. Subí toda la carpeta `adhoc-brand-kit/` a Drive.
2. Compartila como "cualquiera con el link puede ver" (o con tu
   cuenta si el conector tiene permisos de tu workspace).
3. Pedile a Claude que busque el kit: "buscá la carpeta
   adhoc-brand-kit en mi Drive y usá el DESIGN.md que está ahí".

### Claude Code / Cursor / Copilot (agentes de código)

1. Copiá esta carpeta completa a la raíz del proyecto (o a
   `.brand/` o `docs/brand/`).
2. El agente detecta el `DESIGN.md` automáticamente y usa los
   assets relativos a él.
3. En `CLAUDE.md` / `.cursorrules` / `.github/copilot-instructions.md`
   agregá una línea: "For brand design decisions, read
   `./DESIGN.md` and the assets referenced within."

### v0 / Lovable / Bolt (AI builders)

1. Abrí `DESIGN.md` y copiá su contenido completo al prompt inicial.
2. Subí los archivos de `assets/logo/` al builder cuando te pida
   logos.
3. Si el builder acepta ejemplos visuales, subí 1-2 piezas de
   `examples/` para anclar el estilo.

## Qué hacer cuando cambie la marca

1. Actualizá el `adhoc-brandbook.pdf` con la versión nueva.
2. Regenerá los SVGs de logo si cambiaron.
3. Editá el `DESIGN.md` — tokens arriba, prosa abajo.
4. Validá con el linter oficial:
   ```bash
   npx @google/design.md lint DESIGN.md
   ```

## Export a otros formatos

El CLI de Stitch exporta tokens a formatos consumibles por
frameworks:

```bash
npx @google/design.md export --format tailwind DESIGN.md > tailwind.theme.json
npx @google/design.md export --format css DESIGN.md > tokens.css
npx @google/design.md export --format json DESIGN.md > tokens.json
```

## Licencia y fuentes

Las tipografías incluidas (**New Kansas** y **Apercu Pro**) son
fuentes licenciadas. El uso de este kit está limitado al equipo de
Adhoc y a proveedores trabajando en piezas para Adhoc. No
redistribuir los archivos de fuentes fuera de ese contexto.

Los íconos de módulos Odoo son propiedad de Odoo S.A., incluidos
acá con fines de uso interno de Adhoc como partner oficial.
