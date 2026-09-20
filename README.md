# Principios Angular

Proyecto de aprendizaje en equipo (4 personas, todas nuevas en Angular): aprender Angular construyendo entre todos una interfaz de mensajería en vivo (estilo WhatsApp), responsiva para **teléfono, tablet, TV, auto y reloj inteligente**.

El plan completo, con el detalle de cada fase, está en **[PLAN.md](PLAN.md)**. Este README es solo el mapa rápido del repo.

## Cómo avanza el proyecto

No se salta directo a Angular. Se avanza en 3 fases secuenciales, cada una validada antes de pasar a la siguiente:

| Fase | Qué es | Estado | Carpeta |
|---|---|---|---|
| 1 | Maquetado HTML/SCSS del chat, repartido por componentes entre las 4 personas | ✅ Hecho | [`maquetado/`](maquetado/) |
| 2 | Guía de setup de Angular: conceptos, instalación de herramientas, reparto de componentes, convenciones del equipo | ✅ Hecho | [`guia-angular/`](guia-angular/) |
| 3 | Repo base de Angular (creado a partir de lo definido en la Fase 2), con la estructura de componentes lista para que cada persona integre su parte | ⬜ Pendiente | — |

## Estructura del repositorio

```
principios-angular/
├── PLAN.md                # el plan completo, con el reparto de componentes y los breakpoints
├── maquetado/              # Fase 1 — HTML + SCSS del chat (sin Angular todavía)
│   ├── index.html
│   ├── scss/               # un archivo por componente, ver maquetado/README.md
│   └── README.md
├── guia-angular/            # Fase 2 — guía de setup de Angular (documento HTML)
│   ├── index.html
│   ├── scss/styles.scss
│   └── README.md
└── .claude/launch.json      # sirve maquetado/ y guia-angular/ localmente para previsualizarlos
```

## Equipo (4 personas)

El mismo reparto se usa en el maquetado (Fase 1) y se traslada 1:1 a los componentes de Angular (Fase 2 y 3):

| Persona | Parte de la interfaz |
|---|---|
| 1 (integrador/a) | Layout base / app shell, navegación adaptativa, panel de info de contacto (TV) |
| 2 | Sidebar — lista de chats |
| 3 | Header del chat activo + barra de entrada de mensaje |
| 4 | Hilo de mensajes (burbujas) |

Detalle completo (incluyendo el mapeo a componentes de Angular y carpetas) en [PLAN.md](PLAN.md) y en la sección "Reparto de componentes por persona" de la [guía de Angular](guia-angular/index.html).

## Dispositivos y breakpoints

La interfaz se diseñó para verse bien en 5 tipos de pantalla, no solo teléfono/desktop:

| Dispositivo | Ancho aprox. |
|---|---|
| ⌚ Reloj inteligente | ≤ 260px |
| 📱 Teléfono | 261–599px |
| 📱 Tablet | 600–1023px |
| 🚗 Auto (infotainment) | 1024–1280px |
| 📺 TV | ≥ 1281px |

## Cómo ver el maquetado y la guía

El repo está publicado con **GitHub Pages** — ábrelo directo, con estilos, sin instalar nada:

- Maquetado (Fase 1): **https://juan-alva-bustamante.github.io/principios-angular/maquetado/**
- Guía de Angular (Fase 2): **https://juan-alva-bustamante.github.io/principios-angular/guia-angular/**

(Los visores externos tipo "GitHub HTML preview" no funcionan bien aquí: sirven el HTML pero no resuelven las rutas relativas al CSS. Usa los links de arriba en su lugar.)

También puedes abrir `maquetado/index.html` o `guia-angular/index.html` directo en tu máquina (doble clic) — el CSS ya viene compilado y commiteado. Solo necesitas `npm install && npm run build:css` (dentro de `maquetado/` o `guia-angular/`) si vas a **editar** los archivos `.scss` — instrucciones completas en el `README.md` de cada carpeta.
