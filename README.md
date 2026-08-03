# Landing María Fernanda — Psicología Clínica ACT

Sitio web profesional para **María Fernanda Arana**, psicóloga clínica especialista en Terapia de Aceptación y Compromiso (ACT). Desarrollado como una *single-page application* moderna con panel de administración para gestión de blog y testimonios.

---

## 🎯 Descripción General

**Landing María Fernanda** es una página de aterrizaje (landing page) diseñada para convertir visitantes en pacientes. Presenta servicios de terapia presencial en Lima (San Isidro, Surco) y online a nivel mundial, con un enfoque en evidencia científica y narrativa cercana.

- **Target**: Personas buscando terapia ACT para ansiedad, depresión, relaciones, propósito de vida
- **Conversión principal**: Botón WhatsApp flotante + CTA sticky móvil + formulario de agendamiento
- **Diferenciador**: Diseño *Luxto-style* (footer 3-columnas, franja de cita, textura de ruido SVG), animaciones sutiles, performance optimizado

---

## 🛠 Stack Tecnológico

| Capa | Tecnología | Versión / Nota |
|------|------------|----------------|
| **Frontend** | HTML5 semántico, CSS3 (Custom Properties), Vanilla JS (ESM) | Sin frameworks — cero dependencias runtime |
| **Estilos** | CSS Variables (design tokens), Flexbox/Grid, Media Queries | Breakpoints: 768px (mobile), 1024px (tablet), 1440px (desktop) |
| **Backend / BaaS** | **Firebase** — Firestore (DB), Auth (Admin), Hosting | Plan Spark (gratuito) |
| **Editor** | **Quill.js** v2 (CDN) — Rich text para blog posts | Módulos: toolbar, clipboard, history, image-resize |
| **Imágenes** | WebP + srcset (7 densidades), square-crop automático | Original: `foto-fernanda.png` (377×661) → avatares optimizados |
| **Despliegue** | `firebase deploy` → `https://landing-maria-fernanda.web.app` | SSH remote: `git@github.com:elbrujo325/landing-maria-fernanda.git` |
| **Lint/Format** | Prettier (HTML/CSS/JS), ESLint (opcional) | Config en `.prettierrc` |

---

## 📁 Estructura del Proyecto

```
landing-maria-fernanda/
├── public/                          # Código fuente servido (Firebase Hosting)
│   ├── index.html                   # Landing principal (referencia de diseño)
│   ├── blog.html                    # Listado de posts con filtros + búsqueda
│   ├── blog-post.html               # Vista detalle de post + relacionados + CTA
│   ├── admin.html                   # Dashboard admin (login, CRUD posts/testimonios)
│   ├── admin-editor.html            # Editor Quill para crear/editar posts
│   ├── assets/
│   │   ├── images/                  # Fotos optimizadas (WebP srcset + PNG fallback)
│   │   │   ├── foto-fernanda.png            # Original 377×661 (hero/perfil index.html)
│   │   │   ├── foto-fernanda-square.png     # Square crop 1:1 (avatar blog/blog-post)
│   │   │   └── foto-fernanda-{72,108,144,216,260,400,520,800}.webp
│   │   └── logos/
│   │       ├── logo-blanco-transparente.png
│   │       ├── logo-celeste-transparente.png
│   │       └── logo-psh.png
│   └── src/js/
│       └── firebase-config.js       # Configuración Firebase (exporta db, auth)
├── firebase.json                    # Config Hosting + rewrites SPA
├── firestore.indexes.json           # Índices compuestos requeridos
├── docs/                            # Documentación interna
│   ├── CONTEXTO_proyecto_landing-fernanda.md
│   ├── PLAN_TAREAS.md
│   ├── BACKEND_TESTIMONIOS_BLOG.md
│   ├── INVENTARIO_CAMBIOS.md
│   ├── TAREAS_PENDIENTES_FINAL.md
│   ├── PRODUCT.md
│   └── Paginas web de referencia.txt
└── README.md                        # Este archivo
```

