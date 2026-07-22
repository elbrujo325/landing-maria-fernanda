# PLAN DE TAREAS — Landing "Pensar Sentir Hacer"

**Fuente:** Inventario `INVENTARIO_CAMBIOS.md`  
**Orden:** Ejecución secuencial, verificando tras cada tarea que no se rompe nada (nav, estilos, enlaces internos)  
**Criterio done:** Cada tarea se marca ✅ solo si pasa verificación local (abrir `index.html` en browser / live server) y checklist transversal R-1 a R-10

---

## GRUPO 1 — COPY PURO (Solo texto, sin tocar estructura)

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 1.1 | A-1 | `<title>`: TCC → ACT | `index.html:6` | `grep "<title>" index.html` | ✅ |
| 1.2 | A-2 | `<meta description>`: TCC → ACT + copy clienta | `index.html:7` | `grep "meta description" index.html` | ✅ |
| 1.3 | A-3 | Hero eyebrow: "Psicóloga Clínica · TCC · Lima & Online" → "Psicóloga clínica ACT, especialista en bienestar emocional" | `index.html:2699` | Visual hero | ✅ |
| 1.4 | A-4 | Social-proof bar credenciales: "Colegio... N° 48921 TCC..." → "CPsP. 46797 Magister en Terapia de Tercera Generación y Bienestar Emocional" | `index.html:2755` | Visual social-proof bar | ✅ |
| 1.5 | A-5 | Social-proof stats: agregar stat "+12 países" junto a experiencia (no junto a +150 pacientes) | `index.html:2742-2743` | 4 stats visibles: +150, +7 años +12 países, 2 sedes, 100% online | ✅ |
| 1.6 | A-6 | Sección "Sobre mí": reemplazar texto completo por versión clienta (con TCC→ACT) | `index.html:2768-2771` | Visual sobre-mi completo | ✅ |
| 1.7 | A-7 | Credenciales: todas menciones "TCC" → "ACT" (líneas 2813, 2852, etc.) | `index.html:2799-2858` | `grep -i "TCC" index.html` → 0 | ✅ |
| 1.8 | A-8 | FAQ terapia online: "TCC online" → "ACT online" | `index.html:~3379` | Visual FAQ item | ✅ |
| 1.9 | A-9 | FAQ "¿Atendés menores?": respuesta → "Sí atiendo adolescentes, dependiendo del caso y previa evaluación/validación de la psicóloga" | `index.html:3463` | Visual FAQ item | ✅ |
| 1.10 | A-10 | Footer: "Psicóloga Clínica TCC" → "Psicóloga Clínica ACT" | `index.html:3526` | Visual footer | ✅ |
| 1.11 | A-11 | WhatsApp float: `href="#"` → `href="https://wa.me/51939855573"` | `index.html:3532` | Click abre WhatsApp | ✅ |
| 1.12 | A-12 | CTA final botón principal: `href="#agenda"` → `href="https://wa.me/51939855573"` (target=_blank) | `index.html:2714, 3477` | Click abre WhatsApp en nueva pestaña | ✅ |
| 1.13 | A-13 | CTA final botón WhatsApp: `href="#"` → `href="https://wa.me/51939855573"` | `index.html:3478` | Click abre WhatsApp | ✅ |
| 1.14 | A-14 | Nav botón "Agendar": `href="#agenda"` → `href="https://wa.me/51939855573"` | `index.html:2684` | Click nav abre WhatsApp | ✅ |
| 1.15 | A-15 | Servicios botones "Agendar": `href="#agenda"` → `href="https://wa.me/51939855573"` (2 ocurrencias) | `index.html:2985, 3045` | Click botones abre WhatsApp | ✅ |

---

