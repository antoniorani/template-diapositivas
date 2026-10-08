# Registro de regresiones · motor común

Este archivo contiene únicamente regresiones del motor reutilizable. Las plantillas especializadas y los cursos deben registrar en sus propios repositorios solo los fallos específicos de su capa.

## 2026-10-02 — Reveal.js remoto dejó la presentación en blanco

**Cambio que introdujo la regresión**

Se sustituyeron los archivos locales de Reveal.js (`reveal.js`, `reveal.css` y `notes.js`) por referencias equivalentes a un CDN.

**Síntoma**

GitHub Pages desplegó correctamente, pero la presentación publicada quedó en blanco.

**Lección**

Las dependencias necesarias para inicializar el deck son críticas de ejecución. Ahorrar archivos no compensa añadir un punto externo de fallo.

**Regla**

- Mantener Reveal.js y Notes vendorizados en `vendor/reveal/`.
- No sustituir dependencias críticas locales por CDN sin una razón funcional clara.
- Validar los cambios de scripts, CSS, plugins o rutas abriendo la presentación publicada.
- Mantener la Speaker View nativa mediante `RevealNotes`; las personalizaciones deben vivir fuera del código vendorizado.
