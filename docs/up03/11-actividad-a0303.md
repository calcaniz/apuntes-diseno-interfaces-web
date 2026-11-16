---
title: 10. Actividad A03.03. FestWeb con Bootstrap y Sass
---

# 10. Actividad A03.03. FestWeb con Bootstrap y Sass

**Duración:** 55 minutos  
**Modalidad:** Actividad formativa guiada  
**Realización:** Sesión síncrona  
**Entrega:** No requiere entrega independiente  
**Criterios trabajados:** CE02-i y CE02-j

## 10.1. Objetivo

En esta actividad utilizaremos Bootstrap para reconstruir la distribución responsive de FestWeb y Sass para organizar sus personalizaciones visuales.

Al finalizar deberemos haber utilizado:

- El sistema de cuadrícula de Bootstrap.
- Clases responsive.
- Utilidades de espaciado y Flexbox.
- Componentes de tarjeta y botón.
- Variables Sass.
- Archivos parciales.
- El sistema de módulos con `@use`.
- Un mixin reutilizable.
- La compilación de SCSS a CSS.

## 10.2. Punto de partida

Realiza una copia del proyecto anterior y renómbrala:

```text
A03.03/
```

Conserva una copia del CSS de la actividad anterior con el nombre:

```text
css/estilos-a0302.css
```

El nuevo archivo `css/estilos.css` será generado por Sass. No deberá modificarse manualmente.

La estructura final será:

```text
A03.03/
├── index.html
├── css/
│   ├── estilos-a0302.css
│   └── estilos.css
├── scss/
│   ├── _variables.scss
│   ├── _mixins.scss
│   ├── _componentes.scss
│   └── estilos.scss
└── src/
    └── assets/
        ├── img01.png
        ├── img02.png
        └── img03.png
```

## 10.3. Organización de la sesión

| Fase { .table-full-container .table-cl-secundario .table-bg-principal } | Trabajo previsto { .table-cl-secundario .table-bg-principal } | Tiempo { .table-cl-secundario .table-bg-principal } |
|---|---|:---:|
| 1 | Incorporación de Bootstrap | 5 min |
| 2 | Adaptación de la cabecera y presentación | 10 min |
| 3 | Cuadrícula y tarjetas | 15 min |
| 4 | Organización de Sass | 15 min |
| 5 | Compilación y comprobaciones | 10 min |

## 10.4. Incorporación de Bootstrap

Añade la hoja de estilos de Bootstrap dentro de `<head>`:

```html
<link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB"
    crossorigin="anonymous"
>

<link rel="stylesheet" href="./css/estilos.css">
```

Nuestra hoja debe cargarse después de Bootstrap.

Añade también el archivo JavaScript antes de cerrar `</body>`:

```html
<script
    src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI"
    crossorigin="anonymous"
></script>
```

En esta actividad no utilizaremos todavía componentes JavaScript, pero dejaremos preparado el proyecto para poder incorporar posteriormente menús plegables, modales o desplegables.

## 10.5. Adaptación de la cabecera

Modifica las clases del contenedor de la cabecera:

```html
<div
    class="
        container
        cabecera__contenido
        d-flex
        flex-column
        flex-lg-row
        align-items-stretch
        align-items-lg-center
        gap-3
        py-3
    "
>
```

El elemento se organizará:

- Verticalmente en móvil.
- Horizontalmente desde el breakpoint `lg`.
- Con una separación `gap-3`.
- Con espaciado vertical `py-3`.

Añade clases Bootstrap al logotipo:

```html
<a class="logotipo navbar-brand m-0" href="#">
    FestWeb
</a>
```

Adapta la navegación:

```html
<nav
    class="
        navegacion
        d-flex
        flex-column
        flex-md-row
        justify-content-center
        flex-grow-1
        gap-2
    "
    aria-label="Navegación principal"
>
```

Los enlaces pueden recibir las siguientes clases:

```html
<a class="nav-link text-center" href="#">Inicio</a>
<a class="nav-link text-center" href="#">Eventos</a>
<a class="nav-link text-center" href="#">Categorías</a>
<a class="nav-link text-center" href="#">Contacto</a>
```

El botón de acceso utilizará una variante propia que crearemos mediante Sass:

```html
<a class="btn btn-festweb" href="#">
    Acceder
</a>
```

## 10.6. Adaptación de la presentación

Añade las utilidades de Bootstrap a la sección:

```html
<section class="presentacion py-5">
```

