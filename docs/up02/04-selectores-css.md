---
title: Selectores CSS
---

Las declaraciones CSS indican qué apariencia debe tener un elemento. Sin embargo, antes de aplicar esas declaraciones, el navegador necesita saber **qué elementos debe seleccionar**.

Los selectores CSS son patrones que permiten localizar elementos dentro del DOM.

Por ejemplo:

```css
.event-card {
  padding: 1.5rem;
}
```

El selector `.event-card` indica que la declaración debe aplicarse a todos los elementos que contengan la clase `event-card`.

> **Pregunta de partida:**  
> ¿Cómo podemos aplicar un estilo a todas las tarjetas de FestWeb, modificar solamente sus títulos o cambiar la apariencia de un botón cuando el usuario sitúa el puntero sobre él?

## 3.1. Documento HTML de partida

Utilizaremos esta tarjeta de evento como referencia durante el apartado:

```html
<article class="event-card event-card--featured">
  <span class="event-card__category">
    Música
  </span>

  <h2 class="event-card__title">
    Festival SoundWave
  </h2>

  <p class="event-card__meta">
    18 de octubre · Valencia
  </p>

  <a
    class="button event-card__link"
    href="evento.html"
    data-type="featured"
  >
    Ver evento
  </a>
</article>
```

Cada selector nos permitirá localizar una parte diferente de esta estructura.

## 3.2. Selector universal

El selector universal se representa mediante un asterisco:

```css
* {
  box-sizing: border-box;
}
```

Selecciona todos los elementos del documento.

Resulta útil para aplicar determinados ajustes globales.

Por ejemplo:

```css
* {
  box-sizing: border-box;
}
```

Esta regla modifica la forma de calcular el tamaño de todas las cajas. Estudiaremos su funcionamiento en el apartado dedicado al modelo de caja.

También podemos seleccionar los elementos y sus pseudoelementos:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

El selector universal debe utilizarse con una finalidad concreta. Aplicar colores, tamaños o bordes a todos los elementos podría provocar efectos no deseados.

```css
/* Regla excesivamente general */
* {
  color: #213FC2;
  border: 1px solid #50C9E9;
}
```

El problema principal no es que el selector universal sea siempre lento, sino que puede afectar a elementos que no pretendíamos modificar.

## 3.3. Selector de etiqueta

El selector de etiqueta, también denominado selector de tipo, utiliza el nombre de un elemento HTML.

```css
body {
  color: #213FC2;
}
```

Esta regla selecciona el elemento `<body>`.

Podemos aplicar una misma presentación a todos los párrafos:

```css
p {
  line-height: 1.5;
}
```

O a todos los enlaces:

```css
a {
  color: #213FC2;
}
```

Los selectores de etiqueta se utilizan habitualmente para establecer estilos base:

```css
body {
  color: #213FC2;
  background-color: #C6D8FF;
}

h1,
h2,
h3 {
  line-height: 1.2;
}

img {
  max-width: 100%;
}
```

Debemos utilizarlos con cuidado cuando no queremos que todos los elementos del mismo tipo tengan la misma apariencia.

Por ejemplo:

```css
a {
  background-color: #50C9E9;
}
```

Esta regla modificaría todos los enlaces, aunque algunos formen parte del menú, otros de una tarjeta y otros del pie de página.

!!! salto-pagina-pdf ""

## 3.4. Selector de clase

El selector de clase comienza con un punto:

```css
.event-card {
  padding: 1.5rem;
}
```

Selecciona todos los elementos cuyo atributo `class` contiene `event-card`.

```html
<article class="event-card">
  ...
</article>
```

Una misma clase puede utilizarse en varios elementos:

```html
<article class="event-card">...</article>
<article class="event-card">...</article>
<article class="event-card">...</article>
```

Todos recibirán las mismas reglas:

```css
.event-card {
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
}
```

Las clases son la herramienta principal para construir componentes reutilizables.

### Varias clases en un elemento

Un elemento puede contener varias clases separadas mediante espacios:

```html
<article class="event-card event-card--featured">
  ...
</article>
```