## GRUPO 2 — ELIMINACIONES / DESHABILITACIONES

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 2.1 | B-1 | Nav dropdown: ocultar "Ebooks & Recursos" con `style="display:none"` + comentario `<!-- DESHABILITADO v1 - reactivar en v2 -->` | `index.html:2678` | Nav dropdown muestra solo 2 items; código comentado presente | ✅ |
| 2.2 | B-2 | Servicios: ocultar tarjeta 3 "Ebooks & Recursos" con `style="display:none"` + mismo comentario | `index.html:3052` | Grid muestra 2 tarjetas; 3ª oculta en código | ✅ |
| 2.3 | B-3 | **ELIMINAR** sección Precios completa (`id="precios"` líneas 3047-3106) | `index.html:3047-3106` | Sección desaparece; no queda `id="precios"` en HTML | ✅ |
| 2.4 | B-4 | Nav: eliminar `<li><a href="#precios">Precios</a></li>` | `index.html:2683` | Nav sin link Precios | ✅ |
| 2.5 | B-5 | Footer: eliminar `<li><a href="#precios">Precios</a></li>` | `index.html:3449` | Footer sin link Precios | ✅ |
| 2.6 | B-6 | **ELIMINAR** sección "Cómo funciona" completa (`id="como-funciona"` líneas 3019-3044) | `index.html:3019-3044` | Sección desaparece; no queda `id="como-funciona"` | ✅ |

---

## GRUPO 3 — NUEVA SECCIÓN: REDES & AGENDA (reemplaza espacio de Precios)

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 3.1 | C-1 | Crear sección nueva `#redes-agenda` (después de `#testimonios`, antes de `#faq`): grid 4 iconos (IG, TT, FB, WA) todos `@pensarsentirhacer.pe` + botón CTA agenda | `index.html:3312-3363` | Sección visible, links correctos | ✅ |
| 3.2 | C-2 | Embed Behold.so feed Instagram dentro de sección #redes-agenda (iframe/widget). Requiere embed code de clienta. Placeholder con comentario si no hay code aún. | `index.html:3354-3361` | Feed visible o placeholder claro | ✅ (placeholder) |

---

## GRUPO 4 — VIDEO YOUTUBE EN "SOBRE MÍ"

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 4.1 | C-3 | Insertar iframe YouTube responsive después del texto en `#sobre-mi`: `https://www.youtube.com/watch?v=CfACxsC7K-A` → embed `https://www.youtube.com/embed/CfACxsC7K-A` | `index.html:2780-2784` | Video reproduce, responsive 16:9 | ✅ |

---

## GRUPO 5 — ACCORDION EN SERVICIOS

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 5.1 | C-4 | Convertir tarjetas servicio (Presencial, Online) en accordion: click → despliega detalles (duración, modalidad, qué incluye). **Sin precio ni dirección exacta.** | `index.html:2937-3049` + CSS + JS | Click abre/cierra; contenido correcto; mobile ok | ✅ |
| 5.2 | C-4 | Tarjeta "Ebooks" (ya oculta B-2) también con accordion estructura por si se reactiva v2 | `index.html:3052-3070` | Estructura lista, oculta | ✅ |
| 5.3 | — | **Añadir fotos consultorio** (3 imágenes) en Terapia Presencial accordion expandido | `index.html:2976-2995` | 3 fotos visibles al expandir | ✅ |
| 5.4 | — | **Añadir foto manos-libreta.jpg** en Terapia Online accordion expandido | `index.html:3040-3042` | Foto visible al expandir | ✅ |

---

## GRUPO 6 — FORMULARIO RESEÑAS + FIREBASE BACKEND (Fase completa D) — **PENDIENTE (requiere credenciales clienta)**

