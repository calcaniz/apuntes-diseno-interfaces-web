---
title: 6. Bootstrap
---

# 6. Bootstrap

Bootstrap es un **framework CSS** que proporciona estilos, componentes y utilidades preparadas para crear interfaces web responsive.

En lugar de escribir todas las reglas desde cero, podemos aplicar clases ya definidas:

```html
<a class="btn btn-primary" href="#">
    Ver evento
</a>
```

Bootstrap no sustituye a CSS. Para utilizarlo correctamente debemos comprender:

- El modelo de caja.
- Flexbox y Grid.
- El diseño mobile first.
- Los breakpoints.
- La cascada y la especificidad.

## 6.1. ¿Qué aporta un framework CSS?

Un framework CSS ofrece una base común para desarrollar interfaces.

| Recurso { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| Sistema de cuadrícula | Organiza el contenido en filas y columnas responsive. |
| Utilidades | Aplican rápidamente espaciado, alineación, colores o tamaños. |
| Componentes | Proporcionan botones, tarjetas, menús, alertas o formularios. |
| Breakpoints | Permiten modificar la distribución según la anchura. |
| JavaScript | Añade comportamiento a menús, modales o desplegables. |

Su principal ventaja es acelerar el desarrollo y mantener una apariencia coherente.

Sin embargo, si se utiliza sin personalización, muchas páginas pueden terminar teniendo un aspecto demasiado similar.

## 6.2. Incorporación de Bootstrap

Para utilizar Bootstrap mediante CDN, añade su hoja de estilos dentro de `<head>`:

```html
<link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB"
    crossorigin="anonymous"
>
```

Nuestra hoja de estilos debe cargarse después:

```html
<link rel="stylesheet" href="./css/estilos.css">
```

El orden correcto será:

```html
<link href="bootstrap.min.css" rel="stylesheet">
<link href="./css/estilos.css" rel="stylesheet">
```

De esta forma, nuestras reglas pueden personalizar algunos estilos de Bootstrap mediante la cascada.

Los componentes interactivos necesitan también JavaScript. El siguiente script se añade antes de cerrar `</body>`:

```html
<script
    src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI"
    crossorigin="anonymous"
></script>
```

El archivo `bootstrap.bundle.min.js` incluye los elementos necesarios para componentes como:

- Menús desplegables.
- Barras de navegación plegables.
- Ventanas modales.
- Acordeones.
- Carruseles.

!!! salto-pagina-pdf ""

## 6.3. Contenedores

Bootstrap utiliza contenedores para limitar y centrar el contenido.

```html
<div class="container">
    <h1>FestWeb</h1>
</div>
```

Las clases principales son:

| Clase { .table-full-container .table-cl-secundario .table-bg-principal } | Comportamiento { .table-cl-secundario .table-bg-principal } |
|---|---|
| `.container` | Cambia su anchura máxima según el breakpoint. |
| `.container-fluid` | Ocupa siempre el 100 % de la anchura. |
| `.container-md` | Es fluido hasta alcanzar el breakpoint `md`. |

En FestWeb podemos utilizar:

```html
<main class="container py-4">
    <!-- Contenido principal -->
</main>
```

La utilidad `py-4` añade espaciado vertical.

!!! salto-pagina-pdf ""

## 6.4. Sistema de cuadrícula

La cuadrícula de Bootstrap se basa en:

1. Un contenedor.
2. Una fila `.row`.
3. Una o varias columnas `.col`.

```html
<div class="container">
    <div class="row">
        <div class="col">Evento 1</div>
        <div class="col">Evento 2</div>
        <div class="col">Evento 3</div>
    </div>
</div>
```

Bootstrap divide cada fila en **12 columnas virtuales**.

```html
<div class="row">
    <div class="col-8">Contenido principal</div>
    <div class="col-4">Contenido lateral</div>
</div>
```

En este caso:

- El contenido principal ocupa 8 de 12 columnas.
- El contenido lateral ocupa 4 de 12 columnas.

!!! salto-pagina-pdf ""

## 6.5. Cuadrícula responsive

Las clases de la cuadrícula siguen una estrategia mobile first.

```html
<div class="col-12 col-md-6 col-lg-4">
    <!-- Tarjeta -->
</div>
```

Este elemento ocupará:

- 12 columnas en móvil: una tarjeta por fila.
- 6 columnas desde `md`: dos tarjetas por fila.
- 4 columnas desde `lg`: tres tarjetas por fila.

Los breakpoints principales son:

| Prefijo { .table-full-container .table-cl-secundario .table-bg-principal } | Anchura mínima { .table-cl-secundario .table-bg-principal } |
|---|---:|
| Sin prefijo | Desde `0px` |
| `sm` | `576px` |
| `md` | `768px` |
| `lg` | `992px` |
| `xl` | `1200px` |
| `xxl` | `1400px` |

También podemos controlar directamente el número de elementos por fila:

```html
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
    <div class="col">Evento 1</div>
    <div class="col">Evento 2</div>
    <div class="col">Evento 3</div>
</div>
```

Las clases utilizadas indican:

- `row-cols-1`: una columna en móvil.
- `row-cols-md-2`: dos columnas desde `md`.
- `row-cols-lg-3`: tres columnas desde `lg`.
- `g-4`: separación entre filas y columnas.

## 6.6. Utilidades

Las utilidades son clases pequeñas que aplican una única función.

### Espaciado

```html
<section class="mt-4 mb-5 p-3">
```

- `m`: margen.
- `p`: relleno.
- `t`, `b`, `s`, `e`, `x`, `y`: lado o eje.
- `0` a `5`: nivel de espaciado.

Por ejemplo:

```html
<h2 class="mb-4">Próximos eventos</h2>
```

### Flexbox

```html
<div class="d-flex flex-column flex-md-row gap-3">
```

Este elemento:

- Utiliza Flexbox.
- Se organiza verticalmente en móvil.
- Cambia a una fila desde `md`.
- Mantiene una separación mediante `gap-3`.

### Alineación

```html
<div class="d-flex justify-content-between align-items-center">
```

### Tamaños y texto

```html
<a class="btn btn-primary w-100 text-center" href="#">
    Ver evento
</a>
```

Las utilidades deben utilizarse con moderación. Una acumulación excesiva de clases puede dificultar la lectura del HTML.

## 6.7. Componentes

Bootstrap incorpora componentes visuales preparados.

### Botones

```html
<a class="btn btn-primary" href="#">
    Ver evento
</a>

<button class="btn btn-outline-primary" type="button">
    Guardar
</button>
```

La clase `.btn` define el componente base y las demás clases establecen su variante.

### Tarjetas

Una tarjeta de FestWeb puede construirse así:

```html
<article class="card h-100">
    <img
        src="./src/assets/img01.png"
        class="card-img-top"
        alt="Escenario de un festival de música"
    >

    <div class="card-body d-flex flex-column">
        <p class="badge text-bg-primary align-self-start">
            Música
        </p>

        <h2 class="card-title h5">
            Festival Mediterráneo
        </h2>

        <p class="card-text">
            Valencia · 20 de junio
        </p>

        <p class="card-text">
            Una jornada de música en directo junto al mar.
        </p>

        <div class="d-flex gap-2 mt-auto">
            <a class="btn btn-primary" href="#">
                Ver evento
            </a>

            <button class="btn btn-outline-primary" type="button">
                Guardar
            </button>
        </div>
    </div>
</article>
```

En este ejemplo:

- `.card` crea la tarjeta.
- `.card-img-top` coloca la imagen.
- `.card-body` contiene la información.
- `.h-100` iguala la altura de las tarjetas.
- `.mt-auto` desplaza los botones hacia la parte inferior.

!!! salto-pagina-pdf ""

## 6.8. Personalización de FestWeb

No debemos editar directamente `bootstrap.min.css`.

Las personalizaciones se escribirán en nuestra hoja `estilos.css`, cargada después de Bootstrap.

```css
:root {
    --color-principal: #50c9e9;
    --color-secundario: #3b82e6;
    --color-fondo: #c6d8ff;
    --color-acento: #a3a313;
    --color-texto: #213fc2;
    --color-advertencia: #e8b718;
    --color-superficie: #ffffff;
}
```

Podemos crear una variante propia de botón:

```css
.btn-festweb {
    --bs-btn-color: var(--color-superficie);
    --bs-btn-bg: var(--color-texto);
    --bs-btn-border-color: var(--color-texto);
    --bs-btn-hover-color: var(--color-superficie);
    --bs-btn-hover-bg: var(--color-secundario);
    --bs-btn-hover-border-color: var(--color-secundario);
}
```

Y utilizarla en el HTML:

```html
<a class="btn btn-festweb" href="#">
    Ver evento
</a>
```

También podemos adaptar las imágenes de las tarjetas:

```css
.card-img-top {
    aspect-ratio: 16 / 10;
    object-fit: cover;
}
```

Bootstrap resuelve la estructura general, pero la guía de estilo de FestWeb debe seguir definiendo su identidad visual.

!!! salto-pagina-pdf ""

## 6.9. Bootstrap y CSS propio

Bootstrap resulta adecuado para:

- Crear rápidamente una cuadrícula responsive.
- Reutilizar componentes.
- Mantener separaciones coherentes.
- Desarrollar prototipos funcionales.
- Reducir la cantidad de CSS repetitivo.

El CSS propio sigue siendo necesario para:

- Aplicar la identidad visual.
- Crear componentes específicos.
- Ajustar comportamientos particulares.
- Evitar que la interfaz parezca genérica.
- Cumplir los requisitos concretos del proyecto.


## 6.10. Comprueba lo aprendido

Analiza el siguiente código:

```html
<div class="row row-cols-1 row-cols-md-2 row-cols-lg-3 g-4">
    <div class="col">
        <article class="card h-100">
            <!-- Contenido -->
        </article>
    </div>
</div>
```

Responde:

1. ¿Cuántas tarjetas se mostrarán por fila a `390px`?
2. ¿Cuántas se mostrarán a `800px`?
3. ¿Cuántas se mostrarán a `1200px`?
4. ¿Qué función desempeña la clase `g-4`?
5. ¿Por qué se utiliza `h-100` en la tarjeta?
6. ¿Por qué nuestra hoja CSS debe cargarse después de Bootstrap?

---

!!! salto-pagina-pdf ""