En este caso, el elemento pertenece a dos clases:

- `event-card`
- `event-card--featured`

Podemos aplicar estilos generales mediante la primera clase y añadir una variante mediante la segunda.

```css
.event-card {
  border: 2px solid #50C9E9;
}

.event-card--featured {
  border-color: #E8B718;
}
```

La clase modificadora no sustituye a la clase principal. Ambas se aplican sobre el mismo elemento.

## 3.5. Selector de identificador

El selector de identificador comienza con una almohadilla:

```css
#main-header {
  background-color: #C6D8FF;
}
```

Selecciona el elemento cuyo atributo `id` coincide con el nombre indicado:

```html
<header id="main-header">
  ...
</header>
```

Un identificador debe ser único dentro del documento.

El siguiente código no sería correcto:

```html
<header id="main-header">...</header>
<section id="main-header">...</section>
```

### ¿Cuándo utilizar un identificador?

Los identificadores pueden resultar útiles para:

- Crear enlaces internos.
- Relacionar etiquetas y campos de formulario.
- Identificar regiones concretas.
- Localizar elementos desde JavaScript.

```html
<label for="email">Correo electrónico</label>
<input id="email" type="email">
```

También pueden utilizarse como destino de un enlace:

```html
<a href="#featured-events">
  Ir a eventos destacados
</a>

<section id="featured-events">
  ...
</section>
```

Aunque CSS permite seleccionar identificadores, normalmente evitaremos utilizarlos para aplicar estilos.

Los selectores de identificador tienen una especificidad elevada y dificultan la reutilización y posterior redefinición.

```css
/* Menos reutilizable */
#featured-card {
  border-color: #E8B718;
}
```

Es preferible utilizar una clase:

```css
/* Más reutilizable */
.event-card--featured {
  border-color: #E8B718;
}
```

## 3.6. Agrupación de selectores

Podemos aplicar las mismas declaraciones a varios selectores separándolos mediante comas:

```css
h1,
h2,
h3 {
  color: #213FC2;
  line-height: 1.2;
}
```

Sin agrupación tendríamos que repetir las declaraciones:

```css
h1 {
  color: #213FC2;
  line-height: 1.2;
}

h2 {
  color: #213FC2;
  line-height: 1.2;
}

h3 {
  color: #213FC2;
  line-height: 1.2;
}
```

La agrupación reduce la repetición, pero debemos utilizarla únicamente cuando los elementos comparten realmente la misma presentación.

También podemos agrupar clases:

```css
.button,
.event-card__link {
  font-weight: 600;
  text-decoration: none;
}
```

## 3.7. Selectores de atributo

Los selectores de atributo permiten localizar elementos según la presencia o el valor de sus atributos.

Se escriben entre corchetes.

### Existencia de un atributo

```css
[required] {
  border-left: 0.25rem solid #E8B718;
}
```

Selecciona todos los elementos que contienen el atributo `required`.

```html
<input type="text" required>
```

### Coincidencia exacta

```css
input[type="email"] {
  background-color: #C6D8FF;
}
```

Selecciona los elementos `<input>` cuyo atributo `type` tiene exactamente el valor `email`.

### El valor comienza por una cadena

```css
a[href^="https"] {
  font-weight: 600;
}
```

El operador `^=` significa «comienza por».

Seleccionará enlaces como:

```html
<a href="https://example.com">
  Sitio externo
</a>
```

### El valor termina en una cadena

```css
a[href$=".pdf"] {
  color: #213FC2;
}
```

El operador `$=` significa «termina en».

Seleccionará enlaces como:

```html
<a href="programa-festival.pdf">
  Descargar programa
</a>
```

### El valor contiene una cadena

```css
[class*="event-card"] {
  border-radius: 0.75rem;
}
```

El operador `*=` significa «contiene».

Esta regla seleccionaría clases como:

- `event-card`
- `event-card__title`
- `event-card--featured`

Debe utilizarse con cuidado, ya que también podría coincidir con nombres que contengan accidentalmente la misma cadena.

!!! salto-pagina-pdf ""

### Resumen de operadores

