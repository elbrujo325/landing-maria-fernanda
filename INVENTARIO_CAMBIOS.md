# INVENTARIO COMPLETO DE CAMBIOS — Landing "Pensar Sentir Hacer"

**Archivo base:** `index.html` (3.629 líneas)  
**Fecha:** 2026-07-21  
**Fuente:** Brief del cliente + revisión exhaustiva del HTML actual  
**Última actualización:** 2026-07-21 — Commit `8f28dab` (Grupos 1-5 completados ✅)

---

## ÍNDICE DE CAMBIOS

| ID | Categoría | Sección / Línea | Cambio requerido | Estado |
|---|---|---|---|---|
| **A-1** | Copy | `<title>` línea 6 | `TCC` → `ACT` | ✅ |
| **A-2** | Copy | `<meta description>` línea 7 | `TCC` → `ACT`; "Psicóloga clínica y psicoterapeuta Cognitivo Conductual" → "Psicóloga clínica ACT, especialista en bienestar emocional" | ✅ |
| **A-3** | Copy | Hero eyebrow línea 2699 | `"Psicóloga Clínica · TCC · Lima & Online"` → `"Psicóloga clínica ACT, especialista en bienestar emocional"` | ✅ |
| **A-4** | Copy | Social-proof bar líneas 2754-2759 | `"Colegio de Psicólogos del Perú · N° 48921 TCC Certificada Terapia de Pareja Sistémica"` → `"CPsP. 46797 Magister en Terapia de Tercera Generación y Bienestar Emocional"` | ✅ |
| **A-5** | Copy | Social-proof stats líneas 2738-2749 | Insertar stat `+12 países` junto a experiencia (no junto a pacientes). Texto cliente: *"+7 años de experiencia, +12 países"* | ✅ |
| **A-6** | Copy | Sección "Sobre mí" líneas 2769-2783 | Reemplazar texto completo por texto provisto por clienta (con TCC→ACT) | ✅ |
| **A-7** | Copy | Sección Credenciales líneas 2799-2858 | Reemplazar todas las menciones "TCC" → "ACT" (líneas 2813, 2852, etc.) | ✅ |
| **A-8** | Copy | FAQ "Terapia online" línea 3316 | "TCC online" → "ACT online" | ✅ |
| **A-9** | Copy | FAQ "¿Atendés menores?" líneas 3393-3400 | Cambiar respuesta: SÍ atiende adolescentes, según caso y evaluación previa | ✅ |
| **A-10** | Copy | Footer línea 3461 | "Psicóloga Clínica TCC" → "Psicóloga Clínica ACT" + WhatsApp +51 939855573 | ✅ |
| **A-11** | Copy | WhatsApp float línea 3467 | `href="#"` → `href="https://wa.me/51939855573"` | ✅ |
| **A-12** | Copy | CTA final "Agendar mi primera sesión" línea 3414 | `href="#agenda"` → `href="https://wa.me/51939855573"` (target=_blank) | ✅ |
| **A-13** | Copy | Botón WhatsApp CTA línea 3415 | `href="#"` → `href="https://wa.me/51939855573"` | ✅ |
| **A-14** | Copy | Nav botón "Agendar" línea 2685 | `href="#agenda"` → `href="https://wa.me/51939855573"` (target=_blank) | ✅ |
| **A-15** | Copy | Servicios botones "Agendar" líneas 2941, 2956 | `href="#agenda"` → `href="https://wa.me/51939855573"` (target=_blank) | ✅ |

---

