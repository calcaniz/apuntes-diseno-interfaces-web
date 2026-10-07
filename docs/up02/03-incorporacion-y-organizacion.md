---
title: Incorporación y organización de estilos
---

Una vez comprendida la función de CSS, debemos decidir dónde escribiremos las reglas y cómo las relacionaremos con el documento HTML.

CSS puede incorporarse de tres formas principales:

1. Mediante estilos en línea.
2. Mediante una hoja de estilos interna.
3. Mediante una hoja de estilos externa.

Las tres modalidades son válidas para el navegador, pero no ofrecen las mismas posibilidades de reutilización, mantenimiento y organización.

> **Pregunta de partida:**  
> Si queremos cambiar el color de todos los botones de FestWeb, ¿es mejor modificar cada botón por separado o centralizar la decisión en un único lugar?

## 2.1. Estilos en línea

Los estilos en línea se escriben dentro del atributo `style` de un elemento HTML.

```html
<h2 style="color: #213FC2;">
  Festival SoundWave
</h2>
```

El atributo contiene una o varias declaraciones CSS separadas mediante punto y coma.

```html
<article
  style="padding: 1.5rem;
    color: #213FC2;
    background-color: #C6D8FF;
    border: 2px solid #50C9E9;"
>
  Festival SoundWave
</article>
```

Estas declaraciones solo afectan al elemento en el que se ha incluido el atributo.

### Ventajas

- Permiten probar rápidamente una propiedad.
- No necesitan crear una hoja de estilos.
- Pueden utilizarse para valores generados dinámicamente.
- Resultan útiles en determinados correos HTML.

### Inconvenientes

- Mezclan la estructura con la presentación.
- Obligan a repetir declaraciones.
- Dificultan los cambios globales.
- No permiten reutilizar estilos.
- Aumentan el tamaño del documento HTML.
- Dificultan el mantenimiento.
- No permiten crear reglas con pseudoclases como `:hover` o `:focus`.

Por ejemplo, mediante el atributo `style` podemos definir el color inicial de un enlace:

```html
<a
  href="evento.html"
  style="color: #213FC2;"
>
  Ver evento
</a>
```

Sin embargo, no podemos escribir directamente una regla como esta dentro del atributo:

```css
a:hover {
  color: #3B82E6;
}
```

Las pseudoclases necesitan formar parte de una regla CSS completa.

> **Importante:**  
> Los estilos en línea pueden resultar útiles en casos concretos, pero no deberían utilizarse como sistema principal de presentación de una aplicación web.

!!! salto-pagina-pdf ""

## 2.2. Hoja de estilos interna

Una hoja de estilos interna se escribe mediante el elemento `<style>`.

Este elemento suele situarse dentro de `<head>`.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>FestWeb</title>

  <style>
    .event-card {
      padding: 1.5rem;
      color: #213FC2;
      background-color: #C6D8FF;
      border: 2px solid #50C9E9;
      border-radius: 0.75rem;
    }
  </style>
</head>

<body>
  <article class="event-card">
    <h2>Festival SoundWave</h2>
    <p>18 de octubre · Valencia</p>
  </article>
</body>
</html>
```

En este caso, las reglas pueden aplicarse a cualquier elemento del documento que coincida con sus selectores.

### Ventajas

- Mantienen las reglas separadas del contenido de `<body>`.
- Permiten reutilizar estilos dentro del mismo documento.
- Admiten selectores, pseudoclases y pseudoelementos.
- Son útiles para realizar ejemplos y prototipos rápidos.
- No requieren cargar un archivo CSS independiente.

!!! salto-pagina-pdf ""

### Inconvenientes

- Las reglas solamente están disponibles en ese documento.
- Si varias páginas necesitan los mismos estilos, habrá que copiarlos.
- Los cambios deben repetirse en cada archivo HTML.
- El documento puede crecer demasiado.
- Dificultan mantener una apariencia coherente en sitios con varias páginas.

Una hoja interna puede ser apropiada para:

- Una demostración sencilla.
- Una actividad breve.
- Una prueba aislada.
- Un documento HTML independiente.

No será la opción principal para FestWeb, porque sus páginas deben compartir los mismos colores, tipografías y componentes.

## 2.3. Hoja de estilos externa

Una hoja de estilos externa almacena las reglas en un archivo independiente con extensión `.css`.

Por ejemplo:

```text
styles.css
```

El documento HTML debe enlazar ese archivo mediante el elemento `<link>`.

```html
<head>
  <meta charset="UTF-8">
  <title>FestWeb</title>

  <link rel="stylesheet" href="css/styles.css">
</head>
```

El atributo `rel="stylesheet"` indica que el recurso enlazado es una hoja de estilos.

El atributo `href` contiene la ruta del archivo CSS.

El archivo `styles.css` puede contener las reglas:

```css
.event-card {
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.75rem;
}
```

El documento HTML solo contiene la estructura:

```html
<article class="event-card">
  <h2>Festival SoundWave</h2>
  <p>18 de octubre · Valencia</p>
