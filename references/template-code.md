# Plantilla Base de Código para la Skill `/90`

Cuando ejecutes `/90 <tema>`, utiliza como base directa los archivos incluidos dentro de la carpeta `resources/` de esta misma skill:

- **HTML Base**: [../resources/index.html](../resources/index.html)
- **CSS Base (con animaciones glitch, cilindro 3D, reproductor, modo claro/oscuro y Chakra Petch Bold Italic)**: [../resources/styles.css](../resources/styles.css)
- **JS Base (GSAP, ScrollTrigger, inclinación 3D, cilindro 3D arrastrable, filtros, lightbox, tema y audio)**: [../resources/script.js](../resources/script.js)
- **Librerías GSAP**: [../resources/js/gsap.min.js](../resources/js/gsap.min.js), [../resources/js/ScrollTrigger.min.js](../resources/js/ScrollTrigger.min.js), [../resources/js/Flip.min.js](../resources/js/Flip.min.js)

## Checklist de Adaptación por Tema

1. **Variables CSS (`:root` y `html[data-theme="light"]` en `styles.css`)**:
   ```css
   :root {
     --bg: /* fondo oscuro principal del tema */;
     --surface: /* color de tarjetas */;
     --surface-elevated: /* superficie elevada */;
     --border: /* borde sutil */;
     --border-highlight: /* color acento principal en bordes */;
     --text: #f4f3f8;
     --text-secondary: #a8a4b8;
     --text-muted: #76728a;
     --accent: /* color acento vibrante del tema */;
     --accent-text: /* color acento legible */;
     --accent-soft: /* rgba del acento al 0.14 */;
     --chroma-red: /* color aberración cromática 1 */;
     --chroma-cyan: /* color aberración cromática 2 */;
     --font-display: "Chakra Petch", system-ui, -apple-system, sans-serif;
     --font-sans: "Space Grotesk", system-ui, -apple-system, sans-serif;
     --font-mono: "JetBrains Mono", ui-monospace, monospace;
   }
   ```

2. **Titulares en Chakra Petch Bold Italic**:
   - Asegúrate de incluir en el `<head>`:
     ```html
     <link href="https://fonts.googleapis.com/css2?family=Chakra+Petch:ital,wght@0,700;1,700&family=JetBrains+Mono:wght@400;500;700&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
     ```
   - Y que `.section-heading`, `.prota-info h3`, `.lore-card h3` y `.lb-caption h3` tengan:
     ```css
     font-family: var(--font-display);
     font-weight: 700;
     font-style: italic;
     ```

3. **Sin letreritos técnicos (`//`)**:
   - No incluyas `<div class="tag">`, `<span class="section-tag">`, `<span class="prota-badge">`, `<div class="prota-meta">`, `<span class="lore-index">` ni `<div class="cylinder-hud-top">`.

4. **Galería Cilindro 3D (`#galeria`)**:
   - Ajusta `--n` en `.cylinder-carousel` al número total de imágenes de la galería (`style="--n: 18; --w: 225px; --ba: calc(1turn / var(--n)); --anim-dur: 40s;"`) y asigna `style="--i: 0;"` hasta `--i: N-1` en cada `.gal-item`.
   - Conserva intacta la lógica en `script.js` para filtrado por `data-cat`, pausa de rotación (`#cylPauseBtn`), cambio a vista mosaico (`#cylViewToggle`), arrastre con puntero (`pointerdown` / `pointermove` / `pointerup`) y apertura en el `<dialog class="lightbox" id="lightbox">`.