| ID | Categoría | Sección / Línea | Cambio requerido | Estado |
|---|---|---|---|---|
| **B-1** | Eliminar/Deshabilitar | Nav dropdown líneas 2675-2679 | Item "Ebooks & Recursos" → **ocultar con `display:none` + comentario `<!-- DESHABILITADO v1 - reactivar en v2 -->`** NO eliminar del código | ✅ |
| **B-2** | Eliminar/Deshabilitar | Servicios tarjeta 3 líneas 2963-2975 | Tarjeta completa "Ebooks & Recursos" → **ocultar con `display:none` + comentario igual** | ✅ |
| **B-3** | Eliminar | Sección Precios completa líneas 3047-3106 | **ELIMINAR bloque completo** (incluye `id="precios"` y todo su contenido). NO dejar código comentado. | ✅ |
| **B-4** | Eliminar | Nav link "Precios" línea 2683 | Eliminar `<li><a href="#precios">Precios</a></li>` | ✅ |
| **B-5** | Eliminar | Footer link "Precios" línea 3449 | Eliminar `<li><a href="#precios">Precios</a></li>` | ✅ |
| **B-6** | Eliminar | Sección "Cómo funciona" completa líneas 3019-3044 | **ELIMINAR bloque completo** (incluye `id="como-funciona"`). NO dejar código comentado. | ✅ |
| **B-7** | Eliminar | Nav link "¿Te sientes así?" línea 2681 | Se mantiene — apunta a `#problema-solucion` que SÍ queda | ✅ (se queda) |

---

| ID | Categoría | Sección / Línea | Cambio requerido | Estado |
|---|---|---|---|---|
| **C-1** | Nueva sección | Después de Testimonios / Antes de FAQ | **Sección "Redes & Agenda" (reemplaza espacio de Precios)**: Instagram, TikTok, Facebook, WhatsApp todos `@pensarsentirhacer.pe` + botón CTA WhatsApp | ✅ |
| **C-2** | Nueva sección | Dentro de C-1 | **Feed Instagram vivo (Behold.so)**: embed widget conectado a `@pensarsentirhacer.pe`. Requiere que clienta conecte su cuenta en Behold.so. Patrón de proyecto "Luz de Cristo / Luxto". | ✅ (placeholder listo) |
| **C-3** | Nueva sección | Sección "Sobre mí" (líneas 2764-2786) | **Video YouTube embebido** después del texto: `https://www.youtube.com/watch?v=CfACxsC7K-A` → iframe responsive | ✅ |
| **C-4** | Nueva funcionalidad | Servicios líneas 2933-2977 | **Accordion/desplegable** en cada tarjeta servicio (Presencial / Online): duración, modalidad, qué incluye. **NO precio ni dirección exacta.** | ✅ |
| **C-5** | Nueva funcionalidad | Debajo de Testimonios (línea 3300) | **Formulario reseñas públicas**: nombre, texto, estrellas 1-5. Envío → Firestore `testimonios` con `aprobado: false`. Moderación admin. Render dinámico en carrusel. | ⏳ (Grupo 6 - Firebase) |

---

| ID | Categoría | Sección / Línea | Cambio requerido | Estado |
|---|---|---|---|---|
| **D-1** | Backend | Firebase | Configurar projecto Firebase **bajo cuenta Google de la clienta** (coordinar con Paolo). Firestore + Auth + Hosting rules. | ⏳ |
| **D-2** | Backend | Firestore | Colección `testimonios`: `{ nombre, texto, estrellas, fecha, aprobado: boolean }`. Default `aprobado: false`. | ⏳ |
| **D-3** | Backend | Firestore | Colección `blogs`: `{ titulo, cuerpo, imagen_url, fecha, publicado: boolean }`. Solo `publicado: true` se renderiza en público. | ⏳ |
| **D-4** | Backend | Auth/Admin | Ruta protegida `/admin` (Firebase Auth email/password solo clienta). Panel: crear/edit blog (rich text básico: título, cuerpo, imagen opcional), ver/aprobar/rechazar testimonios pendientes. | ⏳ |
| **D-5** | Backend | Frontend | Integrar Firebase SDK en `index.html` (modular SDK v9+). Formulario reseñas → write a `testimonios`. Carrusel testimonios → leer `testimonios` con `aprobado: true` + merge con testimonios estáticos actuales. | ⏳ |