| T# | ID Inventario | Descripción | Archivo/Líneas | Verificación rápida | Estado |
|---|---|---|---|---|---|
| 6.1 | D-1 | Firebase setup: crear proyecto en cuenta Google clienta → Firestore + Auth (email/password) + Hosting rules. Coordinar con Paolo para acceso. | Externo (Firebase Console) | Proyecto creado, Paolo tiene acceso Editor/Owner | ⏳ |
| 6.2 | D-2 | Agregar Firebase SDK modular (v9+) en `index.html` antes de `</body>`: `import { initializeApp } from '...'`, `getFirestore`, `getAuth`, `collection`, `addDoc`, `onSnapshot`, `query`, `where`, `orderBy` | `index.html:~3627` (antes scripts) | Sin errores consola; `firebase` global disponible | ⏳ |
| 6.3 | D-2 | Config `firebaseConfig` con credenciales del proyecto clienta (no hardcodear en repo público: usar build-time env o archivo `firebase-config.js` gitignored) | Nuevo archivo `firebase-config.js` | Config cargada, no en repo | ⏳ |
| 6.4 | D-2 | Colección `testimonios`: formulario público (nombre, texto, estrellas 1-5, fecha `serverTimestamp()`, `aprobado: false`). Submit → `addDoc` → toast éxito "Enviado para revisión". | Nuevo HTML form + JS | Formulario envía, documento en Firestore con `aprobado:false` | ⏳ |
| 6.5 | D-3 | Carrusel testimonios: leer `testimonios` con `where('aprobado','==',true)` + `orderBy('fecha','desc')` + merge con testimonios estáticos actuales. Render dinámico en `#testimoniosTrack`. | JS en `index.html` | Carrusel muestra estáticos + aprobados dinámicos | ⏳ |
| 6.6 | D-4 | Auth admin: ruta `/admin` (o sección oculta en mismo index con `?admin=1`) → `signInWithEmailAndPassword` solo email clienta. Logout button. | Nuevo HTML/JS bloque | Login funciona, solo email clienta accede | ⏳ |
| 6.7 | D-4 | Panel admin: (a) Lista testimonios pendientes (`aprobado:false`) → botones Aprobar/Rechazar (update `aprobado:true/false` + `delete` si rechaza). (b) Form blog: título, cuerpo (textarea + simple toolbar: negrita, cursiva, link, imagen URL), checkbox `publicado`. Submit → `blogs` collection. | JS admin panel | Admin ve pendientes, aprueba/rechaza; crea posts blog | ⏳ |
| 6.8 | D-3 | Render blog público: sección nueva `#blog` (opcional v1) o página aparte. Query `blogs` `where('publicado','==',true)` `orderBy('fecha','desc')`. Mostrar cards con título, excerpt, imagen, fecha. | Nueva sección o página | Posts publicados visibles | ⏳ |
| 6.9 | D-5 | Reglas Firestore: `testimonios` write público solo create con `aprobado:false`; read público solo `aprobado:true`. `blogs` read público solo `publicado:true`; write solo auth clienta. | `firestore.rules` deploy | Reglas deployadas y probadas | ⏳ |

---

## GRUPO 7 — VERIFICACIÓN TRANSVERSAL FINAL

| T# | Descripción | Comando/Check | Estado |
|---|---|---|---|
| 7.1 | **R-1** Cero precios visibles | `grep -i "S/" index.html` → 0 | ✅ |
| 7.2 | **R-2** Cero direcciones exactas | `grep -i "San Isidro\|Surco\|dirección" index.html` → 0 | ✅ |
| 7.3 | **R-3** TCC → ACT en todo el sitio | `grep -i "TCC" index.html` → 0 (salvo comentarios) | ✅ |
| 7.4 | **R-4** Nav links válidos | Todos `href="#..."` en nav/footer tienen `id` correspondiente | ✅ |
| 7.5 | **R-5** Paleta CSS variables intactas | Diff de `:root` block vs original = 0 cambios | ✅ |
| 7.6 | **R-6** Tipografías intactas | Google Fonts link sin cambios | ✅ |
| 7.7 | **R-7** Estilos orgánicos | No nuevos `border-radius: 0px` ni cajas rectangulares duras | ✅ |
| 7.8 | **R-8** Ebooks oculta no borrada | `grep "DESHABILITADO v1" index.html` → 2 resultados | ✅ |
| 7.9 | **R-9** WhatsApp +51 939855573 | `grep "wa.me/51939855573" index.html` → 12 ocurrencias | ✅ |
| 7.10 | **R-10** Botones Agenda → WhatsApp | Todos botones "Agendar" → `wa.me/51939855573` target=_blank | ✅ |
| 7.11 | Navegación fluida | Scroll suave, navbar theme-dark/scroll funciona, mobile menu ok | ✅ |
| 7.12 | Responsive ≤768px | Hero, servicios, testimonios, footer, mobile sticky CTA, WhatsApp float no se solapan | ✅ |
| 7.13 | Performance | Lighthouse ≥90 Performance/Accessibility/Best Practices/SEO | ⏳ |

