# Plan de aprendizaje: Angular a través de una UI de mensajería en vivo

**Equipo:** 4 personas (todas nuevas en Angular)
**Objetivo:** aprender Angular construyendo, en equipo, una interfaz de mensajería en vivo (estilo WhatsApp), responsiva para teléfono, tablet, TV, auto y reloj inteligente.

**Regla de oro del proceso:** no saltar directo a Angular. Se avanza en 3 fases secuenciales, cada una validada antes de pasar a la siguiente.

---

## Fase 1 — Maquetado HTML/CSS (repartido por componentes)

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

### Reparto de componentes (4 personas)

| Persona | Componente(s) | Contenido |
|---|---|---|
| **1 (integrador/a)** | Layout base / Shell + Navegación adaptativa | Grid general, variables CSS (colores, tipografía), breakpoints responsivos, bottom nav para móvil, estado vacío ("selecciona un chat"), transiciones entre vistas |
| **2** | Sidebar — Lista de chats | Buscador, item de chat (avatar, nombre, último mensaje, hora, badge de no leídos) |
| **3** | Header del chat activo + Barra de entrada de mensaje | Avatar, nombre, estado ("en línea"), iconos de llamada/video/menú — Input de texto, emoji, adjuntar, botón enviar |
| **4** | Hilo de mensajes | Burbujas enviado/recibido, separador de fecha, hora, check de leído |

Cada persona trabaja su propio archivo CSS (`sidebar.css`, `messages.css`, etc.) y su bloque de HTML delimitado con comentarios claros (`<!-- INICIO: chat-header -->` / `<!-- FIN: chat-header -->`), para integrarlos luego en un solo `index.html` sin pisarse entre sí.

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
- Convención de commits y flujo de git para el equipo (rama por componente + PRs)

---

## Fase 3 — Repo base de Angular

- `ng new` con las opciones definidas en la guía de Fase 2
- Estructura de carpetas/componentes que refleja 1:1 los componentes del maquetado de Fase 1 (cada persona migra su HTML/CSS ya validado a su componente Angular)
- Componentes generados como placeholders (vacíos o con el maquetado ya movido) para que cada quien complete la lógica
- README con instrucciones de clonado/setup y convenciones
- La integración final (routing, comunicación entre componentes, servicios) queda a cargo del equipo, no se resuelve en esta etapa

---

## Estado actual

- [x] Plan aprobado (equipo de 4 personas)
- [ ] Fase 1: maquetado HTML/CSS
- [ ] Fase 2: guía de setup de Angular
- [ ] Fase 3: repo base de Angular
