---
title: 7. Sass y organización de estilos
---

# 7. Sass y organización de estilos

Sass es un **preprocesador CSS** que incorpora herramientas para organizar, reutilizar y generar estilos.

Permite utilizar:

- Variables.
- Anidamiento.
- Archivos parciales.
- Módulos.
- Mixins.
- Funciones.
- Operaciones y estructuras de control.

El navegador no interpreta directamente los archivos Sass. Primero deben compilarse para generar un archivo CSS estándar.

```text
Archivos SCSS → Compilador Sass → Archivo CSS → Navegador
```

## 7.1. Sass y SCSS

Sass dispone de dos sintaxis:

| Sintaxis { .table-full-container .table-cl-secundario .table-bg-principal } | Extensión { .table-cl-secundario .table-bg-principal } | Características { .table-cl-secundario .table-bg-principal } |
|---|:---:|---|
| SCSS | `.scss` | Utiliza llaves y punto y coma, como CSS. |
| Sass | `.sass` | Utiliza sangrado y omite llaves y punto y coma. |

En esta unidad utilizaremos **SCSS**, porque cualquier código CSS válido también es código SCSS válido.

```scss
.tarjeta-evento {
    padding: 1.5rem;
    border-radius: 0.75rem;
}
```

!!! salto-pagina-pdf ""

## 7.2. Instalación y compilación

Crea o abre el proyecto desde una terminal e instala Sass:

```bash
npm install --save-dev sass
```

Organiza el proyecto de esta forma:

```text
festweb/
├── index.html
├── css/
│   └── estilos.css
├── scss/
│   └── estilos.scss
└── src/
    └── assets/
```

Para compilar el archivo:

```bash
npx sass scss/estilos.scss css/estilos.css
```

Para recompilar automáticamente cada vez que guardemos un cambio:

```bash
npx sass scss/estilos.scss css/estilos.css --watch
```

El HTML debe continuar enlazando el archivo CSS generado:

```html
<link rel="stylesheet" href="./css/estilos.css">
```

No debemos enlazar directamente el archivo `.scss`, ya que el navegador no lo interpreta.

## 7.3. Variables Sass

Las variables Sass comienzan con el símbolo `$`.

```scss
$color-principal: #50c9e9;
$color-secundario: #3b82e6;
$color-fondo: #c6d8ff;
$color-texto: #213fc2;
$color-superficie: #ffffff;

$espacio-md: 1rem;
$espacio-lg: 1.5rem;
$radio-md: 0.75rem;
```

Después podemos reutilizarlas:

```scss
.tarjeta-evento {
    padding: $espacio-lg;
    color: $color-texto;
    background-color: $color-superficie;
    border: 2px solid $color-principal;
    border-radius: $radio-md;
}
```

El CSS compilado contiene los valores resultantes:

```css
.tarjeta-evento {
    padding: 1.5rem;
    color: #213fc2;
    background-color: #ffffff;
    border: 2px solid #50c9e9;
    border-radius: 0.75rem;
}
```

### Variables Sass y propiedades personalizadas

No son exactamente lo mismo:

| Variable Sass { .table-full-container .table-cl-secundario .table-bg-principal } | Propiedad personalizada CSS { .table-cl-secundario .table-bg-principal } |
|---|---|
| Comienza con `$`. | Comienza con `--`. |
| Se resuelve durante la compilación. | Se conserva en el CSS. |
| No puede modificarse desde el navegador. | Puede cambiar durante la ejecución. |
| Ayuda a generar y organizar CSS. | Participa en la cascada y la herencia. |

Ambas pueden combinarse:

```scss
$color-principal: #50c9e9;
$color-texto: #213fc2;

:root {
    --color-principal: #{$color-principal};
    --color-texto: #{$color-texto};
}
```

El resultado será:

```css
:root {
    --color-principal: #50c9e9;
    --color-texto: #213fc2;
}
```

La construcción `#{}` se denomina **interpolación**.

## 7.4. Anidamiento

SCSS permite escribir selectores relacionados dentro de un mismo bloque.

```scss
.navegacion {
    display: flex;
    gap: 1rem;

    a {
        color: $color-texto;
        text-decoration: none;
    }
}
```

Sass genera:

```css
.navegacion {
    display: flex;
    gap: 1rem;
}

.navegacion a {
    color: #213fc2;
    text-decoration: none;
}
```

El símbolo `&` representa el selector actual.

```scss
.boton {
    padding: 0.75rem 1.25rem;

    &:hover {
        transform: translateY(-2px);
    }

    &:focus-visible {
        outline: 3px solid $color-principal;
    }

    &--principal {
        color: $color-superficie;
        background-color: $color-texto;
    }
}
```

El resultado incluye:

```css
.boton:hover {
    transform: translateY(-2px);
}

.boton:focus-visible {
    outline: 3px solid #50c9e9;
}

.boton--principal {
    color: #ffffff;
    background-color: #213fc2;
}
```

El anidamiento debe utilizarse con moderación. Si se anidan demasiados niveles se generan selectores largos y difíciles de mantener.

```scss
/* Debe evitarse */

.cabecera {
    .navegacion {
        div {
            ul {
                li {
                    a {
                        /* Demasiados niveles */
                    }
                }
            }
        }
    }
}
```

## 7.5. Archivos parciales y módulos

Cuando una hoja de estilos crece, podemos dividirla en archivos parciales.

Los archivos parciales comienzan con `_`:

```text
scss/
├── _variables.scss
├── _mixins.scss
├── _componentes.scss
└── estilos.scss
```

El guion bajo indica que el archivo forma parte de otro fichero y no debe compilarse por separado.