---

## ORDEN DE EJECUCIÓN RECOMENDADO

```
Grupos 1-5 COMPLETADOS ✅
Fase 3.6 (Grupo 6) → Tareas 6.1 a 6.9   (Firebase + Form + Admin - FASE COMPLEJA, coordinar con Paolo)
Fase 3.7 (Grupo 7) → Tareas 7.13        (Performance Lighthouse - pendiente)
```

---

## NOTAS DE COORDINACIÓN CRÍTICAS

| Tema | Acción requerida | Responsable | Deadline sugerido |
|---|---|---|---|
| Firebase project | Crear proyecto en cuenta Google clienta → agregar Paolo (Owner/Editor) | Clienta + Paolo | Antes de Tarea 6.1 |
| Behold.so embed | Clienta crea cuenta Behold.so → conecta IG `@pensarsentirhacer.pe` → copia embed code → pasa a Paolo | Clienta | Cuando quiera activar feed real |
| WhatsApp number | Confirmado **+51 939855573** → formato `https://wa.me/51939855573` | Clienta (confirmado en brief) | ✅ Ya |
| Agenda link | **Eliminado bit.ly** por decisión usuario — todos botones → WhatsApp directo | Paolo | ✅ Hecho |
| Moderación testimonios | Default `aprobado:false` (moderación previa). ¿Confirmar o quieren auto-publicar? | Paolo + Clienta | Antes de Tarea 6.4 |
| Blog admin | ¿Rich text básico suficiente (título, cuerpo, imagen URL)? ¿Categorías/tags necesarios v1? | Paolo + Clienta | Antes de Tarea 6.7 |

---

## COMANDOS ÚTILES PARA VERIFICACIÓN RÁPIDA

```bash
# Verificar copy TCC→ACT
grep -n -i "TCC" index.html

# Verificar precios eliminados
grep -n -i "S/" index.html

# Verificar direcciones
grep -n -i "San Isidro\|Surco" index.html

# Verificar nav links vs ids existentes
grep -oP 'href="#[^"]+"' index.html | sort -u
grep -oP 'id="[^"]+"' index.html | sort -u

# Verificar WhatsApp links
grep -n "wa.me/51939855573" index.html

# Verificar Ebooks deshabilitado
grep -n "DESHABILITADO v1" index.html

# Verificar todas las reglas R-1 a R-10
echo "R-1:" && grep -i "S/" index.html | wc -l
echo "R-2:" && grep -i -E "San Isidro|Surco|dirección" index.html | wc -l
echo "R-3:" && grep -i "TCC" index.html | wc -l
echo "R-4:" && grep -oP 'href="#[^"]+"' index.html | sort -u
echo "R-8:" && grep -c "DESHABILITADO v1" index.html
echo "R-9:" && grep -c "wa.me/51939855573" index.html
echo "IDs:" && grep -oP 'id="[^"]+"' index.html | grep -E "(sobre-mi|servicios|problema-solucion|testimonios|faq|redes-agenda|agenda)" | sort -u
```

---

## ARCHIVOS DE IMAGEN AGREGADOS AL REPO (commit 8f28dab)

| Archivo | Uso | Tamaño |
|---|---|---|
| `logo-psh.png` | Navbar + Footer logo (reemplaza logo_mariafernanda.png) | 60 KB |
| `consultorio-1.jpg` | Terapia Presencial accordion | 2.2 MB |
| `consultorio-2.jpg` | Terapia Presencial accordion | 3.0 MB |
| `consultorio-3.jpg` | Terapia Presencial accordion | 2.9 MB |
| `manos-libreta.jpg` | Terapia Online accordion | 109 KB |
| `tarjeta-presentacion.jpg` | Redes & Agenda section | 3.5 MB |
| `fernanda-headshot.png` | Foto profesional (backup) | 199 KB |
| `foto-fernanda.png` | Hero + Sobre mí photo | 199 KB |
| `logo_mariafernanda.png` | Logo original (referencia) | 21 KB |

**Deploy:** GitHub Pages automático desde `main` branch → https://elbrujo325.github.io/landing-maria-fernanda/