---

## 🎨 Sistema de Diseño (Design Tokens)

Variables CSS definidas en `:root` (ver `index.html:1-80`):

```css
/* Colores principales */
--celeste-deep: #11698e;      /* Primary brand */
--celeste-mid:  #3aa8c9;
--celeste-light: #6fc1ff;     /* Accent / hover */
--cream:        #fff8e7;      /* Background warm */
--cream-light:  #fffef0;
--yellow-mid:   #ffe066;      /* Highlights */
--white:        #ffffff;
--text-dark:    #1a1a2e;
--text-muted:   #6b7280;
--card-border:  rgba(17,105,142,0.12);
--card-bg:      #ffffff;

/* Espaciado (escala 4px) */
--space-xs: 4px;  --space-sm: 8px;  --space-md: 16px;
--space-lg: 24px; --space-xl: 32px; --space-2xl: 48px;
--space-3xl: 64px; --space-4xl: 96px;

/* Tipografía */
--font-heading: 'League Spartan', sans-serif;  /* Títulos */
--font-body:    'Open Sans', sans-serif;       /* Texto */

/* Radii & Sombras */
--radius-sm: 8px;  --radius-md: 12px; --radius-lg: 16px;
--radius-xl: 24px; --radius-full: 9999px;
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
--shadow-md: 0 4px 12px rgba(17,105,142,0.10);
--shadow-lg: 0 12px 32px rgba(17,105,142,0.15);

/* Colores sociales (footer) */
--color-wa: #25d366;   --color-ig: #e1306c;
--color-tt: #000000;   --color-fb: #1877f2;
```

---

## 📱 Responsive Breakpoints

| Breakpoint | Dispositivo | Cambios Clave |
|------------|-------------|---------------|
| **≥1440px** | Desktop Large | Container max-width 1280px, hero 2-col, footer 3-col (1.5/1/1fr) |
| **1024–1439px** | Desktop / Tablet Landscape | Hero 2-col, footer 3-col |
| **768–1023px** | Tablet Portrait | **Navbar → Hamburger absolute dropdown**, footer 2-col (brand 100% + nav/contact 50%), hero 1-col |
| **<768px** | Mobile | Footer 1-col, hero image arriba, CTA sticky visible, WhatsApp float colisiona con footer (push up) |

**Navbar móvil (768px)**: Dropdown absoluto bajo la nav (`top: 100%`, `left: 0`, `right: 0`), z-index 1000, animación `slideDown 0.3s`. Excluye `.has-dropdown > a` del handler "close on link click".

---

## 🧩 Componentes Principales

### 1. Navbar (`<nav id="navbar">`)
- **Desktop**: Links horizontales + dropdown "Servicios" (hover/focus)
- **Mobile (≤768px)**: Hamburger → dropdown absoluto con todos los links
- **Scroll effect**: `.scrolled` añade backdrop-blur + sombra
- **Active link**: Resaltado por scroll (IntersectionObserver)

### 2. Hero
- Layout 2-col (texto + imagen) en desktop, 1-col móvil
- Foto original `foto-fernanda.png` (377×661) — **no optimizada** por decisión de cliente
- Wave background animado (SVG)
- Trust indicators: avatares + contador "+150 pacientes"

### 3. Footer — *Luxto Style* (Referencia: `index.html:5558-5650`)
```
┌─────────────────────────────────────────────────────────────┐
│  FRANJA CITA CENTRADA: "Si mejoras tú, mejora el mundo..."  │
├─────────────────────────────────────────────────────────────┤
│  GRID 3 COL:  Brand (1.5fr)  │  Nav (1fr)  │  Contacto (1fr) │
│  • Logo círculo + nombre      │  7 links    │  Ubicación      │
│  • Tagline "PSICOLOGÍA ACT"   │             │  WhatsApp       │
│  • Descripción + pill         │             │  Email          │
│                               │             │  Horario        │
│                               │             │  4 Social btns  │
├─────────────────────────────────────────────────────────────┤
│  BOTTOM BAR: Copyright + Legal links (Privacidad, Términos) │
└─────────────────────────────────────────────────────────────┘
```
- **Noise texture**: SVG filter `feTurbulence` en `.footer-background::before`
- **Social buttons**: Brand colors en hover (`--color-wa`, `--color-ig`, `--color-tt`, `--color-fb`)
- **Responsive**: 1023px → 2-col (brand 100%), 767px → 1-col

