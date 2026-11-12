---
name: "90"
description: >-
  Crea una página web completa, interactiva y tematizada sobre cualquier tema,
  videojuego, anime, película o franquicia (por ejemplo, `/90 fnaf 1` o `/90 fnf 1`),
  conservando la arquitectura, las animaciones GSAP + ScrollTrigger, el reproductor
  de música flotante, las tarjetas con inclinación 3D, la galería de cilindro 3D
  interactiva (con giro 360°, arrastre, filtros, vista mosaico y visor lightbox)
  y la tipografía Chakra Petch Bold Italic para titulares, sin letreritos técnicos.
---

# Generador de Página Temática Estilo Archivo Interactivo (`/90`)

Cuando el usuario invoque `/90 <tema>` (por ejemplo `/90 fnf 1`, `/90 fnaf 1`, `/90 halo`, etc.), debes construir una página web completa (`index.html`, `styles.css`, `script.js` y sus recursos/imágenes) totalmente tematizada sobre `<tema>`, replicando la estructura, las animaciones y la galería 3D de la plantilla base incluida en esta skill.

Para consultar el código base exacto de referencia (HTML, CSS, JS y librerías GSAP), utiliza los archivos incluidos en [resources/](./resources/) (`resources/index.html`, `resources/styles.css`, `resources/script.js` y `resources/js/`) y la guía en [references/template-code.md](./references/template-code.md).

---

## 1. Reglas de Diseño y Preferencias Estrictas del Usuario

1. **Cero "letreritos" o etiquetas técnicas (`//`)**:
   - **PROHIBIDO** incluir etiquetas pequeñas encima de los títulos o dentro de las tarjetas como `● TEMA // ARCHIVO`, `01 // SINOPSIS`, `EXPEDIENTE A // ...`, `ID: ...` o insignias flotantes sobre las fotos de personajes (`.tag`, `.section-tag`, `.prota-badge`, `.prota-meta`, `.lore-index`, `.cylinder-hud-top`).
   - Los encabezados de sección (`.section-header`) deben contener directamente el `<h2 class="section-heading">`.
2. **Tipografía obligatoria**:
   - **Titulares (`--font-display`)**: `"Chakra Petch"` en **Bold Italic** (`font-weight: 700; font-style: italic;`) cargada desde Google Fonts (`Chakra+Petch:ital,wght@0,700;1,700`) aplicada en `.section-heading`, `.prota-info h3`, `.lore-card h3` y `.lb-caption h3`.
   - **Cuerpo (`--font-sans`)**: `"Space Grotesk"` (`400;500;600;700`).
   - **Controles, métricas y tabla técnica (`--font-mono`)**: `"JetBrains Mono"` (`400;500;700`).
3. **Paleta de colores adaptada al `<tema>`**:
   - Personaliza las variables CSS en `:root` y `html[data-theme="light"]` (`--bg`, `--surface`, `--surface-elevated`, `--border`, `--border-highlight`, `--accent`, `--accent-text`, `--accent-soft`, `--chroma-red`, `--chroma-cyan`) para reflejar la identidad visual del `<tema>` (por ejemplo: neón urbano/grafiti cian-magenta para *Friday Night Funkin'*, ámbar/rojo cámaras de seguridad nocturnas para *Five Nights at Freddy's 1*, etc.).

---

## 2. Estructura de Secciones y Componentes Obligatorios

La página generada debe incluir todas estas secciones y componentes interactivos:

1. **Fondo Atmosférico Fijo + Barra de Progreso**:
   - `<div class="scroll-progress" id="scrollProgress"></div>` animado con GSAP `ScrollTrigger`.
   - `<div class="space-cosmos" id="spaceCosmos">` con capas de partículas/estrellas en paralaje (`#starsLayer1`, `#starsLayer2`) y un astro/elemento icónico flotante (`#cyberMoonWrap` / `#cyberMoon`) adaptado al tema, más `<div class="grain-overlay">`.
2. **Navbar Flotante (`<header class="nav" id="mainNav">`)**:
   - Logo principal con efecto glitch tricapa (`.brand-logo.cyber-glitch-brand`).
   - Enlaces de navegación (`.nav-link`) hacia `#historia`, `#personajes`, `#mundo`, `#galeria`, `#datos` con resaltado automático de sección activa al hacer scroll.
   - Botón de cambio de tema (`#themeToggle`) entre Modo Claro y Modo Oscuro con persistencia en `localStorage`.