| Selector { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `[atributo]` | El atributo está presente |
| `[atributo="valor"]` | Coincidencia exacta |
| `[atributo^="valor"]` | El valor comienza por la cadena |
| `[atributo$="valor"]` | El valor termina en la cadena |
| `[atributo*="valor"]` | El valor contiene la cadena |

### Atributos personalizados

Podemos utilizar atributos personalizados que comienzan por `data-`.

```html
<a
  class="button"
  href="evento.html"
  data-type="featured"
>
  Ver evento
</a>
```

Podemos seleccionar el elemento mediante:

```css
[data-type="featured"] {
  border-color: #E8B718;
}
```

Los atributos `data-` también pueden ser consultados desde JavaScript.

## 3.8. Selectores compuestos

Podemos combinar varios selectores sin dejar espacios entre ellos.

```css
a.button {
  text-decoration: none;
}
```

Este selector localiza únicamente elementos `<a>` que también contienen la clase `button`.

```html
<a class="button" href="evento.html">
  Ver evento
</a>
```

No seleccionaría este botón:

```html
<button class="button">
  Guardar evento
</button>
```

También podemos exigir que un elemento contenga dos clases:

```css
.event-card.event-card--featured {
  border-color: #E8B718;
}
```

Selecciona elementos que contengan simultáneamente ambas clases.

```html
<article class="event-card event-card--featured">
  ...
</article>
```

No debemos confundirlo con:

```css
.event-card .event-card--featured {
  border-color: #E8B718;
}
```

El espacio indica que `.event-card--featured` debe encontrarse dentro de `.event-card`.

## 3.9. Combinadores

Los combinadores expresan relaciones entre elementos del DOM.

| Combinador { .table-full-container .table-cl-secundario .table-bg-principal } | Relación { .table-cl-secundario .table-bg-principal } | Ejemplo { .table-cl-secundario .table-bg-principal } |
|:---:|---|---|
| Espacio | Descendiente | `.event-card a` |
| `>` | Hijo directo | `.event-card > h2` |
| `+` | Hermano adyacente | `h2 + p` |
| `~` | Hermanos posteriores | `h2 ~ p` |

### Descendiente

El espacio selecciona elementos situados dentro de otro elemento, sin importar el nivel de profundidad.

```css
.event-card a {
  color: #213FC2;
}
```

Selecciona todos los enlaces que se encuentren dentro de una tarjeta.

```html
<article class="event-card">
  <div>
    <a href="evento.html">Ver evento</a>
  </div>
</article>
```

El enlace es descendiente de `.event-card`, aunque no sea su hijo directo.

### Hijo directo

El combinador `>` selecciona únicamente los hijos inmediatos.

```css
.event-card > h2 {
  margin-top: 0;
}
```

Seleccionará este título:

```html
<article class="event-card">
  <h2>Festival SoundWave</h2>
</article>
```

No seleccionará el título si se encuentra dentro de otro contenedor:

```html
<article class="event-card">
  <header>
    <h2>Festival SoundWave</h2>
  </header>
</article>
```

En este segundo caso, `<h2>` es descendiente de `<article>`, pero no su hijo directo.

### Hermano adyacente

El combinador `+` selecciona el primer elemento situado inmediatamente después de otro, siempre que compartan el mismo padre.

```css
.event-card__title + .event-card__meta {
  margin-top: 0;
}
```

Se aplicará a `.event-card__meta` cuando aparezca inmediatamente después del título:

```html
<h2 class="event-card__title">
  Festival SoundWave
</h2>

<p class="event-card__meta">
  18 de octubre · Valencia
</p>
```

### Hermanos generales

El combinador `~` selecciona los hermanos posteriores que comparten el mismo padre.

```css
.event-card__title ~ p {
  color: #213FC2;
}
```

Seleccionará todos los párrafos situados después del título dentro del mismo contenedor.

## 3.10. Pseudoclases

Una pseudoclase selecciona un elemento existente cuando se encuentra en un estado determinado o cumple una condición.

Las pseudoclases comienzan con dos puntos:

```css
.button:hover {
  border-color: #3B82E6;
}
```

### `:hover`

Se activa cuando el puntero se encuentra sobre el elemento.

```css
.button:hover {
  background-color: #50C9E9;
  border-color: #3B82E6;
}
```

No debemos depender exclusivamente de `:hover`, porque algunos dispositivos no utilizan ratón.

### `:focus`

Selecciona el elemento que ha recibido el foco.

```css
.button:focus {
  outline: 3px solid #E8B718;
  outline-offset: 3px;
}
```

El foco permite saber qué elemento está seleccionado durante la navegación mediante teclado.

### `:focus-visible`

Selecciona el elemento cuando el navegador determina que el indicador de foco debe mostrarse de forma visible.

```css
.button:focus-visible {
  outline: 3px solid #E8B718;
  outline-offset: 3px;
}
```

Normalmente resulta más adecuado que eliminar el contorno:

```css
/* No recomendado */
.button:focus {
  outline: none;
}
```

Si eliminamos el indicador de foco, debemos proporcionar una alternativa claramente visible.

### `:active`

Se aplica durante la activación del elemento.

```css
.button:active {
  transform: translateY(1px);
}
```

En un botón, representa normalmente el instante durante el que está siendo pulsado.

### `:visited`

Selecciona los enlaces que ya han sido visitados.

```css
a:visited {
  color: #A3A313;
}
```

Los navegadores limitan las propiedades que pueden modificarse mediante `:visited` para proteger la privacidad del usuario.

!!! salto-pagina-pdf ""

### Pseudoclases de formulario

```css
input:required {
  border-left: 0.25rem solid #E8B718;
}

input:checked {
  accent-color: #3B82E6;
}

input:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}

input:valid {
  border-color: #A3A313;
}

input:invalid {
  border-color: #E8B718;
}
```

Estas pseudoclases permiten representar estados del formulario sin añadir nuevas clases manualmente.

### Pseudoclases estructurales

#### Primer hijo

```css
.event-list > article:first-child {
  border-color: #E8B718;
}
```

Selecciona el artículo si es el primer hijo de su contenedor.

#### Último hijo

```css
.event-list > article:last-child {
  margin-bottom: 0;
}
```

#### Posición determinada

```css
.event-list > article:nth-child(2) {
  background-color: #C6D8FF;
}
```

También podemos utilizar palabras clave o fórmulas:

```css
/* Posiciones pares */
.event-list > article:nth-child(even) {
  background-color: #C6D8FF;
}

/* Posiciones impares */
.event-list > article:nth-child(odd) {
  background-color: #ffffff;
}

/* Cada tercer elemento */
.event-list > article:nth-child(3n) {
  border-color: #A3A313;
}
```

### Negación con `:not()`

La pseudoclase `:not()` selecciona los elementos que no coinciden con el selector indicado.

```css
.main-navigation a:not(.button) {
  text-decoration: underline;
}
```

Seleccionará los enlaces de la navegación que no tengan la clase `button`.

Debe escribirse sin espacio entre `:not` y los paréntesis.

```css
/* Correcto */
:not(.button)

/* Incorrecto */
:not (.button)
```

## 3.11. Pseudoelementos

Los pseudoelementos permiten seleccionar una parte concreta de un elemento o generar una caja visual que no aparece como una etiqueta independiente en el HTML.

Se escriben habitualmente mediante dos puntos dobles:

```css
.event-card__link::after {
  content: " →";
}
```

### `::before`

Genera contenido antes del contenido del elemento.

```css
.event-card__category::before {
  content: "★ ";
  color: #E8B718;
}
```

### `::after`

Genera contenido después del contenido del elemento.

```css
.event-card__link::after {
  content: " →";
}
```

Los pseudoelementos `::before` y `::after` necesitan normalmente la propiedad `content`.

### `::first-letter`

Selecciona la primera letra de un bloque de texto.

```css
.event-description::first-letter {
  color: #213FC2;
  font-size: 2rem;
  font-weight: 700;
}
```

### `::placeholder`

Selecciona el texto de ayuda de un campo de formulario.

```css
input::placeholder {
  color: #213FC2;
  opacity: 0.7;
}
```

### `::selection`

Permite modificar la apariencia del texto seleccionado por el usuario.

```css
::selection {
  color: #213FC2;
  background-color: #50C9E9;
}
```

### Contenido y accesibilidad

El contenido esencial no debe añadirse únicamente mediante `::before` o `::after`.

Por ejemplo, no deberíamos utilizar:

```css
.price::after {
  content: "Entrada agotada";
}
```

Si «Entrada agotada» es información importante, debe formar parte del HTML:

```html
<p class="event-card__availability">
  Entrada agotada
</p>
```

Los pseudoelementos resultan más adecuados para elementos decorativos o complementarios.

## 3.12. Pseudoclase frente a pseudoelemento

| Característica { .table-full-container .table-cl-secundario .table-bg-principal } | Pseudoclase { .table-cl-secundario .table-bg-principal } | Pseudoelemento { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| Sintaxis habitual | Un punto doble `:` | Dos puntos dobles `::` |
| Selecciona | Un estado o condición | Una parte o caja virtual |
| Ejemplo | `:hover` | `::before` |
| Elemento existente | Sí | Selecciona o genera una parte |
| Uso | Interacción y estructura | Presentación parcial o decorativa |

Ejemplo combinado:

```css
.button:hover::after {
  content: " →";
}
```

Esta regla genera un pseudoelemento después del contenido del botón cuando el botón se encuentra en estado `:hover`.

!!! salto-pagina-pdf ""

## 3.13. Cómo leer un selector complejo

Consideremos este selector:

```css
.event-card > .event-card__content a.button:hover
```

Podemos interpretarlo de derecha a izquierda:

1. Selecciona un elemento con la clase `.button`.
2. Debe ser un enlace `<a>`.
3. Debe encontrarse en estado `:hover`.
4. Debe estar dentro de `.event-card__content`.
5. `.event-card__content` debe ser hijo directo de `.event-card`.

Aunque CSS permite crear selectores muy largos, no siempre son recomendables.

```css
main section article div a.button:hover {
  ...
}
```

Este selector depende demasiado de la estructura del HTML. Si añadimos o eliminamos un contenedor, podría dejar de funcionar.

Es preferible utilizar clases reutilizables:

```css
.button:hover {
  ...
}
```

O un contexto breve cuando sea necesario:

```css
.event-card .button:hover {
  ...
}
```

!!! salto-pagina-pdf ""

## 3.14. Ejemplo completo de FestWeb

### HTML

```html
<section class="event-list">
  <article class="event-card event-card--featured">
    <span class="event-card__category">
      Música
    </span>

    <h2 class="event-card__title">
      Festival SoundWave
    </h2>

    <p class="event-card__meta">
      18 de octubre · Valencia
    </p>

    <a
      class="button event-card__link"
      href="evento.html"
      data-type="featured"
    >
      Ver evento
    </a>
  </article>
</section>
```

!!! salto-pagina-pdf ""

### CSS

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

.event-card {
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.75rem;
}

.event-card--featured {
  border-color: #E8B718;
}

.event-card__category {
  font-weight: 600;
}

.event-card__category::before {
  content: "★ ";
  color: #E8B718;
}

.event-card__title + .event-card__meta {
  margin-top: 0;
}

.button {
  display: inline-block;
  padding: 0.75rem 1rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.5rem;
  font-weight: 600;
  text-decoration: none;
}

.button:hover {
  background-color: #50C9E9;
  border-color: #3B82E6;
}

.button:focus-visible {
  outline: 3px solid #E8B718;
  outline-offset: 3px;
}

[data-type="featured"]::after {
  content: " →";
}
```

Este ejemplo combina:

- Selector universal.
- Selectores de clase.
- Clases modificadoras.
- Selector de atributo.
- Combinador hermano adyacente.
- Pseudoclases.
- Pseudoelementos.
- Agrupación de selectores.

---

> **Un buen selector identifica los elementos necesarios sin depender más de lo imprescindible de la estructura del documento.**

!!! salto-pagina-pdf ""