# Guía de setup de Angular — Fase 2

Documento HTML de referencia para instalar herramientas y entender los conceptos mínimos de Angular antes de crear el repo (Fase 3). Ver [`../PLAN.md`](../PLAN.md).

Un solo `index.html` + un solo `scss/styles.scss`, sin JavaScript — es un documento para leer, no una app.

## Cómo verla

**En línea (recomendado):** https://juan-alva-bustamante.github.io/principios-angular/guia-angular/

También puedes abrirla local: `css/styles.css` ya está compilado y commiteado en el repo, así que puedes abrir `index.html` directamente (doble clic) sin instalar nada ni correr ningún servidor. (Evita los visores externos tipo "GitHub HTML preview": no resuelven bien las rutas relativas al CSS — usa el link de GitHub Pages de arriba.)

Eso sí: `css/styles.css` es un archivo generado — **no lo edites a mano**. Si necesitas cambiar estilos, edita `scss/styles.scss` y recompílalo:

```bash
npm install
npm run build:css
```

O, mientras editas, deja corriendo `npm run watch:css` y solo recarga la página al guardar. Antes de subir tu cambio a git, corre `npm run build:css` una vez más y commitea también el `css/styles.css` actualizado.
