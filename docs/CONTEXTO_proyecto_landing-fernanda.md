# Contexto del proyecto — Landing Page "Pensar Sentir Hacer" (María Fernanda Arana)

## Enlaces clave
- Repo del sitio: https://github.com/elbrujo325/landing-maria-fernanda
- Deploy actual: https://elbrujo325.github.io/landing-maria-fernanda/
- Linktree oficial de la clienta: https://linktr.ee/pensarsentirhacer.pe
- Link de agenda: https://bit.ly/citasPensarSentirHacer
- Video introductorio (YouTube, a embeber en el sitio): https://www.youtube.com/watch?v=CfACxsC7K-A
- Redes sociales (todas como @pensarsentirhacer.pe): Instagram, TikTok, Facebook, WhatsApp

## Archivos fuente recibidos (y qué contiene cada uno)
- `REGLAMENTO_PACIENTES.pdf` — reglas internas para pacientes: pago dentro de 24h post-reserva, tolerancia de 15 min, reprogramación gratuita con 4h de anticipación (si no, penalidad S/45 Perú o $15 extranjero), evaluación de casos a criterio de la psicóloga. Uso interno/operativo, no necesariamente para mostrar tal cual en el landing público.
- `TERAPIA_PSH-_PERU__________.pdf` (17 páginas, deck de Canva) — contiene: presentación de Fernanda, beneficios de la terapia (lista de 10), detalle de servicios (online y presencial, individual y pareja), proceso terapéutico paso a paso, tabla de precios por paquete de sesiones, testimonios de pacientes (capturas de Facebook), stats (+12 países, +7 años, 5★). **Contiene precios y referencia a sedes — no usar esas partes en el sitio público** (decisión del cliente: no mostrar precios ni dirección exacta).
- `BRANDING_PSH.pdf` — paleta de colores oficial, tipografías, moodboard de estilo (minimalismo orgánico / retro moderno groovy), plantillas de referencia para redes sociales (portadas de reels, carruseles, historias) — más orientado a contenido de Instagram que al landing, pero define el lenguaje visual de marca.
- `drive-download-...zip` — 12 archivos: fotos personales/profesionales de Fernanda (`IMG_9006.JPG`, `IMG_9550.JPG`, `IMG_1171.HEIC`, `IMG_1417.HEIC`, `IMG_6650.HEIC`, `IMG_5525.HEIC`, `IMG_4740.JPG`, `482E95C7-....jpg`), su foto de perfil con fondo transparente (`IMG_7030-removebg-preview (1).png`), y variantes del logo circular PSH (`Copia de LOGOS PSH.png`, `LOGOS PSH (2).png`, `LOGOS PSH (1).pdf`).
- `1784673506772_image.png` — captura de la presentación/historia de Instagram de Fernanda con el texto real de "Sobre mí" ya redactado por ella.

## Texto oficial "Sobre mí" (redactado por la clienta)
> ¡Hola! Soy María Fernanda Arana. Licenciada en Psicología Clínica CPP 46797, especialista en Terapia Cognitivo Conductual en casos de ansiedad, depresión, relaciones familiares y de pareja con Diplomado en Terapia de Pareja y Sexualidad. Magister en Terapia de Tercera Generación y Bienestar Emocional en ISEP, Barcelona.
>
> Trabajo como psicóloga y psicoterapeuta con experiencia de atención +7 años, llegando a +12 países para mejorar su salud mental, emocional y relaciones.
>
> "Si mejoras tú, mejora el mundo y los que te rodean"
>
> @pensarsentirhacer.pe

## Branding
- Paleta vainilla: `#FDFDC9`, `#FEFFAF`, `#FFFB85` (amarillos) · `#B0DDFC`, `#89CCFF`, `#6FC1FF` (celestes) · `#FFFEEC`, `#FFFDF4` (cremas)
- Tipografías: título **League Spartan**, texto largo **Open Sans**, subtítulo **Glacial Indifference**
- Estilo: minimalista orgánico, retro moderno "groovy", líneas curvas, sin bordes rectos duros

## Decisiones de alcance (v1 vs v2)
**V1 (ahora):**
- Cambios de copy/texto (créditos, ACT en vez de TCC, sobre mí, +12 países, FAQ adolescentes)
- Quitar precios y "cómo funciona el proceso"; ebooks solo se oculta (no se borra)
- Desplegable de servicios sin precio ni dirección
- Sección de redes ampliada + feed de Instagram embebido vía Behold.so (mismo método usado en el proyecto Luxto)
- Video de YouTube embebido
- Mini-backend en Firebase: testimonios públicos con estrellas (moderados por Fernanda) + modo admin para que ella redacte y publique blogs

**V2 (después):**
- Perfiles de cliente / cuentas de usuario para pacientes
- Sistema de pagos automático, reservas de fecha y generación de link de sesión

## Stack técnico
- Frontend: HTML/CSS/JS estático, hosteado en GitHub Pages (sin cambios)
- Backend: Firebase (Firestore + Auth + Storage), bajo cuenta de Google propiedad de la clienta, región `southamerica-east1`
- Feed social: Behold.so conectado a @pensarsentirhacer.pe (mismo patrón que en el portal Luz de Cristo / Luxto)

## Reglas duras (no negociables)
- Nunca mostrar precios de sesiones/paquetes en el sitio público
- Nunca mostrar dirección exacta de los consultorios
- Mantener paleta y tipografías de marca sin alteraciones no solicitadas
- Preservar estructura existente del HTML — cambios quirúrgicos, no reescrituras completas