### 4. WhatsApp Float (`.whatsapp-float`)
- Fixed bottom-right, `z-index: 100`
- **Mobile collision detection**: Si `floatRect.bottom >= footerRect.top - 16` → `bottom = footerHeight + 24px`
- Pulse animation + tooltip en hover

### 5. Blog System
- **Firestore Collection**: `blogPosts`
- **Query público**: `where('publicado', '==', true).orderBy('fecha', 'desc')`
- **Índice compuesto requerido**: `blogPosts` → `publicado Asc, fecha Desc` (`firestore.indexes.json`)
- **blog.html**: Grid responsivo, filtros por categoría, búsqueda en tiempo real, paginación infinita
- **blog-post.html**: Reading progress bar, share buttons, related posts (3), CTA final

### 6. Admin Panel (`admin.html` + `admin-editor.html`)
- **Auth**: Email/password (Firebase Auth) — solo cuentas autorizadas
- **CRUD Posts**: Crear, editar, publicar/despublicar, eliminar
- **CRUD Testimonios**: Gestión de testimonios con avatar
- **Editor**: Quill.js v2 con toolbar completa, image resize, clipboard cleanup
- **Seguridad**: Reglas Firestore separan `public` (read published) vs `admin` (read/write all)

---

## 🔥 Firebase — Configuración

### `firebase.json`
```json
{
  "hosting": {
    "public": "public",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"],
    "rewrites": [{ "source": "**", "destination": "/index.html" }]
  },
  "firestore": { "rules": "firestore.rules", "indexes": "firestore.indexes.json" }
}
```

### `firestore.indexes.json` (Índices compuestos)
```json
{
  "indexes": [
    {
      "collectionGroup": "blogPosts",
      "queryScope": "COLLECTION",
      "fields": [
        { "fieldPath": "publicado", "order": "ASCENDING" },
        { "fieldPath": "fecha", "order": "DESCENDING" }
      ]
    },
    {
      "collectionGroup": "testimonios",
      "queryScope": "COLLECTION",
      "fields": [
        { "fieldPath": "publicado", "order": "ASCENDING" },
        { "fieldPath": "orden", "order": "ASCENDING" }
      ]
    }
  ]
}
```

