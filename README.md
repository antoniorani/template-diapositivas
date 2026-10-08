# Template Diapositivas

Motor mínimo y autocontenido para crear presentaciones web con Reveal.js y publicarlas con GitHub Pages.

## Responsabilidad de este repositorio

Este repositorio es la **fuente de verdad del motor común**. Aquí viven únicamente las decisiones que deben poder reutilizar todas las presentaciones:

- Reveal.js y Notes vendorizados localmente;
- configuración base del lienzo 1600 × 900;
- navegación, progreso, hash y Auto-Animate;
- Speaker View;
- galería de diapositivas y contador `Diapositiva N / total` para el ponente;
- contrato de renderizado y publicación.

No contiene identidad visual AEPD ni contenido de cursos concretos.

## Estructura

- `index.html`: slides de ejemplo y configuración de Reveal.
- `style.css`: estilos genéricos del template.
- `speaker-gallery.js`: personalizaciones comunes de Speaker View.
- `assets/`: recursos propios de una presentación.
- `vendor/reveal/`: Reveal.js y Notes, servidos localmente.
- `REGRESSIONS.md`: regresiones del motor común.

No hay npm, build, bundler ni framework propio.

## Crear una presentación

1. Crea un repositorio desde este template.
2. Sustituye las slides de ejemplo en `index.html`.
3. Ajusta `style.css` solo cuando el contenido lo necesite.
4. Añade recursos en `assets/`.
5. Publica GitHub Pages desde `main` y `/(root)`.

Una slide es simplemente un `<section>` dentro de `.reveal .slides`. Las notas del ponente van dentro de:

```html
<aside class="notes">...</aside>
```

Reveal ya cubre fragmentos y Auto-Animate; no programes una solución propia cuando el motor ya resuelve el caso.

## Contrato de renderizado

El deck se diseña como un lienzo fijo de **1600 × 900** y Reveal escala la composición completa.

Mantener:

```js
width: 1600,
height: 900,
margin: 0,
minScale: 0.1,
maxScale: 10,
scrollActivationWidth: null
```

No usar breakpoints para reorganizar el contenido como una página responsive. Los media queries de accesibilidad, como `prefers-reduced-motion`, sí son válidos.

## Speaker View

La audiencia **no ve numeración de diapositivas**.

Speaker View muestra `Diapositiva N / total` sobre la slide actual y añade una galería accesible con **G** o con el botón **Todas las diapositivas**.

La personalización vive en `speaker-gallery.js`. No modificar `vendor/reveal/notes.js` para añadir interfaz propia.

## Dependencias

Reveal.js es una dependencia crítica de ejecución y se conserva vendorizado en `vendor/reveal/`. No sustituirlo por CDN solo para reducir archivos; existe una regresión documentada en `REGRESSIONS.md`.

## Publicación

La política común es **GitHub Pages → Deploy from a branch**:

- rama: `main`;
- carpeta: `/(root)`;
- sin workflow de despliegue.

Cada commit en `main` debe actualizar la misma URL pública.

## Relación con repositorios derivados

La relación entre repositorios es por **copia autocontenida**, no por dependencia en runtime.

- `template-diapositivas` mantiene el motor común.
- `template-diapositivas-aepd` copia deliberadamente ese motor y añade únicamente la capa visual AEPD.
- Una presentación concreta copia el template que corresponda y añade únicamente su contenido y excepciones.

Las mejoras genéricas deben incorporarse primero aquí y propagarse después. No introducir submódulos, paquetes remotos ni imports entre repositorios solo para sincronizar copias.