</article>
```

### Ventajas

- Separa completamente la estructura y la presentación.
- Permite utilizar los mismos estilos en varias páginas.
- Centraliza los cambios.
- Facilita el trabajo colaborativo.
- Reduce la repetición.
- Permite organizar mejor el código.
- El navegador puede almacenar el archivo CSS en caché.

### Inconvenientes

- Requiere enlazar correctamente el archivo.
- Una ruta incorrecta impide cargar los estilos.
- El navegador debe solicitar inicialmente el recurso.
- Un error en una hoja compartida puede afectar a varias páginas.

La hoja externa es la opción habitual para proyectos web compuestos por diferentes páginas.

## 2.4. Reutilización entre páginas

Imaginemos que FestWeb contiene los siguientes documentos:

- Página de inicio.
- Listado de eventos.
- Detalle de un evento.
- Página de favoritos.

Todas las páginas pueden utilizar la misma hoja de estilos.

```html
<link rel="stylesheet" href="css/styles.css">
```

Si modificamos una regla en `styles.css`, el cambio se aplicará a todos los documentos enlazados.

Por ejemplo:

```css
.event-card {
  border-radius: 1rem;
}
```

Todas las tarjetas que utilicen la clase `.event-card` recibirán el nuevo redondeo, independientemente de la página en la que aparezcan.

Esta reutilización permite trasladar la guía de estilo de FestWeb a toda la aplicación.

## 2.5. Comparación de las modalidades

| Modalidad { .table-full-container .table-cl-secundario .table-bg-principal } | Ubicación { .table-cl-secundario .table-bg-principal } | Reutilización { .table-cl-secundario .table-bg-principal } | Uso recomendado { .table-cl-secundario .table-bg-principal } |
|---|---|---|---|
| En línea | Atributo `style` | Un único elemento | Casos muy concretos o valores dinámicos |
| Interna | Elemento `<style>` | Un documento HTML | Pruebas, ejemplos o páginas independientes |
| Externa | Archivo `.css` | Varias páginas | Proyectos web y aplicaciones |

Para FestWeb utilizaremos principalmente una **hoja de estilos externa**.

Los estilos en línea y las hojas internas se utilizarán inicialmente para comprender sus diferencias y limitaciones.

!!! salto-pagina-pdf ""

## 2.6. Rutas hacia una hoja de estilos

Para cargar una hoja externa debemos indicar correctamente su ubicación.

Supongamos esta estructura:

```text
festweb/
├── index.html
├── eventos.html
├── css/
│   └── styles.css
└── images/
    └── festival.jpg
```

Desde `index.html`, la hoja se enlaza así:

```html
<link rel="stylesheet" href="css/styles.css">
```

La ruta indica que el navegador debe:

1. Partir de la carpeta donde se encuentra `index.html`.
2. Entrar en la carpeta `css`.
3. Cargar el archivo `styles.css`.

Si HTML y CSS se encuentran en la misma carpeta, bastará con indicar el nombre:

```html
<link rel="stylesheet" href="styles.css">
```

Si escribimos una ruta incorrecta, el navegador mostrará el documento HTML, pero no aplicará los estilos.

```html
<!-- Ruta incorrecta si no existe la carpeta estilos -->
<link rel="stylesheet" href="estilos/styles.css">
```

!!! salto-pagina-pdf ""

## 2.7. Cómo comprobar si la hoja se ha cargado

Si los estilos no aparecen, podemos realizar estas comprobaciones:

1. Verificar que el archivo termina en `.css`.
2. Comprobar el nombre exacto del archivo.
3. Revisar las mayúsculas y minúsculas.
4. Revisar la ruta indicada en `href`.
5. Confirmar que `<link>` se encuentra dentro de `<head>`.
6. Abrir las herramientas de desarrollo del navegador.
7. Revisar la pestaña de red o *Network*.
8. Comprobar si aparece un error `404`.

También podemos introducir temporalmente una regla muy visible:

```css
body {
  background-color: red;
}
```

Si el fondo no cambia, probablemente la hoja no se ha cargado.

Esta regla debe eliminarse una vez realizada la comprobación.

## 2.8. Varias hojas de estilo

Un documento puede enlazar más de una hoja CSS.

```html
<link rel="stylesheet" href="css/base.css">
<link rel="stylesheet" href="css/components.css">
```

El navegador procesa las hojas en el orden en el que aparecen.

Cuando dos reglas tienen la misma prioridad y especificidad, una regla cargada posteriormente puede reemplazar a otra anterior.

```html
<link rel="stylesheet" href="css/base.css">
<link rel="stylesheet" href="css/custom.css">
```

En este caso, `custom.css` se procesa después de `base.css`.

El orden de las hojas forma parte de la cascada, que estudiaremos con más detalle en un apartado posterior.

En proyectos pequeños no es necesario dividir el código en muchos archivos. Una única hoja bien organizada puede resultar más clara.

## 2.9. Organización inicial del archivo CSS

Aunque CSS permite escribir las reglas en cualquier orden, conviene establecer una estructura predecible.

Una primera organización puede ser:

```css
/* ========================================
   1. Propiedades personalizadas
   ======================================== */