Sustituye la clase `contenedor` por el contenedor de Bootstrap:

```html
<div class="container">
```

La categoría puede mostrarse como una insignia:

```html
<p class="etiqueta badge mb-3">
    Agenda de eventos
</p>
```

El título mantendrá su clase propia y añadirá separación:

```html
<h1 class="presentacion__titulo display-4 fw-bold mb-3">
    Encuentra tu próximo plan
</h1>
```

La descripción tendrá una anchura de lectura controlada mediante nuestra hoja Sass:

```html
<p class="presentacion__descripcion lead mb-0">
    Descubre propuestas musicales, deportivas y culturales
    cerca de ti.
</p>
```

## 10.7. Cuadrícula de eventos

Modifica la cabecera de la sección:

```html
<div
    class="
        eventos__cabecera
        d-flex
        flex-column
        flex-sm-row
        justify-content-between
        align-items-sm-center
        gap-2
        mb-4
    "
>
```

Transforma el listado en una fila responsive de Bootstrap:

```html
<div
    class="
        listado-eventos
        row
        row-cols-1
        row-cols-md-2
        row-cols-lg-3
        g-4
    "
>
```

La cuadrícula mostrará:

- Una tarjeta por fila en móvil.
- Dos tarjetas desde `md`.
- Tres tarjetas desde `lg`.

## 10.8. Adaptación de las tarjetas

Cada tarjeta debe quedar dentro de una columna Bootstrap.

La estructura será:

```html
<div class="col">
    <article class="tarjeta-evento card h-100">
        <!-- Contenido de la tarjeta -->
    </article>
</div>
```

Por tanto, envuelve cada uno de los tres elementos `<article>` existentes con:

```html
<div class="col">
```

y cierra el contenedor después de `</article>`:

```html
</div>
```

La imagen utilizará:

```html
<img
    class="tarjeta-evento__imagen card-img-top"
    src="./src/assets/img01.png"
    alt="Escenario de un festival de música"
    width="800"
    height="450"
>
```

El contenido de la tarjeta será:

```html
<div class="tarjeta-evento__contenido card-body d-flex flex-column">
```

Adapta la etiqueta:

```html
<p class="etiqueta badge align-self-start mb-3">
    Música
</p>
```

Adapta el título:

```html
<h3 class="tarjeta-evento__titulo card-title h5">
    Festival Mediterráneo
</h3>
```

Los datos secundarios pueden utilizar:

```html
<p class="tarjeta-evento__datos small mb-2">
    Valencia · 20 de junio
</p>
```

La descripción utilizará:

```html
<p class="tarjeta-evento__descripcion card-text">
    Una jornada de música en directo junto al mar.
</p>
```

Las acciones se situarán al final de la tarjeta:

```html
<div
    class="
        tarjeta-evento__acciones
        d-flex
        flex-column
        flex-sm-row
        gap-2
        mt-auto
    "
>
```

Los botones quedarán así:

```html
<a class="btn btn-festweb" href="#">
    Ver evento
</a>

<button
    class="btn btn-outline-festweb"
    type="button"
>
    Guardar
</button>
```

Repite la misma estructura en las tres tarjetas.

## 10.9. Instalación de Sass

Abre una terminal dentro de `A03.03` e instala Sass:

```bash
npm install --save-dev sass
```

Si el proyecto todavía no dispone de `package.json`, ejecuta primero:

```bash
npm init -y
```

## 10.10. Variables de FestWeb

Crea el archivo:

```text
scss/_variables.scss
```

Añade:

```scss
$color-principal: #50c9e9;
$color-secundario: #3b82e6;
$color-fondo: #c6d8ff;
$color-acento: #a3a313;
$color-texto: #213fc2;
$color-advertencia: #e8b718;
$color-superficie: #ffffff;

$espacio-md: 1rem;
$espacio-lg: 1.5rem;

$radio-md: 0.75rem;
```

## 10.11. Mixin de foco

Crea:

```text
scss/_mixins.scss
```

Añade un mixin para mantener un foco de teclado visible:

```scss
@mixin foco-visible($color) {
    &:focus-visible {
        outline: 3px solid $color;
        outline-offset: 3px;
    }
}
```

Este mixin podrá aplicarse a diferentes componentes interactivos.

## 10.12. Componentes personalizados

Crea:

```text
scss/_componentes.scss
```

Carga las variables y los mixins:

```scss
@use "variables" as v;
@use "mixins" as m;
```

Personaliza el logotipo:

