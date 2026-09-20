# Maquetado — Fase 1

Maquetado estático en HTML + SCSS de la interfaz de chat (ver [`../PLAN.md`](../PLAN.md)). Todavía no hay Angular: esto es lo que se valida en equipo antes de pasar a la Fase 2.

## Cómo verlo

```bash
npm install
npm run build:css
```

Esto compila `scss/main.scss` → `css/main.css`. Luego abre `index.html` en el navegador (o sirve la carpeta con cualquier servidor estático, por ejemplo `npx serve`).

Mientras edites estilos, deja corriendo:

```bash
npm run watch:css
```

y solo recarga la página cada vez que guardes un archivo `.scss`.

## Estructura

```
maquetado/
├── index.html
├── scss/
│   ├── _variables.scss           # tokens: color, tipografía, espaciado, breakpoints
│   ├── _mixins.scss              # mixins de los 5 breakpoints
│   ├── _base.scss                # reset + estilos globales
│   ├── _layout.scss              # app shell (columnas según dispositivo)
│   ├── _sidebar.scss             # lista de chats
│   ├── _chat-header.scss         # header del chat activo
│   ├── _messages.scss            # hilo de mensajes / burbujas
│   ├── _message-input.scss       # barra de entrada
│   ├── _chat-info.scss           # panel de info de contacto (solo TV)
│   ├── _responsive-overrides.scss # overrides entre componentes (se importa AL FINAL, ver comentario dentro)
│   └── main.scss                 # punto de entrada, compila a css/main.css
└── css/main.css                  # generado, no editar a mano
```

## Quién edita qué (equipo de 4)

| Persona | Archivo(s) SCSS | Bloque en `index.html` |
|---|---|---|
| 1 (integrador/a) | `_layout.scss`, `_chat-info.scss`, `_responsive-overrides.scss` | `<div class="app">`, `<aside class="chat-info">` |
| 2 | `_sidebar.scss` | `<aside class="sidebar">` |
| 3 | `_chat-header.scss`, `_message-input.scss` | `<header class="chat__header">`, `<form class="message-input">` |
| 4 | `_messages.scss` | `<div class="chat__messages">` |

El `index.html` ya está completo con contenido de ejemplo y comentarios (`<!-- PERSONA N — ... -->`) marcando cada bloque, para que cada quien lo use de referencia y no haya que "repartir" el archivo físicamente: todos pueden editar su sección con git (una rama por persona + PR).

**Regla importante de CSS:** si necesitas cambiar cómo se ve el componente de otra persona según el dispositivo (ej. "en reloj, ocultar el botón X del header"), ese ajuste va en `_responsive-overrides.scss`, no en el archivo de esa persona. Está explicado (el porqué) en un comentario dentro de ese archivo — es un bug real de cascada CSS en el que ya caímos al construir este maquetado.

## Breakpoints

Ver la tabla completa en [`../PLAN.md`](../PLAN.md). Resumen:

| Dispositivo | Ancho | Mixin |
|---|---|---|
| ⌚ Reloj | ≤ 260px | `bp-watch-only` |
| 📱 Teléfono | 261–599px | (base, sin mixin) |
| 📱 Tablet | ≥ 600px | `bp-tablet-up` |
| 🚗 Auto | ≥ 1024px | `bp-car-up` |
| 📺 TV | ≥ 1281px | `bp-tv-up` |

## Principios de diseño que se siguieron

- **Una sola familia tipográfica** (Plus Jakarta Sans) en toda la app — menos decisiones, más consistencia.
- **Paleta corta y con roles claros**: azul pizarra como color principal (mensajes enviados, acentos), coral solo para el badge de no leídos — nada de color "porque sí".
- **Firma visual simple y reutilizable en Angular**: avatares de iniciales con color determinístico por contacto (mapa `$avatar-colors` en `_variables.scss`), en vez de depender de imágenes/assets que no tenemos.
- **Casi sin animación**: solo transiciones cortas (120ms) en hover/foco. Nada de animaciones de entrada ni efectos.
- **El único cambio estructural real entre dispositivos es cuántas columnas se ven** (1 en reloj/teléfono, 2 en tablet/auto, 3 en TV) — todo lo demás son ajustes de tamaño/espaciado dentro de esa estructura. Eso mantiene el CSS entendible para gente nueva en esto.
- **Accesibilidad mínima no negociable**: HTML semántico, `aria-label` en botones de solo ícono, foco visible (`:focus-visible`) siempre — importante para TV, donde se navega con control remoto.

## Checklist de validación (antes de pasar a Fase 2)

- [x] Se ve bien en los 5 breakpoints (reloj, teléfono, tablet, auto, TV) — probado en DevTools
- [x] HTML semántico
- [x] Sin errores de consola
- [ ] Revisado por las 4 personas del equipo
- [ ] Probado con contenido "real" adicional (nombres muy largos, chat sin mensajes, chat con muchísimos mensajes)
