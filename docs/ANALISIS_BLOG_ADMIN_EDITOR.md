# ANÁLISIS EXHAUSTIVO: Discrepancia Preview vs Vista Real (blog-post.html vs admin-editor.html)

**Fecha:** 2026-08-11  
**Autor:** Análisis conjunto (Claude + agente auxiliar)  
**Archivos analizados:** `public/admin-editor.html` (1.348 líneas), `public/blog-post.html` (1.308 líneas)  
**Estado:** **DIAGNOSTICADO — ACCIÓN REQUERIDA**

---

## RESUMEN EJECUTIVO

Existen **dos sistemas de renderizado completamente independientes** que no comparten código:

| Sistema | Archivo | Función principal | Líneas clave |
|---------|---------|-------------------|--------------|
| **Preview Modal** | `admin-editor.html` | Simula vista previa en modal | `openPreview()` líneas 1169-1206 |
| **Vista Real** | `blog-post.html` | Renderiza artículo publicado | `renderPost()` líneas 1094-1154 |

**Resultado:** Lo que la clienta ve en "Vista previa" **NO coincide** con lo que se publica en `blog-post.html`. Diferencias en colores, tipografía, layout, clases Quill, lógica de plantillas y bugs funcionales.

---

## DISCREPANCIAS CRÍTICAS (Rompen funcionalidad/UX)

### 🔴 1. Bug: Publicación accidental al guardar borrador
**Archivo:** `admin-editor.html:1123`  
**Código actual:**
```javascript
const publicado = publish || postPublished.checked;
```
**Problema:** Si checkbox "Publicar inmediatamente" está marcado (`true`) y la clienta clicka "Guardar borrador" (`publish = false`), evalúa `false || true = true` → **publica sin querer**.  
**Fix:** `const publicado = publish ? true : postPublished.checked;`

---

### 🔴 2. Alineaciones Quill no funcionan en blog publicado
**Archivo:** `admin-editor.html:13` carga `quill.snow.css` → incluye `.ql-align-center`, `.ql-align-right`, `.ql-align-justify`, `.ql-indent-*`  
**Archivo:** `blog-post.html` **NO carga** `quill.snow.css`  
**Resultado:** Texto centrado/justificado/indentado en editor → **aparece alineado a la izquierda** en blog publicado.  
**Fix:** Añadir `<link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">` al `<head>` de `blog-post.html`

---

### 🔴 3. Descripción corta desaparece con plantilla "imagen-destacada"
**Archivo:** `blog-post.html:1134` → `articleHeader.style.display = 'none'` oculta TODO el header (incluye `.article-description`)  
**Overlay reconstruido en JS** (líneas 1118-1132) **NO incluye la descripción**  
**Resultado:** Plantilla "imagen-destacada" pierde el excerpt/descripción corta completamente.  
**Fix:** Mover descripción al overlay ANTES de ocultar header, o renderizarla dentro del overlay.

---

### 🔴 4. Plantilla "galería" es placebo en AMBOS lados
**Editor:** Opción existe en radio group (líneas 728-737), se guarda en Firestore como `plantilla: 'galeria'`  
**blog-post.html:** En `renderPost()` (línea 1117) solo ramifica para `imagen-destacada`; `galeria` cae en `else` → **comportamiento idéntico a "estándar"**  
**Resultado:** Clientas elige "Galería + texto" → ve preview estándar → se publica estándar. **No existe layout de galería real.**

---

## DISCREPANCIAS ALTAS (Engañan al redactor)

### 🟠 5. Color del título: Preview celeste vs Real gris oscuro
| Preview (`admin-editor.html` CSS `.preview-content h1`) | Real (`blog-post.html` CSS `.article-title`) |
|--------------------------------------------------------|---------------------------------------------|
| `color: var(--title-color)` → **#6FC1FF (celeste)** | `color: var(--text-dark)` → **#3A4A5A (gris)** |