3. **Hero Section (`<section class="hero" id="top">`)**:
   - Imagen de fondo con máscara radial y paralaje (`#heroBgImg`).
   - Logo/título principal con glitch (`.hero-logo-wrap.cyber-glitch-title`), subtítulo con glitch (`.subtitle.cyber-glitch-sub`), párrafo `.lead` y botones `.btn.primary` / `.btn.tertiary`.
   - **Reproductor de música flotante (`.vmp-player#audioWidget`)**: botón de contraer/expandir (`#vmpCollapseBtn`), miniatura del tema (`.vmp-avatar-wrap`), ecualizador animado de 4 barras (`#eqBars`), título y artista del tema musical icónico de la franquicia, retroceso `-10s` (`#vmpPrevBtn`), play/pause (`#vmpPlayBtn`) y barra de progreso interactiva (`#vmpProgressTrack`).
   - **Barra de estadísticas (`.hero-bar#heroBar`)**: 4 `.stat-pill` con contadores numéricos animados mediante `data-counter`.
4. **Sección 1 — Historia (`#historia`)**:
   - Título `<h2 class="section-heading">` en Chakra Petch Bold Italic.
   - `.story-grid` con `.story-visual` a la izquierda (imagen enmarcada `.story-frame`, pie `.story-caption` con `<strong>` y cita destacada `<blockquote class="badge-quote">`) y `.prose` a la derecha con 4 párrafos narrativos (`.story-p`).
5. **Sección 2 — Protagonistas (`#personajes`)**:
   - `.protas-container` con tarjetas `.prota-card.gs-prota-card[data-spotlight]` que reaccionan al cursor con iluminación radial (`--mouse-x`, `--mouse-y`) e inclinación 3D (`rotationX`, `rotationY`) en escritorio.
   - Cada tarjeta incluye `.prota-media` (solo la imagen, sin insignias encima), `.prota-info` con `<h3>` en Chakra Petch Bold Italic, descripción y `.spec-grid` (`<dl>` con 3 atributos clave).
6. **Sección 3 — Lore / Mundo (`#mundo`)**:
   - `.lore-bento` (grid de 3 columnas) con 4 tarjetas `.lore-card.gs-lore-card[data-spotlight]` (la primera y la cuarta con clase `.wide` ocupando 2 columnas).
   - Incluye `.crew-tags` con píldoras de personajes secundarios o facciones.
7. **Sección 4 — Galería Cilindro 3D Interactiva (`#galeria`)**:
   - Cabecera `.gal-header` con `<h2 class="section-heading">`, barra de filtros por categoría (`.filter-bar` con botones `.filter-btn[data-filter]`) y controles del cilindro (`.cylinder-tools`: `#cylPauseBtn` para pausar/reanudar el giro 360° y `#cylViewToggle` para alternar entre **Cilindro 3D** y **Vista Mosaico**).
   - Cámara `.cylinder-chamber#cylinderChamber` con `.cylinder-viewport#cylinderViewport` y `.cylinder-carousel#gallery` (`--n` tarjetas distribuidas en un anillo 3D con `rotateY(calc(var(--i) * var(--ba))) translateZ(...)`).
   - Soporte completo de rotación continua CSS (`@keyframes ry`), giro manual arrastrando horizontalmente con el puntero (`--drag-rot`), filtrado interactivo (`.is-dimmed` / `.is-highlighted`), modo cuadrícula (`.is-grid-mode`) y pie de instrucciones `.cylinder-hud-bottom`.
   - Visor modal `<dialog class="lightbox" id="lightbox">` con contador dinámico (`#lb-counter`), navegación con teclado (`ArrowLeft`, `ArrowRight`, `Escape`), botones anterior/siguiente y transiciones suaves con GSAP.
8. **Sección 5 — Ficha Técnica (`#datos`) y Footer (`.footer`)**:
   - `.data-table#dataTable` con 6 filas `.data-row` (`.data-k` y `.data-v`) detallando título, creador/director, arte/diseño, estudio/desarrollador, música y lanzamiento/reconocimientos.
   - Footer con logo, nota de tributo y enlaces de navegación.

---

## 3. Flujo de Ejecución Paso a Paso

1. **Analizar el `<tema>` solicitado**:
   - Identifica la franquicia, su estética visual, paleta de colores, protagonistas, historia, elementos del mundo/lore, banda sonora icónica y datos de producción.
   - Define dónde crear los archivos y copia las librerías `gsap.min.js`, `ScrollTrigger.min.js` y `Flip.min.js` desde [resources/js/](./resources/js/) hacia la carpeta `js/` del nuevo proyecto.
2. **Preparar recursos visuales y de audio**:
   - Reúne o genera las imágenes temáticas para el hero, historia, protagonistas y la galería 3D, y configura una pista de audio temática funcional en `<audio id="bgMusic">`.
3. **Generar `index.html`, `styles.css` y `script.js`**:
   - Basa el código en [resources/index.html](./resources/index.html), [resources/styles.css](./resources/styles.css) y [resources/script.js](./resources/script.js), manteniendo intactos los selectores, las animaciones GSAP/ScrollTrigger, el cilindro 3D, el lightbox y el reproductor de audio.
   - Verifica que **no exista ningún letrerito tipo `.tag`, `.section-tag`, `.prota-badge`, `.prota-meta`, `.lore-index` ni `.cylinder-hud-top`** y que todos los titulares usen **Chakra Petch Bold Italic**.
