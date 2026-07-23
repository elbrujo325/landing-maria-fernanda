# TAREAS PENDIENTES — Landing "Pensar Sentir Hacer" (Versión Final)

**Fecha:** 2026-07-23  
**Fuente:** Brief final del cliente + revisión del estado actual  
**Archivo objetivo:** `index.html` (single-file, CSS interno)  
**Estado actual:** Paleta oficial aplicada, copy corregido,Firebase/Backend pendiente, optimizaciones de imagen listas

---

## RESUMEN EJECUTIVO DE CAMBIOS REQUERIDOS

El cliente solicita un **cambio radical de paleta y estética**:
- **ELIMINAR** `--ink` (`#1A2E35`) completamente — ningún elemento usa azul oscuro
- **NUEVA** `--text-dark: #3A4A5A` (gris con matiz celeste) para párrafos/texto
- **NUEVA** `--title-color: #6FC1FF` (`--celeste-deep`) para títulos y elementos destacados
- **SOMBRAS** solo tonos celestes/amarillos suaves (ej: `rgba(111, 193, 255, 0.25)`)
- **ONDAS ANIMADAS** dinámicas en Hero (y opcional en secciones clave)
- **BOTONES** redefinidos: primario celeste/blanco, secundario outline celeste
- **IMÁGENES** usar versiones `-optimized` ya en repo

---

## PLAN DE EJECUCIÓN (Orden secuencial)

### FASE 1 — PALETA Y VARIABLES CSS (Crítico, base de todo)

| T# | Descripción | Verificación |
|---|---|---|
| 1.1 | En `:root`: Borrar `--ink: #1A2E35;`, `--muted: #7A9A8A;`, `--accent-cool`, `--card-bg`, `--card-border` | `grep "ink\|muted\|accent-cool\|card-bg\|card-border" index.html` → 0 (salvo comentarios) |
| 1.2 | Añadir/Actualizar variables: `--text-dark: #3A4A5A;`, `--title-color: #6FC1FF;`, `--white: #FFFFFF;`, `--celeste-deep: #6FC1FF;`, `--celeste-mid: #89CCFF;`, `--celeste-light: #B0DDFC;`, `--yellow-deep: #FFFB85;`, `--yellow-mid: #FEFFAF;`, `--yellow-light: #FDFDC9;`, `--cream: #FFFEEC;`, `--cream-light: #FFFDF4;` | `:root` block completo y limpio |
| 1.3 | `body`: `color: var(--text-dark);` `background: var(--cream);` | Visual: texto gris-celeste, fondo crema |
| 1.4 | `h1,h2,h3,h4`: `color: var(--title-color);` `font-family: 'League Spartan';` | Todos los títulos celeste |
| 1.5 | Enlaces/texto destacado: `color: var(--celeste-mid);` o `--celeste-deep` | Consistente |

---

### FASE 2 — LIMPIEZA DE USOS DE --ink (Recorrido exhaustivo)

