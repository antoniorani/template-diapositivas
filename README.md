# Template Diapositivas

Template mínimo para crear presentaciones web y publicarlas directamente con GitHub Pages.

La idea es deliberadamente sencilla:

- **Reveal.js** resuelve el motor de presentación.
- **index.html** contiene las diapositivas.
- **style.css** contiene el aspecto visual.
- **notes-panel.js** muestra en la propia presentación las notas de la diapositiva actual.
- **assets/** guarda imágenes, vídeos y otros recursos.
- No hay npm, build, framework propio ni GSAP por defecto.

## Para crear una presentación

1. Crea un repositorio usando este template.
2. Edita `index.html`.
3. Sustituye las slides de ejemplo por las tuyas.
4. Ajusta `style.css` solo si necesitas cambiar el lenguaje visual.
5. Activa GitHub Pages sobre la rama `main` y `/root`.

Eso es todo.

## Anatomía de una slide

Cada diapositiva es un `<section>` dentro de:

```html
<div class="reveal">
  <div class="slides">
    <!-- slides aquí -->
  </div>
</div>
```

Ejemplo:

```html
<section>
  <p class="eyebrow">Sección</p>
  <h2>Título principal</h2>
  <p class="lead">Idea central de la diapositiva.</p>
</section>
```

## Apariciones paso a paso

Reveal.js ya incluye fragmentos. Solo añade `class="fragment"`:

```html
<p class="fragment">Aparezco al avanzar.</p>
```

## Transiciones automáticas entre dos slides

Reveal.js también incluye Auto-Animate. Pon `data-auto-animate` en dos slides consecutivas y usa el mismo `data-id` en los elementos que deban transformarse:

```html
<section data-auto-animate>
  <h2 data-id="title">Antes</h2>
</section>

<section data-auto-animate>
  <h2 data-id="title">Después</h2>
</section>
```

No hace falta escribir JavaScript para esa transición.

## Notas del presentador

Dentro de una slide:

```html
<aside class="notes">
  Estas notas solo aparecen en la vista del presentador.
</aside>
```

Durante la presentación pulsa **S** para abrir la vista del presentador.

El template incluye además un **panel inferior de notas** que sigue automáticamente la diapositiva actual. Pulsa **N** o haz clic en la pestaña **Notas** para abrirlo o cerrarlo.

## Controles útiles

| Acción | Control |
|---|---|
| Avanzar / retroceder | Flechas |
| Avanzar | Espacio |
| Vista general | Esc |
| Notas del presentador | S |
| Ayuda de atajos | ? |
| Navegación táctil | Deslizar |

## Publicar en GitHub Pages

En el repositorio:

1. **Settings → Pages**
2. **Build and deployment → Deploy from a branch**
3. Rama: **main**
4. Carpeta: **/(root)**
5. **Save**

La presentación quedará en una URL similar a:

```text
https://TU_USUARIO.github.io/NOMBRE-DEL-REPO/
```

Cada commit nuevo en `main` actualizará la misma URL.

## Criterio del template

Este repositorio no pretende acumular funciones. Pretende quitar trabajo.

Para una presentación normal, no añadas librerías. Reveal.js ya cubre navegación, responsive, progreso, enlaces por slide, fragmentos, Auto-Animate y notas.

Solo añadiremos JavaScript específico cuando una diapositiva concreta realmente lo necesite.