### 🟠 6. Color de H2: Preview gris vs Real celeste (contradicción)
| Preview (`#editorContainer .ql-editor h2`) | Real (`.article-content h2`) |
|--------------------------------------------|------------------------------|
| `color: var(--text-dark)` → **gris** | `color: var(--title-color)` → **celeste** |

**Ambos son contradictorios:** El preview muestra título celeste + H2 gris; el real muestra título gris + H2 celeste. **El redactor nunca ve la verdad.**

---

### 🟠 7. Badge categoría: Diferente estilo visual
| Preview (`.preview-badge`) | Real (`.article-category`) |
|----------------------------|----------------------------|
| `bg: rgba(111,193,255,0.15)`, `color: celeste-deep`, `rounded-full`, `text-transform: uppercase`, `letter-spacing: 0.08em`, `font-weight: 700`, `font-size: 12px` | `bg: cream-light`, `color: text-dark`, `rounded-20px`, `font-weight: 600`, `font-family: League Spartan`, `font-size: 13px` |

---

### 🟠 8. Plantilla "imagen-destacada": Overlay gradient distinto
| Preview (`.preview-hero-overlay`) | Real (`.article-featured-overlay`) |
|-----------------------------------|-----------------------------------|
| `linear-gradient(180deg, rgba(26,46,53,0.0) 30%, rgba(26,46,53,0.88) 100%)` | `linear-gradient(180deg, transparent 0%, rgba(26,46,53,0.8) 100%)` |
| **Más oscuro, empieza fade a 30%** | **Más claro, empieza fade a 0%** |

---

### 🟠 9. Imagen portada: Aspect ratio vs Max-height
| Preview (`.preview-cover`) | Real (`.article-cover`) |
|----------------------------|-------------------------|
| `aspect-ratio: 16/9`, `border-radius: 20px`, fijo | `max-height: 500px`, `border-radius: 20px`, variable |

---

## DISCREPANCIAS MEDIAS/BAJAS (CSSspacing, sombras, tipografía contenido)

| Elemento | Preview (`admin-editor.html` modal CSS) | Real (`blog-post.html` `.article-content`) |
|----------|------------------------------------------|---------------------------------------------|
| **Line-height base** | 1.9 | 1.85 |
| **Font-size base** | Hereda Quill (15px) | 17px explícito |
| **H3** | 1.25rem, `text-dark` | 1.35rem, `text-dark` |
| **Blockquote** | `border-left-color: celeste-deep`, `bg: cream-light`, `padding: 16px 20px`, `radius: 0 12px 12px 0` | `border-left: 4px solid celeste-deep`, `padding: 16px 24px`, `radius: 0 12px 12px 0`, `italic`, `font-size: 1.05rem` |
| **Imágenes inline** | `margin: 18px 0` | `margin: 24px auto`, `max-width: 100%` |
| **Listas (ul/ol)** | `padding-left: 24px` | `padding-left: 28px` |
| **Código inline** | No definido | `bg: cream-light`, `padding: 2px 6px`, `radius: 4px` |
| **Pre/Code blocks** | No definido | `bg: text-dark`, `color: cream`, `radius: 12px` |
| **HR** | No definido | `border-top: 2px solid card-border` |

---

## CAUSA RAÍZ: ARQUITECTURA DUPLICADA

```
admin-editor.html (Preview)
├── Función openPreview() [líneas 1169-1206]
│   ├── Genera HTML string manualmente (template literals)
│   ├── Usa clases CSS propias del modal (.preview-*)
│   └── Inserta en #previewContent.innerHTML
│
└── CSS del modal [líneas 231-256]
    ├── .preview-content, .preview-hero, .preview-badge, .preview-cover, etc.
    └── Estilos SCOPE al modal (no reutilizables)

blog-post.html (Real)
├── Función renderPost() [líneas 1094-1154]
│   ├── Manipula DOM directamente (.article-*)
│   ├── Lógica condicional: if (plantilla === 'imagen-destacada') else
│   └── Inserta en #articleContent.innerHTML
│
└── CSS del artículo [líneas 290-328]
    ├── .article-content, .article-cover, .article-category, .article-title, etc.
    └── Estilos GLOBALES de la página
```