| T# | Zona | Acción | Verificación |
|---|---|---|---|
| 2.1 | Navbar (`.navbar`, `.nav-logo`, textos, bordes, sombras) | Reemplazar `--ink` → `--text-dark`, `--celeste-deep`, `--white`; sombras → `rgba(111,193,255,0.XX)` | Nav glassmorphism con colores claros |
| 2.2 | Hero (`h1`, `p`, botones, trust bar, photo frame) | Títulos `--title-color`, textos `--text-dark`, botones ver Fase 4 | Hero limpio |
| 2.3 | Social Proof Bar | Textos `--text-dark`, stats `--title-color` | Ok |
| 2.4 | Sobre Mí (textos, video wrapper, stats) | Textos `--text-dark`, títulos `--title-color` | Ok |
| 2.5 | Credenciales (cards, iconos, años, textos) | Iconos `--celeste-deep`, textos `--text-dark`, años `--title-color` | Ok |
| 2.6 | Problema/Solución (cards, iconos) | Fondos `--cream-light`, bordes `--celeste-light`, textos `--text-dark` | Ok |
| 2.7 | Servicios (accordion, headers, contenido, fotos) | Headers `--title-color`, body `--text-dark`, bordes `--celeste-light` | Ok |
| 2.8 | Misión (quote, cards) | Quote `--title-color`, cards `--text-dark` | Ok |
| 2.9 | Testimonios (cards, avatars, stars, indicators) | Cards `--text-dark`, avatars ring `--celeste-light`, stars `--yellow-deep`, dots `--celeste-deep` | Ok |
| 2.10 | Redes & Agenda (chips, embed, CTA) | Chips base `--ink`→`--text-dark`, hover brand colors, CTA ver Fase 4 | Ok |
| 2.11 | FAQ (accordion, preguntas, respuestas) | Preguntas `--title-color`, respuestas `--text-dark`, iconos `--celeste-deep` | Ok |
| 2.12 | CTA Final (títulos, textos, botones) | Título `--title-color`, texto `--text-dark`, botones ver Fase 4 | Ok |
| 2.13 | Footer (quote, brand, nav, contact, social, bottom bar) | Quote `--title-color`, textos `--text-dark`/`--cream`, social base `--text-dark`, hover brand | Ok |
| 2.14 | WhatsApp Float | Fondo `--text-dark`, icono `--white`, shadow `rgba(111,193,255,0.4)` | Ok |
| 2.15 | Responsive / Media queries | Mismos reemplazos en bloques `@media` | Ok |
| 2.16 | Sombras GLOBALES | Buscar `rgba(26,46,53` o `rgba(1,1,1` o `rgba(0,0,0` → reemplazar por `rgba(111,193,255,0.25)` o `rgba(255,251,133,0.2)` | `grep -n "rgba(" index.html` → solo tonos celeste/amarillo |

---

### FASE 3 — ONDAS DINÁMICAS (Hero + secciones opcionales)

| T# | Descripción | Verificación |
|---|---|---|
| 3.1 | En `:root` añadir: `--wave1: var(--yellow-light); --wave2: var(--celeste-light);` | Variables presentes |
| 3.2 | Añadir CSS completo `.wave-background`, `.wave`, `@keyframes waveMove` (ver brief) | CSS en `<style>` |
| 3.3 | En Hero: añadir `style="position: relative; overflow: hidden; background: var(--cream);"` y `<div class="wave-background"><div class="wave"></div><div class="wave"></div></div>` como primer hijo | HTML correcto |
| 3.4 | Contenido Hero: `position: relative; z-index: 2;` en `.hero .container` o wrapper | Contenido sobre ondas |
| 3.5 | (Opcional) Repetir en `#sobre-mi`, `#servicios`, `#testimonios` con versiones sutiles (`opacity: 0.15`, `animation-duration: 30s+`) | Visual: movimiento orgánico |

---

### FASE 4 — BOTONES (Sistema unificado)

| T# | Clase | Estilos | Verificación |
|---|---|---|---|
| 4.1 | `.btn-primary` | `background: var(--celeste-deep); color: var(--white); border: none; box-shadow: 0 8px 20px -5px rgba(111,193,255,0.3);` | Visual: celeste sólido, sin sombra verde |
| 4.2 | `.btn-primary:hover` | `background: var(--celeste-mid); transform: scale(1.03); box-shadow: 0 12px 28px -5px rgba(111,193,255,0.4);` | Hover celeste medio |
| 4.3 | `.btn-secondary` | `background: transparent; color: var(--celeste-deep); border: 2px solid var(--celeste-deep); box-shadow: none;` | Outline celeste |
| 4.3b | `.btn-secondary:hover` | `background: var(--celeste-deep); color: var(--white);` | Fill on hover |
| 4.4 | `.btn-ghost` (si existe) | `background: transparent; color: var(--text-dark); border: 1px solid var(--celeste-light);` | Muted |
| 4.5 | **Aplicar clases** a TODOS los botones: Nav "Agendar", Hero CTA, Servicios accordion CTAs, CTA Final (2 botones), Redes CTA, Mobile Sticky CTA | `grep 'class="btn' index.html` → solo `btn-primary`/`btn-secondary` |

---

### FASE 5 — IMÁGENES (Rutas correctas)

