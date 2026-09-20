# Plan de aprendizaje: Angular a través de una UI de mensajería en vivo

**Autor/a:** 1 persona (nueva en Angular)
**Objetivo:** aprender Angular construyendo una interfaz de mensajería en vivo (estilo WhatsApp), responsiva para teléfono, tablet, TV, auto y reloj inteligente.

**Regla de oro del proceso:** no saltar directo a Angular. Se avanza en 3 fases secuenciales, cada una validada antes de pasar a la siguiente.

---

## Fase 1 — Maquetado HTML/CSS (por componentes)

### Estructura de la interfaz

```
┌─────────────┬──────────────────────────┐
│  Sidebar    │  Header del chat activo   │
│  (buscador  ├──────────────────────────┤
│  + lista de │                          │
│  chats)     │  Hilo de mensajes         │
│             │  (burbujas + fechas)      │
│             ├──────────────────────────┤
│             │  Barra de entrada         │
└─────────────┴──────────────────────────┘
```

### Componentes a construir

| Componente | Contenido |
|---|---|
| Layout base / Shell + Navegación adaptativa | Grid general, variables CSS (colores, tipografía), breakpoints responsivos, bottom nav para móvil, estado vacío ("selecciona un chat"), transiciones entre vistas |
| Sidebar — Lista de chats | Buscador, item de chat (avatar, nombre, último mensaje, hora, badge de no leídos) |
| Header del chat activo | Avatar, nombre, estado ("en línea"), iconos de llamada/video/menú |
| Barra de entrada de mensaje | Input de texto, emoji, adjuntar, botón enviar |
| Hilo de mensajes | Burbujas enviado/recibido, separador de fecha, hora, check de leído |

Cada componente vive en su propio archivo CSS (`sidebar.css`, `messages.css`, etc.) y su bloque de HTML está delimitado con comentarios claros, para que sea fácil ubicar qué HTML corresponde a qué archivo — y más adelante, a qué componente de Angular.

### Breakpoints responsivos

| Dispositivo | Ancho aprox. | Enfoque de UI |
|---|---|---|
| ⌚ Reloj inteligente | ≤ 260px | Solo el mensaje/chat más reciente, texto grande, sin sidebar |
| 📱 Teléfono | 261–599px | Una vista a la vez (lista **o** chat), navegación tipo "stack" |
| 📱 Tablet | 600–1023px | Maestro-detalle: lista + chat lado a lado |
| 🚗 Auto (pantalla infotainment) | 1024–1280px, horizontal | Maestro-detalle simplificado, botones grandes, alto contraste, mínima distracción |
| 📺 TV | ≥ 1281px | 3 columnas, tipografía grande, estados de `:focus` visibles (navegación con control remoto/flechas) |

### Entregable de la fase

Carpeta `/maquetado` con:
- `index.html`
- `/css`: `variables.css`, `layout.css`, `sidebar.css`, `chat-header.css`, `messages.css`, `message-input.css`, `responsive.css`
- `/assets`: avatares/íconos placeholder

HTML semántico, mobile-first, con comentarios explicando el "por qué" de cada regla responsiva (no solo el qué), ya que este maquetado es material de aprendizaje y luego mapea 1:1 a los componentes de Angular.

### Checklist de validación antes de pasar a Fase 2

- [ ] Se ve bien en los 5 breakpoints (probado con DevTools)
- [ ] HTML semántico (`<header>`, `<nav>`, `<main>`, `<ul>` para listas, etc.)
- [ ] Sin errores de consola, contraste de color aceptable
- [ ] Probado con contenido "real" (nombres largos, muchos mensajes, sin mensajes)

---

## Fase 2 — Guía de setup inicial de Angular (documento HTML)

Contenido de la guía:
- Qué es Angular y conceptos clave (componentes, templates, data binding, standalone components vs NgModules)
- Requisitos previos: Node.js LTS, npm, VS Code + extensiones recomendadas
- Instalación de Angular CLI y comandos básicos (`ng new`, `ng generate component`, `ng serve`)
- Estructura de carpetas de un proyecto Angular explicada
- Stack a usar: standalone components (enfoque moderno, más simple para empezar), SCSS, Angular Router, Signals para estado (se evita NgRx por ahora), ESLint + Prettier
- Convención de commits y flujo de git (rama por componente)

---

## Fase 3 — Repo base de Angular

Tutorial completo, paso a paso: [`guia-angular/tutorial-paso-a-paso.html`](guia-angular/tutorial-paso-a-paso.html) — desde instalar Node.js hasta el proyecto Angular funcionando, con el contenido exacto de cada archivo.

Diagrama de referencia: [`guia-angular/diagrama-componentes.html`](guia-angular/diagrama-componentes.html) — mapea cada región del maquetado a su componente Angular y carpeta en `src/app/`.

- `ng new` con las opciones definidas en la guía de Fase 2
- Estructura de carpetas/componentes que refleja 1:1 los componentes del maquetado de Fase 1 (se migra cada bloque de HTML/CSS ya validado a su propio componente Angular, uno a la vez)
- Componentes generados como placeholders (vacíos o con el maquetado ya movido) para completar la lógica después
- README con instrucciones de setup y convenciones
- La integración final (routing, comunicación entre componentes, servicios) se resuelve en esta fase, componente por componente

---

## Estado actual

- [x] Plan aprobado (proyecto individual)
- [x] Fase 1: maquetado HTML/CSS
- [x] Fase 2: guía de setup de Angular
- [ ] Fase 3: repo base de Angular