**No hay código compartido.** Cada archivo reinventa el renderizado por completo.

---

## DATOS GUARDADOS EN FIRESTORE (editor → blog-post)

Campos que guarda `savePost()` en `admin-editor.html:1129-1138`:
```javascript
{
  titulo: string,
  descripcionCorta: string | null,
  categoria: 'ansiedad'|'depresion'|'pareja'|'familiar'|'autoestima'|'otros',
  plantilla: 'estandar' | 'imagen-destacada' | 'galeria',
  contenidoHtml: string,  // HTML crudo de Quill (incluye .ql-align-* classes)
  imagenPortadaUrl: string | null,
  publicado: boolean,
  fecha: serverTimestamp()
}
```

**blog-post.html lee `plantilla`** pero **solo ramifica para `imagen-destacada`**. `estandar` y `galeria` caen en mismo `else`.

---

## QUÉ SUCEDE HOY SEGÚN PLANTILLA ELEGIDA

| Plantilla | En Preview se ve | En blog-post se ve |
|-----------|------------------|---------------------|
| **Estándar** | Título celeste, imagen 16:9 fija, badge celeste translúcido, H2 gris | Título gris, imagen hasta 500px, badge crema sólido, H2 celeste |
| **Imagen destacada** | Overlay oscuro 30%→88%, badge celeste, título blanco grande, **SIN descripción** | Overlay claro 0%→80%, badge crema, título blanco mayor, **SIN descripción** |
| **Galería** | Igual que Estándar (fallback) | Igual que Estándar (fallback) |

---

## SOLUCIONES EVALUADAS

