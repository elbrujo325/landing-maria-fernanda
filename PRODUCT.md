# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

**Primary:** Adultos (25–55 años) en Perú y Latinoamérica que buscan terapia psicológica online o presencial. Presentan ansiedad, depresión, conflictos de pareja/familiares, o buscan crecimiento personal. Valoran la credencial profesional (CPP 46797), la especialización en ACT (Terapia de Aceptación y Compromiso) y la flexibilidad de modalidad (online desde +12 países / presencial en Lima).

**Secondary:** Familiares que buscan ayuda para un ser querido; profesionales de salud que derivan pacientes.

## Product Purpose

Landing page de conversión ("Persuade") para **María Fernanda Arana — Psicóloga Clínica ACT**. Su único objetivo: que el visitante agende su primera sesión vía WhatsApp (+51 939 855 573).

**Qué hace posible:** Comunicar autoridad clínica (7+ años, +12 países, Magíster ISEP Barcelona, ACT tercera generación) y calidez humana en < 3 segundos, eliminar fricción (botón WhatsApp flotante, nav CTA, hero CTA, mobile sticky CTA), y convertir visitantes en leads calificados.

**Éxito =** Clics a `wa.me/51939855573` / mensajes de WhatsApp recibidos / citas agendadas.

## Positioning

**Mecanismo diferenciador real:** Especialista ACT certificada con práctica internacional real (+12 países) — no "terapeuta online genérico". La combinación de **rigor académico** (Magíster ISEP, diplomados en pareja/sexualidad) + **acceso directo humano** (WhatsApp personal, sin formularios fríos, sin chatbots) es lo que un competidor no puede copiar sin credenciales equivalentes.

## Operating Context

- **Tráfico:** Orgánico (Instagram @pensarsentirhacer.pe, TikTok, Facebook), referidos boca-a-boca, Linktree en bio.
- **Dispositivo:** 70%+ mobile. Thumb-zone CTAs críticos.
- **Ritual de decisión:** Visitante llega → escanea hero (3s) → valida credenciales (social proof bar) → lee "Sobre mí" / ve video → click WhatsApp.
- **Contenido real disponible:** Texto "Sobre mí" redactado por la clienta, 4 fotos profesionales (hero, sobre mí, 3 consultorio), video YouTube intro, testimonios reales (capturas FB), logo PSH.
- **Contenido NO disponible (no inventar):** Precios exactos, dirección exacta de consultorios, paquetes de sesiones, ebooks/resources (deshabilitado v1).

## Capabilities and Constraints

**Confirmado (v1):**
- Single-file `index.html` (CSS/JS inline) → GitHub Pages
- Paleta oficial PSH **inmutable**: creams (`#FFFEEC`, `#FFFDF4`), yellows (`#FDFDC9`, `#FEFFAF`, `#FFFB85`), celestes (`#B0DDFC`, `#89CCFF`, `#6FC1FF`), white `#FFFFFF`, text-dark `#3A4A5A`, title-color `#6FC1FF`
- Tipografías oficiales **inmutables**: League Spartan (títulos), Open Sans (body), Glacial Indifference (subtítulos)
- Estilo orgánico/retro-groovy: border-radius asimétricos, blobs, ondas animadas, cero esquinas duras (0px/4px)
- Zero precios, zero direcciones exactas, zero paquetes públicos
- Ebooks/recursos: **ocultos con comentario `<!-- DESHABILITADO v1 -->`**, no borrados
- Firebase backend: **bloqueado v1** (esperando credenciales clienta)
- Behold.so Instagram feed: **placeholder listo**, pendiente embed code clienta
- WhatsApp: `https://wa.me/51939855573` en 12+ puntos (nav, hero, servicios, cta-final, sticky, float)

**Técnicamente:**
- Lighthouse ≥90 objetivo (Performance/Accessibility/Best Practices/SEO)
- `prefers-reduced-motion` respetado en ondas/carruseles
- `currentColor` en todos los SVGs inline
- Imágenes optimizadas (<300KB c/u) ya referenciadas en HTML

## Brand Commitments

- **Nombre:** Pensar Sentir Hacer (PSH)
- **Logo:** Circular celeste/crema (`logo-psh.png`, `logo-celeste-transparente.png`, `logo-blanco-transparente.png`)
- **Voz:** "Si mejoras tú, mejora el mundo y los que te rodean" — empática, autoritaria sin arrogancia, esperanzadora
- **Identidad visual:** Minimalismo orgánico, retro-groovy suave, movimiento (ondas), espacios respirados
- **Referencia visual vinculante:** `BRANDING_PSH.pdf` (paleta, tipografías, moodboard) + `TERAPIA_PSH` deck (contenido/estructura)

## Evidence on Hand

| Asset | Path | Estado |
|-------|------|--------|
| Texto "Sobre mí" oficial | `CONTEXTO_proyecto_landing-fernanda.md:18-25` | ✅ En HTML |
| Foto hero / sobre mí | `foto-fernanda.png` (199KB) | ✅ En HTML |
| 3 fotos consultorio | `consultorio-1/2/3-optimized.jpg` (103/171/227KB) | ✅ En accordion Presencial |
| Foto manos libreta | `manos-libreta.jpg` (109KB) | ✅ En accordion Online |
| Tarjeta presentación | `tarjeta-presentacion-optimized.jpg` (122KB) | ✅ En sección Redes |
| Logo PSH variants | `logo-psh.png` + transparentes | ✅ Navbar + Footer + Favicon |
| Video intro YouTube | `https://youtu.be/CfACxsC7K-A` | ✅ Embed en Sobre mí |
| Testimonios reales | Capturas FB en `INVENTARIO_CAMBIOS.md` | ⚠️ Estáticos en carrusel; dinámicos requieren Firebase |
| Paleta oficial | `CONTEXTO:28` + `TAREAS_PENDIENTES_FINAL:13-17` | ✅ En `:root` |
| Tipografías oficiales | `CONTEXTO:29` + `TAREAS_PENDIENTES_FINAL:13-17` | ✅ Google Fonts + CSS |

**Ausencias que NO fabricar:** Precios, direcciones exactas, paquetes, ebooks, blogs (admin pendiente Firebase).

## Product Principles

1. **Credibilidad por evidencia, no por adorno** — Cada elemento visual sirve a la confianza: credenciales visibles, fotos reales, video, WhatsApp directo.
2. **Calidez sin ruido** — Paleta suave, movimiento orgánico (ondas), tipografía legible. Nada compite con el CTA.
3. **Mobile-first real** — Thumb-zone CTAs, sticky CTA móvil, WhatsApp float no invasivo, carrusel pausable.
4. **Accesibilidad por defecto** — Contraste WCAG AA, `prefers-reduced-motion`, semantic HTML, labels ARIA.
5. **Extensible sin reescribir** — Ebooks ocultos (no borrados), Firebase placeholder, Behold.so placeholder. v2 = activar, no rehacer.

## Accessibility & Inclusion

- **Contraste actual:** Fallando WCAG AA en 30+ combinaciones (detectado por Impeccable) — **fix prioritario**.
- **Motion:** `prefers-reduced-motion` desactiva ondas Hero + carrusel testimonios.
- **Navegación:** Semantic HTML5, focus-visible states, skip-link recomendado.
- **Idioma:** Español (es-PE) primario; sin i18n en v1.
- **Dispositivos:** 320px–1440px probados; touch targets ≥48px.