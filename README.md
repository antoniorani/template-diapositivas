# Template Diapositivas

Template mínimo para crear presentaciones web y publicarlas directamente con GitHub Pages.

La idea es deliberadamente sencilla:

- **Reveal.js** resuelve el motor de presentación.
- **index.html** contiene las diapositivas.
- **style.css** contiene el aspecto visual.
- **assets/** guarda imágenes, vídeos y otros recursos.
- **vendor/reveal/** contiene Reveal.js y el plugin de notas servidos localmente.
- **speaker-gallery.js** añade la galería de navegación a la Speaker View sin modificar el código vendorizado de Reveal.js.
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

## Fiabilidad de dependencias

Reveal.js se sirve localmente desde `vendor/reveal/`. No lo sustituyas por un CDN solo para reducir archivos: una regresión real dejó una presentación completamente en blanco aunque GitHub Pages había desplegado correctamente. Consulta `REGRESSIONS.md` antes de simplificar dependencias de ejecución.


## Contrato de diseño: lienzo fijo

Las presentaciones se diseñan como un lienzo fijo de **1600 × 900**. Reveal.js escala el lienzo completo para adaptarlo al viewport; el contenido interno no debe reorganizarse según el tamaño de pantalla.

Reglas:

- No uses `@media (max-width: ...)` para cambiar columnas, paddings, tamaños o posiciones dentro de una slide.
- No construyas una versión móvil distinta de la diapositiva.
- Mantén `width: 1600`, `height: 900`, `margin: 0`, `minScale: 0.1` y `scrollActivationWidth: null`.
- Usa píxeles, porcentajes, Grid y Flexbox relativos al lienzo, no al viewport, para la geometría interna.
- Los media queries de accesibilidad como `prefers-reduced-motion` sí son válidos porque no cambian la composición.
- Comprueba que la misma composición se conserva en escritorio, portátil, móvil horizontal y móvil vertical; solo debe variar la escala.


## Galería de diapositivas en Speaker View

La audiencia no ve numeración de diapositivas. Speaker View muestra `Diapositiva N / total` sobre la vista actual.


Pulsa **S** para abrir la Speaker View. Dentro de esa ventana, pulsa **G** o el botón **Todas las diapositivas** para abrir una galería temporal con miniaturas de todo el deck.

- Flechas: recorrer miniaturas.
- Enter o Espacio: saltar a la diapositiva seleccionada.
- Esc: cerrar la galería y volver a las notas.
- Clic en una miniatura: saltar directamente a esa diapositiva.

La implementación vive en `speaker-gallery.js`. **No modifiques `vendor/reveal/notes.js` para personalizaciones de interfaz**: mantener nuestra extensión separada reduce el riesgo al actualizar Reveal.js.

## Relación entre templates y presentaciones

Este repositorio es la **referencia del motor técnico** de las presentaciones.

La relación entre repositorios es deliberadamente por copia, no por dependencia en tiempo de ejecución:

1. `template-diapositivas` mantiene el motor común: Reveal.js, configuración base, Speaker View, galería y contrato de renderizado.
2. `template-diapositivas-aepd` incorpora de forma deliberada los cambios técnicos que sean útiles y añade la identidad visual AEPD.
3. Cada presentación creada desde un template es una **instantánea autocontenida**. No se actualiza automáticamente cuando cambia el template de origen.

Reglas de mantenimiento:

- Los cambios del motor común deben evaluarse primero aquí.
- Los cambios visuales específicos de AEPD pertenecen a `template-diapositivas-aepd`, no a este repositorio.
- Una presentación ya publicada solo debe recibir cambios del template si existe una razón concreta, especialmente una corrección importante o de fiabilidad.
- No añadas submódulos, CDN, paquetes remotos ni otras dependencias solo para mantener repositorios sincronizados.
- Antes de propagar un cambio técnico entre repositorios, valida primero que funciona en navegador y revisa `REGRESSIONS.md`.
