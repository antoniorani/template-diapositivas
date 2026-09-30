# Template Diapositivas

Plantilla base para crear presentaciones web animadas, publicables en GitHub Pages.

## Qué incluye

- Presentación 16:9 adaptable a cualquier pantalla.
- Navegación con teclado, ratón y táctil.
- Animaciones por diapositiva y por fragmentos.
- Soporte para GSAP desde CDN, con fallback nativo si no carga.
- Modo pantalla completa con `F`.
- Reinicio de animación con `R`.
- Vista de notas del presentador con `P` o `?presenter=1`.
- Enlaces directos a diapositivas con `#/1`, `#/2`, etc.
- Estilo premium oscuro tipo producto/Keynote.

## Cómo usarlo

Edita principalmente estos archivos:

- `index.html`: contenido de las diapositivas.
- `src/styles.css`: diseño visual, colores y composición.
- `src/app.js`: motor de navegación y animaciones.

Para presentar localmente, abre `index.html` en el navegador. Para evitar restricciones de algunos navegadores, también puedes lanzar un servidor local:

```bash
python3 -m http.server 8080
```

Y abrir:

```text
http://localhost:8080
```

## Publicar en GitHub Pages

En GitHub:

1. Abre **Settings → Pages**.
2. En **Build and deployment**, elige **Deploy from a branch**.
3. Selecciona la rama `main` y la carpeta `/root`.
4. Guarda.

La presentación quedará disponible en una URL como:

```text
https://TU_USUARIO.github.io/template-diapositivas/
```

## Controles

| Acción | Tecla / gesto |
|---|---|
| Avanzar | `→`, `Espacio`, clic |
| Retroceder | `←` |
| Ir al inicio | `Home` |
| Ir al final | `End` |
| Pantalla completa | `F` |
| Reiniciar animación | `R` |
| Mostrar/ocultar notas | `P` |
| Salir de notas | `Esc` |

## Estructura recomendada para nuevas presentaciones

Cada diapositiva es una sección:

```html
<section class="slide" data-title="Título corto" data-notes="Notas para el presentador">
  <p class="eyebrow">Sección</p>
  <h2>Título principal</h2>
  <p class="lead">Idea central de la diapositiva.</p>
  <div class="fragment">Aparece al avanzar.</div>
</section>
```

Usa `.fragment` para elementos que deben aparecer paso a paso.

## Recomendación de estilo

Mantén cada diapositiva como una escena, no como una lista de bullets. Mejor una idea fuerte, una visual clara y pocas palabras.