---

## REGLAS TRANSVERSALES (Deben verificarse en CADA cambio)

| Regla | Descripción | Verificación | Estado |
|---|---|---|---|
| **R-1** | **Cero precios visibles** | `grep -i "S/" index.html` → 0 resultados; `grep -i "precio" index.html` → 0 (excepto comentarios) | ✅ |
| **R-2** | **Cero direcciones exactas** | `grep -i "San Isidro\|Surco\|dirección" index.html` → 0 resultados | ✅ |
| **R-3** | **TCC → ACT en TODO el sitio** | `grep -i "TCC" index.html` → 0 resultados (excepto comentarios) | ✅ |
| **R-4** | **Nav links válidos** | Todos los `href="#..."` del nav/footer apuntan a `id` existentes en el HTML final | ✅ |
| **R-5** | **Paleta vainilla intacta** | Variables CSS `--blue-light`, `--blue-mid`, `--blue-deep`, `--brand-cream`, `--white`, `--ink`, `--muted`, `--gradient-bg`, `--gradient-hero`, `--card-bg`, `--accent-cool` **no cambian** | ✅ |
| **R-6** | **Tipografías intactas** | `Bebas Neue`, `Fraunces`, `Inter`, `Glacial Indifference` (si se usa) no cambian | ✅ |
| **R-7** | **Estilos orgánicos/retro-groovy** | `border-radius` orgánicos, blobs/ondas, no bordes rectangulares duros nuevos | ✅ |
| **R-8** | **Sección Ebooks oculta, no borrada** | Buscar `<!-- DESHABILITADO v1` → 2 ocurrencias (nav + servicios) | ✅ |
| **R-9** | **WhatsApp +51 939855573** | Todos los `href="https://wa.me/51939855573"` (formato sin espacios) | ✅ (12 ocurrencias) |
| **R-10** | **Botones Agenda → WhatsApp** | Todos los botones "Agendar" → `https://wa.me/51939855573` con `target="_blank"` | ✅ |

---

## MAPA DE SECCIONES HTML (IDs actuales)

| ID | Sección | Estado final |
|---|---|---|
| `#navbar` | Navbar | Queda (con links actualizados) |
| `#hero` | Hero | Queda (copy A-3, A-5, CTA WhatsApp) |
| `#social-proof-bar` | Social proof bar | Queda (copy A-4, A-5) |
| `#sobre-mi` | Sobre mí | Queda (copy A-6 + video C-3) |
| `#credenciales` | Credenciales | Queda (copy A-7) |
| `#problema-solucion` | Problema/Solución | Queda |
| `#servicios` | Servicios | Queda + accordion C-4 + oculta ebooks B-2 + fotos consultorio/manos-libreta |
| `#mision` | Misión | Queda |
| **`#como-funciona`** | Cómo funciona | **ELIMINADO (B-6)** |
| **`#precios`** | Precios | **ELIMINADO (B-3)** |
| `#testimonios` | Testimonios | Queda + pendiente formulario reseñas C-5 |
| `#faq` | FAQ | Queda (copy A-9) |
| `#agenda` | CTA Final | Queda (links A-12, A-13, A-14, A-15 → WhatsApp) |
| `#redes-agenda` | Redes & Agenda | **NUEVA (C-1, C-2)** insertada entre `#testimonios` y `#faq` |

---

## CHECKLIST DE VERIFICACIÓN FINAL (Antes de cerrar cada fase)