| Opción | Descripción | Arregla bugs críticos (#1-3) | Arregla discrepancias visuales | Arregla plantilla galería | Mantenibilidad |
|--------|-------------|------------------------------|-------------------------------|---------------------------|----------------|
| **A: Módulo compartido (RECOMENDADA)** | `public/src/js/blog-renderer.js` exporta `renderArticle(data, container, mode)` usado por AMBOS archivos | ✅ (lógica centralizada) | ✅ (CSS único) | ✅ (una implementación) | ✅ Excelente |
| **B: Iframe preview** | Preview abre `blog-post.html?id=TEMP&preview=1` en iframe | ✅ | ✅ | ✅ | ✅ Buena (pero requiere endpoint temporal) |
| **C: Parche CSS + unificar clases** | Copiar `.article-*` styles al modal, cambiar `openPreview()` a usar mismas clases | ❌ (no arregla #1 lógica JS, #2 Quill CSS falta, #3 lógica DOM) | Parcial | ❌ | ❌ Deuda técnica |
| **D: Documentar y dejar** | "Preview es aproximado; vista final en blog-post.html" | ❌ | ❌ | ❌ | ❌ Confunde a clienta |

---

## RECOMENDACIÓN FINAL: **OPCIÓN A (Módulo Compartido)**

### Archivo nuevo: `public/src/js/blog-renderer.js`
```javascript
// Módulo ESM compartido
export function renderArticle(data, container, options = {}) {
  // options.mode: 'preview' | 'full'
  // options.isPreview: boolean (para ajustes menores: sin CTA, sin related, etc.)
  
  // UNA sola implementación para:
  // - Plantillas: estandar | imagen-destacada | galeria (REAL)
  // - Quill classes support (.ql-align-*, .ql-indent-*, etc.)
  // - CSS consistente usando design tokens (--celeste-deep, --text-dark, etc.)
  // - Descripción, badge, meta, contenido, tags
  // - Accesibilidad (ARIA, semántica)
}

// Helpers internos
function buildHero(data, options) { ... }
function buildStandardHeader(data, options) { ... }
function buildContent(data, options) { ... }
function applyQuillStyles(container) { ... }  // Asegura .ql-align-* funcionen
```

### Integración:
- **admin-editor.html:** `import { renderArticle } from './src/js/blog-renderer.js';` → `renderArticle(data, previewContent, { mode: 'preview' })`
- **blog-post.html:** `import { renderArticle } from './src/js/blog-renderer.js';` → `renderArticle(data, articleMain, { mode: 'full' })`

---

## PLAN DE IMPLEMENTACIÓN DETALLADO

### FASE 0: Hotfixes Inmediatos (15 min) — **HACER HOY**
- [ ] **HF-1** Fix bug publicación accidental: `admin-editor.html:1123` → `const publicado = publish ? true : postPublished.checked;`
- [ ] **HF-2** Añadir Quill CSS a blog-post: `<link href="https://cdn.quilljs.com/1.3.7/quill.snow.css" rel="stylesheet">` en `<head>`
- [ ] **HF-3** Fix descripción en imagen-destacada: mover `.article-description` al overlay ANTES de `articleHeader.style.display = 'none'` o renderizarla en overlay

### FASE 1: Crear Módulo Compartido `blog-renderer.js` (2-3h)
- [ ] **M-1** Crear `public/src/js/blog-renderer.js` con:
  - [ ] `renderArticle(data, container, options)` — función principal
  - [ ] `buildHero()` — para plantilla `imagen-destacada`
  - [ ] `buildStandardHeader()` — para `estandar` y `galeria`
  - [ ] `buildGalleryLayout()` — **NUEVO**: layout real para plantilla `galeria` (texto + 2-3 imágenes intercaladas)
  - [ ] `buildContent()` — renderiza `contenidoHtml` con estilos Quill normalizados
  - [ ] `applyQuillStyles(container)` — inyecta estilos `.ql-align-*`, `.ql-indent-*` si no existen
  - [ ] `buildMeta()` — badge, autor, fecha, categoría
  - [ ] `buildTags()` — categoria tag
  - [ ] Helpers: `escapeHtml()`, `stripHtml()`, `formatDate()`, `categoryLabels`
- [ ] **M-2** CSS interno del módulo (o referenciar CSS global) usando design tokens oficiales

### FASE 2: Integrar en admin-editor.html (30 min)
- [ ] **I-1** Añadir `import { renderArticle } from './src/js/blog-renderer.js';`
- [ ] **I-2** Reemplazar `openPreview()` (líneas 1169-1206) por llamada a `renderArticle(data, previewContent, { mode: 'preview' })`
- [ ] **I-3** Eliminar CSS del modal `.preview-*` (líneas 231-256) ahora innecesario
- [ ] **I-4** Verificar: preview muestra exactamente lo que renderizará blog-post

### FASE 3: Integrar en blog-post.html (30 min)
- [ ] **I-5** Añadir `import { renderArticle } from './src/js/blog-renderer.js';`
- [ ] **I-6** Reemplazar `renderPost()` (líneas 1094-1154) por `renderArticle(data, articleMain, { mode: 'full' })`
- [ ] **I-7** Mantener lógica de `loadRelatedPosts()`, meta tags SEO, reading progress, navbar — son propios de página completa
- [ ] **I-8** Eliminar CSS `.article-*` duplicado (líneas 290-328) ahora manejado por módulo

### FASE 4: Implementar Plantilla Galería Real (30 min)
- [ ] **G-1** En `blog-renderer.js`: `buildGalleryLayout(data, options)` que:
  - Renderiza contenido HTML
  - Inserta imágenes intercaladas cada ~300-400 palabras (o usar markers `<!-- gallery-img-1 -->` en contenido)
  - Grid 2 columnas en desktop, 1 en mobile
  - Captions opcionales
- [ ] **G-2** Actualizar `radio-group` en `admin-editor.html` para que `galeria` tenga descripción precisa

### FASE 5: Testing & Verificación (45 min)
- [ ] **T-1** Crear post prueba con cada plantilla (estandar, imagen-destacada, galeria)
- [ ] **T-2** Verificar preview === publicado pixel-perfect
- [ ] **T-3** Verificar Quill alignments: centrado, derecha, justificado, indent
- [ ] **T-4** Verificar descripción aparece en TODAS las plantillas
- [ ] **T-5** Verificar botón "Guardar borrador" NO publica si checkbox marcado
- [ ] **T-6** Verificar responsive mobile/tablet/desktop
- [ ] **T-7** Lighthouse: Performance ≥90, Accessibility ≥90, SEO ≥90

### FASE 6: Actualizar Documentación (15 min)
- [ ] **D-1** Actualizar `TAREAS_PENDIENTES_FINAL.md` → agregar Grupo 9 (Blog/Editor Unificación)
- [ ] **D-2** Actualizar `INVENTARIO_CAMBIOS.md` → items E-1 a E-7
- [ ] **D-3** Actualizar `PLAN_TAREAS.md` → Grupo 9
- [ ] **D-4** Commit + Push con mensaje convencional

---

## ARCHIVOS A MODIFICAR

| Archivo | Tipo de cambio | Líneas aproximadas |
|---------|----------------|-------------------|
| `public/admin-editor.html` | **Hotfix** (1123), **Import + refactor** openPreview, **Eliminar CSS** .preview-* | 1123, 838+, 1169-1206, 231-256 |
| `public/blog-post.html` | **Hotfix** (head + 1134), **Import + refactor** renderPost, **Eliminar CSS** .article-* | head, 1117-1134, 1094-1154, 290-328 |
| `public/src/js/blog-renderer.js` | **NUEVO** — módulo compartido completo | ~300-400 líneas nuevas |

---

## VERIFICACIONES POST-IMPLEMENTACIÓN

```bash
# 1. Verificar que NO quedan referencias a clases .preview-* en admin-editor.html
grep -n "preview-" public/admin-editor.html

# 2. Verificar que NO quedan .article-* styles en blog-post.html (excepto los que use el módulo)
grep -n "article-" public/blog-post.html | head -30

# 3. Verificar import del módulo en ambos archivos
grep -n "blog-renderer" public/admin-editor.html public/blog-post.html

# 4. Verificar Quill CSS en blog-post.html
grep -n "quill.snow.css" public/blog-post.html

# 5. Verificar fix bug publicación
grep -n "publicado = " public/admin-editor.html

# 6. Checklist transversal (siempre)
grep -i "TCC" public/index.html
grep -i "S/" public/index.html
grep -i "San Isidro\|Surco" public/index.html
grep -c "wa.me/51939855573" public/index.html
grep -c "DESHABILITADO v1" public/index.html
```

---

## NOTAS PARA DESARROLLO FUTURO (v2+)

1. **Extensibilidad:** `renderArticle()` acepta `options` para variantes (preview sin CTA, full con related posts, AMP, email template, etc.)
2. **Testing visual:** Considerar Chromatic/Percy para regression testing visual automático
3. **Plantillas configurables:** Mover definiciones de plantillas a JSON config para añadir nuevas sin tocar código
4. **Editor visual de plantillas:** Permitir a clienta crear layouts custom (drag-drop) → guarda config JSON → renderer lo interpreta

---

## HISTORIAL DE CAMBIOS

| Fecha | Autor | Cambio |
|-------|-------|--------|
| 2026-08-11 | Análisis conjunto | Diagnóstico completo, 9 discrepancias identificadas, 3 bugs críticos, 4 opciones evaluadas, plan detallado Opción A |

---

**Próximo paso:** Ejecutar **FASE 0 (Hotfixes)** → **FASE 1-4 (Módulo + Integración + Galería)** → **FASE 5 (Testing)** → **FASE 6 (Docs)**

¿Procedemos con FASE 0 ahora?