```scss
.logotipo {
    padding: 0.5rem 1rem;
    color: v.$color-texto;
    background-color: v.$color-principal;
    border-radius: v.$radio-md;
    font-weight: 700;
}
```

Crea la etiqueta:

```scss
.etiqueta {
    color: v.$color-texto;
    background-color: v.$color-fondo;
    border-left: 4px solid v.$color-acento;
}
```

Crea el botón principal:

```scss
.btn-festweb {
    --bs-btn-color: #{v.$color-superficie};
    --bs-btn-bg: #{v.$color-texto};
    --bs-btn-border-color: #{v.$color-texto};
    --bs-btn-hover-color: #{v.$color-superficie};
    --bs-btn-hover-bg: #{v.$color-secundario};
    --bs-btn-hover-border-color: #{v.$color-secundario};

    @include m.foco-visible(v.$color-principal);
}
```

Crea el botón secundario:

```scss
.btn-outline-festweb {
    --bs-btn-color: #{v.$color-texto};
    --bs-btn-border-color: #{v.$color-texto};
    --bs-btn-hover-color: #{v.$color-superficie};
    --bs-btn-hover-bg: #{v.$color-texto};
    --bs-btn-hover-border-color: #{v.$color-texto};

    @include m.foco-visible(v.$color-principal);
}
```

Personaliza las tarjetas:

```scss
.tarjeta-evento {
    border-color: v.$color-principal;
    border-radius: v.$radio-md;
    overflow: hidden;
}

.tarjeta-evento__imagen {
    aspect-ratio: 16 / 10;
    object-fit: cover;
}
```

## 10.13. Archivo principal Sass

Crea:

```text
scss/estilos.scss
```

Carga los módulos:

```scss
@use "variables" as v;
@use "componentes";

body {
    color: v.$color-texto;
    background-color: v.$color-fondo;
}

.cabecera,
.presentacion,
.tarjeta-evento {
    background-color: v.$color-superficie;
}

.presentacion__descripcion {
    max-width: 42rem;
}

.pie {
    padding-block: 2rem;
    color: v.$color-superficie;
    background-color: v.$color-texto;
}
```

## 10.14. Compilación

Ejecuta Sass en modo observación:

```bash
npx sass scss/estilos.scss css/estilos.css --watch
```

Mantén la terminal abierta mientras trabajas.

Cada vez que guardes un archivo SCSS, Sass actualizará:

```text
css/estilos.css
```

No modifiques directamente el archivo generado.

## 10.15. Comprobaciones finales

Revisa FestWeb en:

| Anchura { .table-full-container .table-cl-secundario .table-bg-principal } | Resultado esperado { .table-cl-secundario .table-bg-principal } |
|---|---|
| `390px` | Cabecera vertical, una tarjeta por fila y botones apilados. |
| `768px` | Navegación horizontal y dos tarjetas por fila. |
| `1280px` | Cabecera horizontal y tres tarjetas por fila. |

Comprueba también que:

- Bootstrap se carga correctamente.
- `estilos.css` aparece después de Bootstrap.
- Las tarjetas mantienen la misma altura.
- Las imágenes no se deforman.
- Los botones utilizan los colores de FestWeb.
- El foco de teclado resulta visible.
- Sass recompila al guardar.
- No aparecen errores en la terminal.
- No existe desplazamiento horizontal.

## 10.16. Puesta en común

Al finalizar, responde oralmente:

1. ¿Qué partes de la interfaz resuelve Bootstrap?
2. ¿Qué estilos siguen siendo responsabilidad de FestWeb?
3. ¿Qué significan `row-cols-1`, `row-cols-md-2` y `row-cols-lg-3`?
4. ¿Por qué se utiliza un contenedor `.col` alrededor de cada tarjeta?
5. ¿Qué función realiza el mixin `foco-visible`?
6. ¿Qué archivo se modifica y cuál se genera?
7. ¿Por qué nuestra hoja CSS se carga después de Bootstrap?

## 10.17. Ampliación

Si terminas antes, añade un efecto visual reutilizable mediante un mixin:

```scss
@mixin elevacion($sombra) {
    box-shadow: $sombra;
    transition:
        transform 0.2s ease,
        box-shadow 0.2s ease;

    &:hover {
        transform: translateY(-4px);
    }
}
```

Aplícalo a las tarjetas:

```scss
.tarjeta-evento {
    @include m.elevacion(
        0 4px 12px rgb(33 63 194 / 15%)
    );
}
```

---