- [x] `grep -i "TCC" index.html` → 0 resultados (salvo comentarios)
- [x] `grep -i "S/" index.html` → 0 resultados (salvo comentarios)
- [x] `grep -i "San Isidro\|Surco\|dirección" index.html` → 0 resultados
- [x] Todos los `href="#..."` del nav/footer tienen `id` correspondiente en el HTML
- [x] Paleta CSS variables sin cambios
- [x] Fonts Google Fonts sin cambios
- [x] Sección Ebooks: 2 comentarios `<!-- DESHABILITADO v1 - reactivar en v2 -->` presentes
- [x] WhatsApp links todos `https://wa.me/51939855573`
- [x] Botones Agenda: todos → WhatsApp con `target="_blank"`
- [ ] Firebase SDK cargado (modular v9+) — **Grupo 6 pendiente**
- [ ] `/admin` route protegida — **Grupo 6 pendiente**

---

## ORDEN DE EJECUCIÓN SUGERIDO (Fase 3)

1. ✅ **Copy-only** (A-1 a A-15) — cambios puros de texto, sin tocar estructura
2. ✅ **Eliminaciones/Deshabilitaciones** (B-1 a B-6) — borrar/ocultar secciones
3. ✅ **Nav/Footer links cleanup** (B-4, B-5, A-14, A-15) — consistencia navegación
4. ✅ **Nueva sección Redes & Agenda** (C-1, C-2) — HTML + CSS + Behold.so embed placeholder
5. ✅ **Video YouTube en Sobre mí** (C-3) — iframe responsive
6. ✅ **Accordion Servicios** (C-4) — JS + CSS + HTML en tarjetas existentes
7. ✅ **Fotos reales** — consultorio-1/2/3, manos-libreta, tarjeta-presentacion, logo-psh
8. ⏳ **Formulario Reseñas + integración Firebase** (C-5, D-1 a D-5) — **Fase completa de backend (requiere credenciales clienta)**
9. ✅ **Verificación final completa** checklist R-1 a R-10 (excepto R-7.13 performance)

---

## NOTAS DE COORDINACIÓN CON PAOLO/CLIENTA

- **Firebase**: La clienta debe crear cuenta Google → crear proyecto Firebase → agregar a Paolo como colaborador → Paolo configura Firestore/Auth/Hosting.
- **Behold.so**: La clienta debe crear cuenta en Behold.so → conectar Instagram `@pensarsentirhacer.pe` → obtener embed code → dar a Paolo. **Placeholder ya está en código.**
- **WhatsApp**: Número confirmado `+51 939855573` → formato wa.me `https://wa.me/51939855573`.
- **Agenda bit.ly**: **ELIMINADO por decisión del usuario** — todos los botones CTA ahora van directo a WhatsApp.
- **Moderación testimonios**: Por defecto `aprobado: false` (moderación previa). Confirmar con Paolo/clienta si quieren auto-publicar.
- **Blog admin**: Rich text básico (título, cuerpo, imagen opcional). Confirmar si necesitan categorías/tags o solo posts planos.

---

## IMÁGENES AGREGADAS AL REPO (commit 8f28dab)

| Archivo | Tamaño | Uso | Notas |
|---|---|---|---|
| `logo-psh.png` | 60 KB | Navbar + Footer | Reemplaza logo_mariafernanda.png (21 KB) — tamaño correcto para clip-path CSS |
| `consultorio-1.jpg` | 2.2 MB | Terapia Presencial accordion | Sala de espera |
| `consultorio-2.jpg` | 3.0 MB | Terapia Presencial accordion | Sillón y jardín |
| `consultorio-3.jpg` | 2.9 MB | Terapia Presencial accordion | Vista amplia |
| `manos-libreta.jpg` | 109 KB | Terapia Online accordion | Manos con libreta |
| `tarjeta-presentacion.jpg` | 3.5 MB | Redes & Agenda section | Tarjeta presentación PSH |
| `fernanda-headshot.png` | 199 KB | Backup/futuro | Foto profesional transparente |
| `foto-fernanda.png` | 199 KB | Hero + Sobre mí | Foto profesional actual |
| `logo_mariafernanda.png` | 21 KB | Referencia | Logo original pequeño |

**Deploy:** GitHub Pages automático desde `main` branch → https://elbrujo325.github.io/landing-maria-fernanda/
