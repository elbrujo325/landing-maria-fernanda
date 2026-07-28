# Backend de Testimonios + Blog — Landing "Pensar Sentir Hacer"

**Estado:** Planificado, pendiente de acceso al proyecto Firebase de la clienta
**Referencia:** Complementa `TAREAS_PENDIENTES_FINAL.md` Fase 7 (ver nota al final)
**Alcance:** v1 — testimonios públicos moderados + panel de blog para la clienta

---

## 1. Objetivo

La clienta (María Fernanda) no sabe programar y no debe tocar código nunca. Necesita:
1. Que cualquier visitante (incluso anónimo) pueda dejar un testimonio con estrellas, que ella modera antes de que aparezca en el carrusel público.
2. Un "modo usuario" propio donde ella redacte y publique artículos de blog — texto, imágenes, tipo de letra — sin código.

## 2. Stack — costo $0, sin tarjeta

| Función | Herramienta | Costo | Requiere tarjeta |
|---|---|---|---|
| Datos (testimonios, posts) | Firestore (Firebase, plan Spark) | $0 | No |
| Login admin de la clienta | Firebase Authentication | $0 | No |
| Imágenes (blog, testimonios) | Cloudinary (plan Free), cuenta de la clienta | $0 | No |
| Hosting del sitio | GitHub Pages | $0 | Ya lo tienen |

**Importante:** NO se usa Firebase Storage. Desde el 3 de febrero de 2026 Firebase Storage exige el plan Blaze (tarjeta vinculada) incluso dentro de la cuota gratis. Como la clienta no quiere pagar ni vincular tarjeta, las imágenes van a Cloudinary (cuenta separada, gratis, sin tarjeta, creada por nosotros — no requiere nada de la clienta).

## 3. Estructura de archivos (5 HTML en total)

| Archivo | Acceso | Contenido |
|---|---|---|
| `index.html` | Público (ya existe) | Se agrega un link "Blog" en el nav, sin más cambios de este proyecto |
| `blog.html` | Público, nuevo | Listado de artículos con chips de filtro por categoría |
| `blog-post.html` | Público, nuevo | Plantilla única que muestra un artículo (`?id=...`), reutilizable para todos los posts |
| `admin.html` | Privado, nuevo | Login + panel: testimonios pendientes (Aprobar/Rechazar) + lista "Mis posts" (Nuevo/Editar) |
| `admin-editor.html` | Privado, nuevo | El "modo Word": redactar, elegir plantilla, insertar imágenes, Guardar borrador / Publicar |

`admin.html` y `admin-editor.html` validan la sesión de forma independiente (si alguien entra directo por URL sin login, se le rebota igual).

## 4. Esquema de datos (Firestore)

**Colección `testimonios`**
```
nombre: string | null      (null si es anónimo)
anonimo: boolean
texto: string
estrellas: number (1-5)
fecha: timestamp
aprobado: boolean           (default: false)
```

**Colección `blogPosts`**
```
titulo: string
contenidoHtml: string        (generado por el editor Quill)
categoria: string            (una de la lista fija, ver sección 6)
imagenPortadaUrl: string     (URL de Cloudinary)
plantilla: string            ("estandar" | "imagen-destacada" | "galeria")
fecha: timestamp
publicado: boolean           (default: false, se activa al dar "Publicar")
```

## 5. Reglas de seguridad (Firestore rules)

- **Público:** puede leer `testimonios` donde `aprobado == true` y `blogPosts` donde `publicado == true`. Puede *crear* un testimonio nuevo (nunca editar ni borrar, nunca leer los pendientes).
- **Admin (solo el correo de la clienta):** lectura y escritura total sobre ambas colecciones.

## 6. Blog — el "modo Word" con barandas de marca

Editor: **Quill.js** (gratis, vía CDN, liviano).

- **Tipo de letra:** el selector solo ofrece las 3 fuentes oficiales de marca (League Spartan / Open Sans / Glacial Indifference), con nombres simples ("Título", "Texto normal", "Destacado"). Ella elige, pero no puede romper la identidad visual.
- **Imágenes:** botón "Insertar imagen" en el punto del texto donde está el cursor → sube a Cloudinary → se inserta ahí, tamaño responsive automático.
- **Categoría:** desplegable de opciones fijas (no texto libre, para evitar duplicados por typo). Propuesta inicial, a confirmar con la clienta:
  - Ansiedad
  - Depresión
  - Relaciones de pareja
  - Relaciones familiares
  - Autoestima
  - Otros
- **Plantillas predeterminadas** (elige una al crear un post nuevo):
  1. Estándar — imagen de portada arriba + título + texto corrido
  2. Imagen destacada — imagen grande a ancho completo + título superpuesto + texto abajo
  3. Galería + texto — texto con 2-3 imágenes intercaladas
- **Vista previa** antes de publicar: botón que muestra el post exactamente como se verá en vivo.

## 7. Qué necesitamos de la clienta (checklist)

1. Que cree un proyecto en Firebase desde su cuenta de Google del negocio (console.firebase.google.com) y agregue a Paolo como **Editor u Owner**. Plan Spark (gratis) alcanza — no hace falta activar Blaze.
2. El **correo exacto** que va a usar para loguearse al panel admin (queda fijo en las reglas de seguridad).
3. Confirmar o ajustar la lista de categorías del blog (sección 6).
4. Confirmar que quiere moderar cada testimonio antes de publicarlo (recomendado, dado que se permite anónimo).
5. Que cree una cuenta gratis en Cloudinary (con su Google, sin tarjeta) — misma lógica que Firebase: las imágenes de su blog son datos de su negocio, deben quedar en una cuenta suya. Después de crearla, solo necesita compartir dos datos de texto (no contraseña): el **cloud name** y el **nombre del upload preset** que se configura una sola vez.

## 8. Fuera de alcance en v1 (queda documentado para v2)

No se construye ahora, pero se deja registrado para no perder el contexto cuando se retome:

- Cuenta/perfil propio por paciente: récord de asistencia, fecha de próxima terapia, contenido en PDF, link de Meet generado automáticamente.
- Flujo completo de reservas: paciente ve disponibilidad → clienta valida el caso → se genera fecha + link, todo después de un pago adjunto.
- Definir más adelante: pasarela de pago (Perú: Culqi, Niubiz, MercadoPago) y automatización de Google Calendar/Meet.
- Contexto de volumen para dimensionar v2: la clienta atiende ~245 pacientes al año, con ~13 activos por semana (salen 5, entran 6-7) — volumen bajo, sin problema de escala para Firebase.

---

**Nota sobre `TAREAS_PENDIENTES_FINAL.md`:** la Fase 7 de ese archivo queda como referencia rápida del checklist original; este documento la reemplaza en nivel de detalle. Sugerido: en la Fase 7, cambiar la línea de la nota final de "Firebase (QUEDA PENDIENTE credenciales)" a "Ver detalle completo en `BACKEND_TESTIMONIOS_BLOG.md`", y quitar cualquier mención a Blaze/Storage ya que se reemplazó por Cloudinary.