| T# | Elemento | Nueva ruta (`src`) | Verificación |
|---|---|---|---|
| 5.1 | Hero photo / Sobre mí | `foto-fernanda.png` | Ya correcta |
| 5.2 | Navbar logo | `logo-psh.png` | Verificar `nav-logo-img` |
| 5.3 | Footer logo | `logo-psh.png` | Verificar `footer-logo` |
| 5.4 | Terapia Presencial accordion (3 fotos) | `consultorio-1-optimized.jpg`, `consultorio-2-optimized.jpg`, `consultorio-3-optimized.jpg` | 3 imágenes en accordion expandido |
| 5.5 | Terapia Online accordion | `manos-libreta.jpg` | Imagen visible |
| 5.6 | Redes & Agenda (tarjeta presentación) | `tarjeta-presentacion-optimized.jpg` | En sección redes |
| 5.7 | Favicons / Apple touch | `logo-psh.png` (ya en `<head>`) | Pestaña navegador |

---

### FASE 6 — VERIFICACIONES OBLIGATORIAS (Checklist final)

| Check | Comando / Acción | Estado esperado |
|---|---|---|
| C-1 | Cero precios visibles | `grep -i "S/" index.html` → 0 |
| C-2 | Cero direcciones exactas | `grep -i "San Isidro\|Surco\|dirección" index.html` → 0 |
| C-3 | TCC → ACT en TODO el sitio | `grep -i "TCC" index.html` → 0 (salvo comentarios) |
| C-4 | Nav links válidos | Todos `href="#..."` tienen `id` correspondiente |
| C-5 | Paleta oficial aplicada | Variables `:root` = cremas, yellows, celestes; NO `--ink`, NO `--muted` viejo |
| C-6 | Tipografías de marca | Google Fonts: League Spartan, Open Sans, Glacial Indifference |
| C-7 | Estilos orgánicos | `border-radius` orgánicos, ondas, no cajas rectangulares duras |
| C-8 | Ebooks oculta no borrada | `grep "DESHABILITADO v1" index.html` → 2 ocurrencias |
| C-9 | WhatsApp +51 939855573 | `grep "wa.me/51939855573" index.html` → 12+ ocurrencias |
| C-10 | Botones Agenda → WhatsApp | Todos botones "Agendar" → `wa.me/51939855573` `target="_blank"` |
| C-11 | **Sin azul oscuro** | `grep -i "1A2E35\|INK\|ink" index.html` → 0 (salvo comentarios) |
| C-12 | **Sombras solo celeste/amarillo** | `grep -n "rgba(" index.html` → solo `111,193,255` o `255,251,133` |
| C-13 | **Títulos son celeste** | `grep "title-color\|celeste-deep" index.html` en headings |
| C-14 | **Textos son gris-celeste** | `grep "text-dark\|3A4A5A" index.html` en párrafos |
| C-15 | Ondas Hero funcionando | Abrir en browser → ondas animadas detrás del contenido |
| C-16 | Responsive ≤768px | Hero, servicios, testimonios, footer, mobile sticky CTA, WhatsApp float OK |
| C-17 | Performance | Lighthouse ≥90 (Performance/Accessibility/Best Practices/SEO) |

---

### FASE 7 — FIREBASE / BACKEND (Pendiente credenciales clienta)

| T# | Descripción | Bloqueante |
|---|---|---|
| 7.1 | Firebase project en cuenta Google clienta → agregar Paolo (Owner/Editor) | Clienta |
| 7.2 | Firestore + Auth (email/password) + Hosting rules | 7.1 |
| 7.3 | Firebase SDK modular v9+ en `index.html` (antes `</body>`) | 7.1 |
| 7.4 | `firebase-config.js` (gitignored) con credenciales | 7.1 |
| 7.5 | Colección `testimonios` + formulario público (`aprobado: false`) | 7.2 |
| 7.6 | Carrusel testimonios: merge estáticos + `where('aprobado',==',true)` | 7.5 |
| 7.7 | Auth admin `/admin` → solo email clienta | 7.2 |
| 7.8 | Panel admin: aprobar/rechazar testimonios + crear posts blog | 7.7 |
| 7.9 | Render blog público (sección `#blog` o página aparte) | 7.8 |
| 7.10 | Firestore rules deploy | 7.2 |

> **NOTA:** Fase 7 NO se ejecuta hasta que la clienta provea credenciales. Placeholder Behold.so ya está en código (ver `INVENTARIO_CAMBIOS.md` C-2).

---

## ARCHIVOS DE REFERENCIA DEL PROYECTO (Mantener)

