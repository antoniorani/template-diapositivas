# Registro de regresiones

Este archivo recoge fallos reales introducidos durante cambios técnicos para evitar repetirlos en futuras presentaciones.

## 2026-10-02 — Reveal.js remoto dejó la presentación en blanco

**Cambio que introdujo la regresión**

Se sustituyeron los archivos locales de Reveal.js 6.0.1 (`reveal.js`, `reveal.css` y `notes.js`) por referencias equivalentes a jsDelivr con el objetivo de simplificar el repositorio.

**Síntoma observado**

La presentación publicada en GitHub Pages cargaba como una página completamente en blanco. El workflow de GitHub Pages terminaba correctamente, por lo que el despliegue exitoso no detectó el fallo de ejecución en el navegador.

**Lección**

Las dependencias necesarias para que la presentación llegue siquiera a inicializarse son dependencias críticas de ejecución. Reducir archivos no compensa introducir un nuevo punto externo de fallo.

**Regla para el futuro**

- Mantener Reveal.js y el plugin de notas vendorizados localmente en `vendor/reveal/`.
- No sustituir dependencias críticas locales por CDN sin una razón funcional clara.
- Después de cambiar rutas de scripts, CSS, plugins o dependencias, hacer una prueba de humo sobre la URL publicada, no solo comprobar que GitHub Pages haya desplegado.
- Conservar la Speaker View nativa de Reveal.js mediante `RevealNotes`; no reimplementar un sistema propio salvo necesidad demostrada.

**Corrección aplicada**

Se restauraron los archivos locales de Reveal.js 6.0.1 y se actualizó el template para que las nuevas presentaciones hereden este enfoque.