### Reglas Firestore (`firestore.rules` — resumidas)
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Blog posts: público lee solo publicados; admin lee/escribe todo
    match /blogPosts/{docId} {
      allow read: if resource.data.publicado == true || request.auth != null;
      allow write: if request.auth != null && request.auth.token.admin == true;
    }
    // Testimonios: similar
    match /testimonios/{docId} {
      allow read: if resource.data.publicado == true || request.auth != null;
      allow write: if request.auth != null && request.auth.token.admin == true;
    }
  }
}
```

---

## 🖼 Optimización de Imágenes

### Avatar María Fernanda (Blog / Blog-Post)
- **Source**: `foto-fernanda.png` (377×661, portrait)
- **Crop**: Square 1:1 desde **top-center** (cara centrada) → `foto-fernanda-square.png`
- **WebP densities**: 72, 108, 144, 216, 260, 400, 520, 800px
- **HTML** (`blog.html`, `blog-post.html`):
  ```html
  <img src="assets/images/foto-fernanda-square.png"
       srcset="
         assets/images/foto-fernanda-72.webp   72w,
         assets/images/foto-fernanda-108.webp  108w,
         assets/images/foto-fernanda-144.webp  144w,
         assets/images/foto-fernanda-216.webp  216w,
         assets/images/foto-fernanda-260.webp  260w,
         assets/images/foto-fernanda-400.webp  400w,
         assets/images/foto-fernanda-520.webp  520w,
         assets/images/foto-fernanda-800.webp  800w
       "
       sizes="(max-width: 767px) 60px, (max-width: 1023px) 72px, 80px"
       alt="María Fernanda Arana"
       loading="lazy"
       style="image-rendering: -webkit-optimize-contrast; image-rendering: crisp-edges;">
  ```
- **CSS**: `image-rendering` para nitidez en avatares pequeños (60–80px)

### Hero / Perfil (index.html) — **NO optimizadas**
- Usan `foto-fernanda.png` original a resolución completa
- Decisión de cliente: máxima calidad en zonas destacadas

---

## 🚀 Despliegue

### Prerrequisitos
```bash
npm install -g firebase-tools
firebase login
```

### Desarrollo local
```bash
cd landing-maria-fernanda
firebase serve --only hosting  # http://localhost:5000
```

### Deploy producción
```bash
firebase deploy --project landing-maria-fernanda
# → https://landing-maria-fernanda.web.app
```

### Git workflow
```bash
git add .
git commit -m "feat: descripción del cambio"
git push origin main  # SSH: git@github.com:elbrujo325/landing-maria-fernanda.git
```

---

## 🔐 Acceso Admin

1. Ir a `/admin.html`
2. Login con cuenta autorizada (Firebase Auth → Authentication → Users)
3. **Custom claim `admin: true`** requerido para writes en Firestore:
   ```bash
   # Via Firebase Admin SDK (Node)
   admin.auth().setCustomUserClaims(uid, { admin: true })
   ```

---

## 📋 Checklist de Calidad (Pre-deploy)

- [ ] **HTML válido**: `npx html-validate public/*.html`
- [ ] **CSS sin errores**: `npx stylelint public/**/*.html` (inline styles)
- [ ] **JS sin errores consola**: Navegar todas las páginas en Chrome DevTools
- [ ] **Responsive**: Test en 320px, 768px, 1024px, 1440px (Chrome Device Toolbar)
- [ ] **Firestore indexes**: Verificar en Console → Firestore → Indexes (verdes = listos)
- [ ] **Imágenes WebP**: Verificar `Network` tab → `img` → `webp` servido
- [ ] **Accesibilidad**: `axe DevTools` — 0 critical/serious
- [ ] **Performance**: Lighthouse ≥90 (Performance, Accessibility, Best Practices, SEO)

---

## 🐛 Known Issues / TODO

| Issue | Archivo | Prioridad |
|-------|---------|-----------|
| Blog posts no cargan sin índice compuesto | `blog.html` / Firebase Console | 🔴 Crítico — crear índice en Console |
| Admin Quill image upload → Firebase Storage | `admin-editor.html` | 🟡 Medio — actualmente base64/URL externo |
| SEO meta tags dinámicos por post | `blog-post.html` | 🟡 Medio |
| PWA manifest + service worker | `public/` | 🟢 Bajo |
| Tests E2E (Playwright/Cypress) | — | 🟢 Bajo |

---

## 📄 Licencia

Proyecto privado — Todos los derechos reservados a **María Fernanda Arana** y **Henry Paolo Alfaro Sotil** (desarrollador).

---

## 👨‍💻 Autor

**Henry Paolo Alfaro Sotil**  
Full-stack Developer · Firebase · Web Performance · UX Engineering . Physics . Data Science

- GitHub: [@elbrujo325](https://github.com/elbrujo325)
- LinkedIn: [linkedin.com/in/henry-paolo-alfaro-sotil](https://linkedin.com/in/henry-paolo-alfaro-sotil)
- Email: paolo.alfaro.sotil@gmail.com

> *Desarrollado con enfoque en performance, accesibilidad y mantenibilidad. Código limpio, documentado y listo para escalar.*