/* ========================================
   2. Ajustes globales
   ======================================== */

/* ========================================
   3. Tipografía
   ======================================== */

/* ========================================
   4. Componentes
   ======================================== */

/* ========================================
   5. Utilidades
   ======================================== */
```

Todavía no conocemos todos estos conceptos, pero utilizaremos esta estructura progresivamente.

### Propiedades personalizadas

Contendrán las decisiones generales de la guía de estilo:

```css
:root {
  --color-principal: #50C9E9;
  --color-secundario: #3B82E6;
  --color-fondo: #C6D8FF;
  --color-acento: #A3A313;
  --color-texto: #213FC2;
  --color-advertencia: #E8B718;
}
```

!!! salto-pagina-pdf ""

### Ajustes globales

Afectarán a todo el documento:

```css
body {
  color: #213FC2;
  background-color: #C6D8FF;
}
```

### Tipografía

Agruparán las reglas relacionadas con títulos y textos:

```css
h1,
h2,
h3 {
  line-height: 1.2;
}
```

### Componentes

Contendrán elementos reutilizables:

```css
.button {
  padding: 0.75rem 1rem;
}

.event-card {
  padding: 1.5rem;
}
```

### Utilidades

Contendrán clases sencillas con una única finalidad:

```css
.text-center {
  text-align: center;
}

.is-hidden {
  display: none;
}
```

!!! salto-pagina-pdf ""

## 2.10. Formato del código

Una hoja de estilos debe ser legible.

Es recomendable:

- Escribir una declaración por línea.
- Mantener una sangría uniforme.
- Utilizar espacios de forma coherente.
- Separar las reglas mediante líneas en blanco.
- Finalizar las declaraciones con punto y coma.
- Utilizar comentarios para identificar secciones.
- Evitar líneas excesivamente largas.

### Código difícil de leer

```css
.event-card{padding:1.5rem;color:#213FC2;background-color:#C6D8FF;border:2px solid #50C9E9;}
```

### Código organizado

```css
.event-card {
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
}
```

Ambas reglas producen el mismo resultado, pero la segunda resulta más fácil de leer, revisar y modificar.

## 2.11. Nombres comprensibles

Los nombres de las clases deben describir la función del elemento.

### Nombre poco recomendable

```css
.caja-azul {
  background-color: #3B82E6;
}
```

El nombre depende de una característica visual que podría cambiar.

### Nombre más adecuado

```css
.event-card {
  background-color: #C6D8FF;
}
```

La clase identifica el componente, no su color actual.

También debemos evitar nombres sin significado:

```css
.caja1
.elemento2
.texto-grande-azul
```

Es preferible utilizar nombres como:

```css
.event-card
.event-card__title
.button
.warning-message
.main-navigation
```

Estudiaremos con más detalle la creación de clases y la convención BEM en el apartado dedicado a los componentes reutilizables.

!!! salto-pagina-pdf ""

## 2.12. Ejemplo completo de FestWeb

La estructura del proyecto puede quedar así:

```text
festweb/
├── index.html
└── css/
    └── styles.css
```

### `index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
  >

  <title>FestWeb</title>

  <link rel="stylesheet" href="css/styles.css">
</head>

<body>
  <main>
    <article class="event-card">
      <h1 class="event-card__title">
        Festival SoundWave
      </h1>

      <p class="event-card__meta">
        18 de octubre · Valencia
      </p>

      <a class="event-card__link" href="evento.html">
        Ver evento
      </a>
    </article>
  </main>
</body>
</html>
```

!!! salto-pagina-pdf ""

### `css/styles.css`

```css
/* ========================================
   Estilos generales de FestWeb
   ======================================== */

body {
  color: #213FC2;
  background-color: #C6D8FF;
}

/* ========================================
   Tarjeta de evento
   ======================================== */

.event-card {
  padding: 1.5rem;
  border: 2px solid #50C9E9;
  border-radius: 0.75rem;
}

.event-card__title {
  margin-top: 0;
}

.event-card__link {
  color: #213FC2;
  font-weight: 600;
}
```

HTML contiene la estructura y CSS contiene la presentación.

Esta separación nos permitirá modificar posteriormente los colores, los espacios o la apariencia de las tarjetas sin alterar el contenido.

> **Una hoja de estilos externa permite convertir las decisiones visuales de FestWeb en un sistema centralizado, reutilizable y fácil de mantener.**

!!! salto-pagina-pdf ""