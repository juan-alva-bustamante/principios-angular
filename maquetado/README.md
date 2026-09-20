# Maquetado — Fase 1

Maquetado estático en HTML + SCSS de la interfaz de chat (ver [`../PLAN.md`](../PLAN.md)). Todavía no hay Angular: esto es lo que se valida antes de pasar a la Fase 2.

## Cómo verlo

**En línea (recomendado):** https://juan-alva-bustamante.github.io/principios-angular/maquetado/

También puedes abrirlo local: `css/main.css` ya está compilado y commiteado en el repo, así que puedes abrir `index.html` directamente (doble clic) sin instalar nada ni correr ningún servidor. (Evita los visores externos tipo "GitHub HTML preview": no resuelven bien las rutas relativas al CSS — usa el link de GitHub Pages de arriba.)

Eso sí: `css/main.css` es un archivo generado a partir de `scss/main.scss` — **no lo edites a mano**, tus cambios se perderían en el siguiente `build:css`. Si necesitas cambiar estilos:

```bash
npm install
npm run build:css
```

O, mientras editas, deja corriendo `npm run watch:css` y solo recarga la página al guardar cada `.scss`. Antes de subir tu cambio a git, corre `npm run build:css` una vez más y commitea también el `css/main.css` actualizado.

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
└── css/main.css                  # generado y commiteado, no editar a mano
```

## Qué archivo edita cada componente

| Componente | Archivo(s) SCSS | Bloque en `index.html` |
|---|---|---|
| App shell / layout | `_layout.scss`, `_responsive-overrides.scss` | `<div class="app">` |
| Panel de info de contacto (TV) | `_chat-info.scss` | `<aside class="chat-info">` |
| Sidebar — lista de chats | `_sidebar.scss` | `<aside class="sidebar">` |
| Header del chat activo | `_chat-header.scss` | `<header class="chat__header">` |
| Barra de entrada | `_message-input.scss` | `<form class="message-input">` |
| Hilo de mensajes | `_messages.scss` | `<div class="chat__messages">` |

El `index.html` ya está completo con contenido de ejemplo y comentarios marcando cada bloque, para que sea fácil ubicar qué HTML corresponde a qué archivo SCSS (y, más adelante, a qué componente de Angular).

**Regla importante de CSS:** si necesitas cambiar cómo se ve un componente según el dispositivo (ej. "en reloj, ocultar el botón X del header"), ese ajuste va en `_responsive-overrides.scss`, no en el archivo de ese componente. Está explicado (el porqué) en un comentario dentro de ese archivo — es un bug real de cascada CSS en el que ya caí al construir este maquetado.

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
- [ ] Probado con contenido "real" adicional (nombres muy largos, chat sin mensajes, chat con muchísimos mensajes)