| Archivo | Propósito |
|---|---|
| `CONTEXTO_proyecto_landing-fernanda.md` | Contexto, branding, reglas duras, stack, decisiones v1/v2 |
| `INVENTARIO_CAMBIOS.md` | Inventario exhaustivo de cambios (A/B/C/D) con IDs trazables |
| `PLAN_TAREAS.md` | Plan de ejecución con checklist R-1 a R-10 y estado actual |
| `assets/logos/README.md` | Guía técnica para exportar logos (celeste/ink, 96/192px, PNG transparente) |
| `TAREAS_PENDIENTES_FINAL.md` | **ESTE ARCHIVO** — Plan final consolidado |

---

## ORDEN DE EJECUCIÓN RECOMENDADO

```
┌─────────────────────────────────────────────────────────────┐
│ 1️⃣  FASE 1 — Paleta y variables CSS (30 min)               │
│ 2️⃣  FASE 2 — Limpieza --ink global (60-90 min)             │
│ 3️⃣  FASE 3 — Ondas dinámicas Hero (30 min)                 │
│ 4️⃣  FASE 4 — Botones unificados (30 min)                   │
│ 5️⃣  FASE 5 — Rutas de imágenes (15 min)                    │
│ 6️⃣  FASE 6 — Checklist C-1 a C-17 (45 min)                 │
│ 7️⃣  FASE 7 — Firebase (QUEDA PENDIENTE credenciales)       │
└─────────────────────────────────────────────────────────────┘
```

---

## COMANDOS ÚTILES DE VERIFICACIÓN RÁPIDA

```bash
# Paleta: verificar que NO quedan referencias a colores viejos
grep -n "1A2E35\|7A9A8A\|INK\|ink" index.html

# Sombras: solo tonos permitidos
grep -n "rgba(" index.html

# Títulos usan title-color / celeste-deep
grep -n "title-color\|celeste-deep" index.html | head -20

# Textos usan text-dark / 3A4A5A
grep -n "text-dark\|3A4A5A" index.html | head -20

# Botones
grep -n 'class="btn' index.html

# Imágenes optimizadas
grep -n "optimized" index.html

# Nav IDs vs hrefs
grep -oP 'href="#[^"]+"' index.html | sort -u
grep -oP 'id="[^"]+"' index.html | sort -u

# Checklist final
echo "R-1:" && grep -ic "S/" index.html
echo "R-2:" && grep -ic -E "San Isidro|Surco|dirección" index.html
echo "R-3:" && grep -ic "TCC" index.html
echo "R-8:" && grep -c "DESHABILITADO v1" index.html
echo "R-9:" && grep -c "wa.me/51939855573" index.html
```

---

## NOTAS CRÍTICAS PARA LA IMPLEMENTACIÓN

1. **Single-file architecture**: Todo CSS en `<style>` dentro de `index.html`. NO crear archivos externos.
2. **Paleta bloqueada**: Solo redistribuir usos. NO inventar nuevos hex. Los 11 colores oficiales son inmutables.
3. **Organic/retro-groovy**: `border-radius` asimétricos (ej: `40% 60% 30% 70%`), blobs, ondas, transiciones suaves. Cero esquinas de 0px o 4px rígidas en elementos nuevos.
4. **currentColor en SVGs**: Todos los iconos inline usan `fill="currentColor"` o `stroke="currentColor"` para heredar color del contenedor.
5. **will-change**: Solo en `.wave`, `.testimonios-track`, `.hero-photo` (elementos animados).
6. **Comentarios en CSS**: Marcar bloques con `/* SECCIÓN: Nombre */` para navegación rápida en 3600+ líneas.
7. **Deploy**: GitHub Pages automático desde `main` → https://elbrujo325.github.io/landing-maria-fernanda/

---

## ENTREGABLE ESPERADO

**`index.html`** que cumpla:
- ✅ Visual: Limpio, moderno, orgánico, en movimiento (ondas Hero)
- ✅ Paleta: 100% oficial PSH, sin verde/azul oscuro, sombras celeste/ámbar
- ✅ Tipografía: League Spartan / Open Sans / Glacial Indifference
- ✅ Funcional: Nav, accordion, carrusel, WhatsApp links, responsive
- ✅ Código: Estructurado, comentado, single-file, sin CSS/JS externo
- ✅ Checklist: C-1 a C-17 en verde

---

**Próximo paso:** Ejecutar Fase 1 → 2 → 3 → 4 → 5 → 6 en orden, verificando tras cada fase. Fase 7 queda en `⏳ BLOQUEADA` hasta credenciales Firebase.