### Archivo de variables

```scss
// _variables.scss

$color-principal: #50c9e9;
$color-secundario: #3b82e6;
$color-fondo: #c6d8ff;
$color-texto: #213fc2;
$color-superficie: #ffffff;

$espacio-md: 1rem;
$espacio-lg: 1.5rem;
$radio-md: 0.75rem;

$breakpoint-md: 48rem;
$breakpoint-lg: 64rem;
```

### Utilización con `@use`

```scss
// _componentes.scss

@use "variables" as v;

.tarjeta-evento {
    padding: v.$espacio-lg;
    color: v.$color-texto;
    background-color: v.$color-superficie;
    border: 2px solid v.$color-principal;
    border-radius: v.$radio-md;
}
```

El archivo principal cargará los módulos:

```scss
// estilos.scss

@use "variables";
@use "mixins";
@use "componentes";
```

Para acceder a una variable se utiliza el espacio de nombres del módulo:

```scss
v.$color-principal
```

No se escribe la extensión `.scss` ni el guion bajo del archivo parcial.

!!! warning "Importante"

    No utilizaremos `@import` para cargar archivos Sass. El sistema actual se basa en `@use` y `@forward`.

!!! salto-pagina-pdf ""

## 7.6. Mixins

Un **mixin** almacena un conjunto de declaraciones reutilizables.

Se define con `@mixin` y se aplica con `@include`.

```scss
@mixin superficie {
    background-color: $color-superficie;
    border: 2px solid $color-principal;
    border-radius: $radio-md;
    box-shadow: 0 4px 12px rgb(33 63 194 / 15%);
}
```

Podemos reutilizarlo en diferentes componentes:

```scss
.tarjeta-evento {
    @include superficie;
}

.aviso {
    @include superficie;
}
```

### Mixins con parámetros

Los mixins también pueden recibir valores.

```scss
@mixin boton($fondo, $texto) {
    padding: 0.75rem 1.25rem;
    color: $texto;
    background-color: $fondo;
    border: 2px solid $fondo;
    border-radius: 0.5rem;
}
```

Después podemos generar distintas variantes:

```scss
.boton--principal {
    @include boton($color-texto, $color-superficie);
}

.boton--secundario {
    @include boton($color-superficie, $color-texto);
}
```

!!! salto-pagina-pdf ""

## 7.7. Mixin para media queries

Podemos encapsular los breakpoints de FestWeb en un mixin.

```scss
// _mixins.scss

@mixin desde($anchura) {
    @media (min-width: $anchura) {
        @content;
    }
}
```

El bloque `@content` representa las reglas incluidas al utilizar el mixin.

```scss
@use "variables" as v;
@use "mixins" as m;

.listado-eventos {
    display: grid;
    grid-template-columns: 1fr;
    gap: v.$espacio-lg;

    @include m.desde(v.$breakpoint-md) {
        grid-template-columns: repeat(2, 1fr);
    }

    @include m.desde(v.$breakpoint-lg) {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

Sass generará las media queries correspondientes en el archivo CSS.

## 7.8. Funciones

Una función Sass recibe valores y devuelve un resultado.

```scss
@use "sass:math";

@function convertir-rem($pixeles) {
    @return math.div($pixeles, 16) * 1rem;
}
```

Podemos utilizarla en cualquier propiedad:

```scss
.tarjeta-evento {
    padding: convertir-rem(24);
    border-radius: convertir-rem(12);
}
```

El CSS generado será:

```css
.tarjeta-evento {
    padding: 1.5rem;
    border-radius: 0.75rem;
}
```

La diferencia principal es:

- Un **mixin** genera un conjunto de declaraciones.
- Una **función** devuelve un valor.

## 7.9. Compilación para desarrollo y producción

Durante el desarrollo utilizaremos:

```bash
npx sass scss/estilos.scss css/estilos.css --watch
```

Para generar una versión comprimida:

```bash
npx sass scss/estilos.scss css/estilos.min.css \
    --style=compressed \
    --no-source-map
```

La versión comprimida reduce el tamaño del archivo, pero resulta más difícil de leer.

No debemos modificar manualmente el CSS generado, porque los cambios desaparecerán en la siguiente compilación.

El flujo correcto es:

```text
Modificar SCSS → Compilar → Generar CSS → Comprobar en el navegador
```

## 7.10. Sass y Bootstrap

Bootstrap puede utilizarse junto con una hoja Sass propia.

El orden será:

```html
<link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
>

<link rel="stylesheet" href="./css/estilos.css">
```

Nuestro archivo `estilos.css` será generado a partir de:

```text
scss/estilos.scss
```

De esta forma podemos:

- Utilizar la cuadrícula y los componentes de Bootstrap.
- Mantener la identidad visual de FestWeb.
- Organizar nuestros estilos mediante módulos.
- Crear mixins y funciones propias.
- Evitar modificar los archivos de Bootstrap.

## 7.11. Comprueba lo aprendido

Observa el siguiente código:

```scss
@use "variables" as v;
@use "mixins" as m;

.tarjeta-evento {
    padding: v.$espacio-md;

    @include m.desde(v.$breakpoint-md) {
        padding: v.$espacio-lg;
    }
}
```

Responde:

1. ¿Qué función tiene `@use "variables" as v`?
2. ¿Por qué se escribe `v.$espacio-md`?
3. ¿Qué diferencia existe entre una variable Sass y una propiedad personalizada CSS?
4. ¿Qué genera el mixin `m.desde()`?
5. ¿Qué archivo debe enlazarse desde el HTML?
6. ¿Por qué no debemos modificar directamente el CSS generado?

---