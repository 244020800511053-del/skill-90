# Skill `/90` — Generador de Páginas Web Temáticas con Galería 3D y GSAP

Skill para **Antigravity** que permite generar páginas web completas, interactivas y tematizadas sobre cualquier videojuego, anime, serie o franquicia escribiendo en el chat:

```text
/90 <tema>
```

Por ejemplo:
- `/90 fnf 1`
- `/90 fnaf 1`
- `/90 halo`

## Características principales

- **Animaciones GSAP + ScrollTrigger**: Intro animada, paralaje multicapa de fondo, contadores numéricos, revelación por scroll e inclinación 3D con spotlight en tarjetas.
- **Galería Cilindro 3D Interactiva**: Carrusel cilíndrico 360° con rotación continua, giro manual por arrastre horizontal, filtros por categoría, interruptor a Vista Mosaico y visor modal Lightbox con soporte de teclado.
- **Reproductor de Audio Flotante**: Widget colapsable con avatar, ecualizador animado, retroceso `-10s`, play/pause y barra de progreso.
- **Modo Oscuro / Claro**: Selector de tema con persistencia en `localStorage`.
- **Tipografía y Diseño Limpio**: Titulares en **Chakra Petch Bold Italic** (`700 italic`), sin etiquetas ni subtítulos técnicos (`//`) encima de los encabezados.

## Estructura del Repositorio

```text
skill-90/
├── SKILL.md                      # Instrucciones principales de la skill (/90)
├── README.md                     # Documentación del repositorio
├── references/
│   └── template-code.md          # Guía de adaptación de la plantilla
└── resources/                    # Plantilla base funcional y librerías GSAP
    ├── index.html
    ├── styles.css
    ├── script.js
    └── js/
        ├── gsap.min.js
        ├── ScrollTrigger.min.js
        └── Flip.min.js
```

## Instalación

Copia o clona esta carpeta dentro de `~/.gemini/config/skills/90` (global) o `.agents/skills/90` (en tu proyecto):

```bash
git clone https://github.com/244020800511053-del/skill-90.git ~/.gemini/config/skills/90
```
