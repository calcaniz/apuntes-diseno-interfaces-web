---
title: Introducción a CSS
---

# 1. Introducción a CSS

Una página web puede contener información correctamente organizada y, sin embargo, resultar difícil de utilizar si no presenta una jerarquía visual clara.

HTML permite definir títulos, párrafos, imágenes, enlaces, formularios y otros elementos. No obstante, para decidir cómo deben mostrarse necesitamos utilizar **CSS**.

CSS corresponde a las siglas de *Cascading Style Sheets*, que puede traducirse como **hojas de estilo en cascada**.

Su función consiste en describir la presentación visual de los documentos HTML.

Mediante CSS podemos controlar, entre otros aspectos:

- Los colores.
- Las tipografías.
- El tamaño de los elementos.
- Los márgenes y rellenos.
- Los fondos y bordes.
- La alineación.
- La visibilidad.
- La adaptación a diferentes pantallas.
- Los estados visuales de los elementos interactivos.

> **Pregunta de partida:**  
> Si HTML ya permite crear títulos, párrafos, botones e imágenes, ¿por qué necesitamos otro lenguaje para controlar su apariencia?

!!! salto-pagina-pdf ""

## 1.1. Estructura, presentación y comportamiento

En el desarrollo web se separan tres responsabilidades principales:

| Tecnología { .table-full-container .table-cl-secundario .table-bg-principal } | Responsabilidad { .table-cl-secundario .table-bg-principal } | Pregunta a la que responde { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| **HTML** | Estructura y contenido | ¿Qué información contiene la página? |
| **CSS** | Presentación visual | ¿Cómo se muestra esa información? |
| **JavaScript** | Comportamiento e interacción | ¿Cómo reacciona la página? |

### HTML: estructura y contenido

HTML define el significado y la organización de la información.

Por ejemplo:

```html
<article class="event-card">
  <h2>Festival SoundWave</h2>
  <p>18 de octubre · Valencia</p>
  <a href="evento.html" target="_blank" rel="noopener noreferrer">Ver evento</a>
</article>
```

Este fragmento indica que existe:

- Un artículo.
- Un título.
- Un párrafo con información.
- Un enlace hacia otra página.

El navegador puede mostrar estos elementos, pero HTML no determina todavía la identidad visual de FestWeb.

!!! salto-pagina-pdf ""

### CSS: presentación

CSS permite decidir cómo deben representarse esos elementos.

```css
.event-card {
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.75rem;
}
```

La estructura HTML no ha cambiado. Únicamente hemos definido su apariencia.

### JavaScript: comportamiento

JavaScript permite añadir comportamiento e interacción.

Por ejemplo, podría utilizarse para:

- Guardar un evento como favorito.
- Filtrar los eventos por categoría.
- Cargar nuevos eventos desde un servidor.
- Mostrar u ocultar información.
- Actualizar una parte de la página sin recargarla.

```javascript
const card = document.querySelector(".event-card");

card.addEventListener("click", () => {
  console.log("Se ha seleccionado el evento");
});
```

Cada tecnología tiene una responsabilidad diferente, aunque las tres trabajan conjuntamente.

!!! salto-pagina-pdf ""

## 1.2. ¿Por qué debemos separar HTML y CSS?

Podríamos modificar la apariencia escribiendo estilos directamente dentro de cada elemento HTML:

```html
<h2 style="color: #213FC2; font-size: 2rem;">
  Festival SoundWave
</h2>
```

Este código funciona, pero presenta varios problemas:

- Mezcla el contenido con la presentación.
- Obliga a repetir las mismas propiedades.
- Dificulta realizar cambios globales.
- Reduce la reutilización.
- Complica el mantenimiento.
- Aumenta la posibilidad de crear estilos incoherentes.

Imaginemos que FestWeb contiene cincuenta tarjetas de evento y queremos modificar el color de todos sus títulos.

Si el estilo está escrito en cada elemento, deberemos modificar cincuenta fragmentos diferentes. Si utilizamos una regla CSS común, solamente tendremos que cambiar una declaración.

```css
.event-card__title {
  color: #213FC2;
}
```

Todos los títulos que utilicen esa clase recibirán el mismo estilo.

> **Idea clave:**  
> CSS no solo permite decorar una página. También permite centralizar decisiones visuales y aplicarlas de forma coherente en todo el proyecto.

!!! salto-pagina-pdf ""

## 1.3. Los estilos predeterminados del navegador

Aunque no escribamos ninguna hoja CSS, el navegador aplica algunos estilos básicos.

Por ejemplo:

- Los títulos aparecen con mayor tamaño y en negrita.
- Los enlaces suelen aparecer azules y subrayados.
- Las listas incorporan viñetas o números.
- Los botones tienen un borde y un fondo.
- El elemento `<body>` suele incluir un pequeño margen.

Estos estilos proceden de la **hoja de estilos del navegador** o del **agente de usuario**.

Por este motivo, una página HTML no aparece completamente vacía de estilos aunque todavía no hayamos escrito CSS.

Cada navegador puede aplicar pequeñas diferencias. Nuestra hoja de estilos permitirá redefinir esos valores y establecer una apariencia común para FestWeb.

## 1.4. Cómo representa el navegador una página

El navegador no muestra directamente el texto contenido en los archivos HTML y CSS. Antes debe analizarlos y construir una representación interna de la página.

El proceso puede resumirse en las siguientes fases.

### 1. Interpretación del HTML

El navegador analiza el código HTML y construye el **DOM** (*Document Object Model*).

El DOM representa los elementos como una estructura jerárquica en forma de árbol.

Por ejemplo:

```html
<article class="event-card">
  <h2>Festival SoundWave</h2>
  <p>18 de octubre · Valencia</p>
</article>
```

!!! salto-pagina-pdf ""

Puede representarse conceptualmente así:

```text
article.event-card
    h2
        Festival SoundWave
    p
        18 de octubre · Valencia
```

Cada elemento, atributo y texto se convierte en un nodo que el navegador puede localizar y manipular.

### 2. Interpretación del CSS

El navegador analiza las hojas de estilo y construye el **CSSOM** (*CSS Object Model*).

El CSSOM contiene:

- Los selectores.
- Las propiedades.
- Los valores.
- Las relaciones entre las reglas.
- La información necesaria para resolver la cascada.

Por ejemplo:

```css
.event-card {
  color: #213FC2;
  background-color: #C6D8FF;
}
```

El navegador deberá determinar qué elementos coinciden con `.event-card` y qué valores deben aplicarse finalmente.

### 3. Construcción del árbol de representación

El navegador combina la información del DOM y del CSSOM para construir el **árbol de representación** o *render tree*.

Este árbol contiene los elementos que deben dibujarse en la pantalla y los estilos finales que les corresponden.

Algunos nodos del DOM no forman parte del árbol de representación. Por ejemplo:

- Los elementos incluidos en `<head>`.
- Los metadatos.
- Los elementos que tienen `display: none`.

### 4. Maquetación

En la fase de **maquetación**, también denominada *layout*, el navegador calcula:

- El ancho y el alto de cada elemento.
- Su posición.
- El espacio que ocupa.
- Su relación con los elementos cercanos.

En esta fase intervienen propiedades como:

- `width`
- `height`
- `margin`
- `padding`
- `display`

### 5. Pintado

En la fase de **pintado**, el navegador dibuja los elementos:

- Textos.
- Colores.
- Fondos.
- Bordes.
- Imágenes.
- Sombras.

### 6. Composición

Finalmente, el navegador combina las diferentes capas visuales y muestra el resultado en la pantalla.

El proceso completo puede resumirse así:

```text
HTML → DOM
CSS  → CSSOM
DOM + CSSOM → árbol de representación
árbol de representación → maquetación → pintado → composición
```

> **Observa:**  
> Cuando modificamos una propiedad CSS, el navegador puede tener que volver a calcular la maquetación, repintar determinados elementos o recomponer algunas capas.

## 1.5. Anatomía de una regla CSS

Una hoja de estilos está formada por un conjunto de **reglas CSS**.

```css
.event-card {
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
}
```

Una regla contiene dos partes principales:

1. Un **selector**.
2. Un **bloque de declaraciones**.

### 1. Selector

El selector indica qué elementos HTML deben recibir los estilos.

```css
.event-card
```

En este caso, el navegador buscará todos los elementos que contengan la clase `event-card`.

### 2. Bloque de declaraciones

El bloque está delimitado por llaves:

```css
{
  color: #213FC2;
  background-color: #C6D8FF;
}
```

En su interior se incluyen una o varias declaraciones.

### 3. Declaración

Cada declaración está formada por una propiedad y un valor:

```css
color: #213FC2;
```

- `color` es la **propiedad**.
- `#213FC2` es el **valor**.
- Los dos puntos separan la propiedad del valor.
- El punto y coma indica el final de la declaración.

!!! salto-pagina-pdf ""

La estructura general de una regla es:

```css
selector {
  propiedad: valor;
  propiedad: valor;
}
```

## 1.6. Propiedades y valores

Una propiedad representa la característica que queremos modificar.

Por ejemplo:

```css
color
background-color
font-size
border
padding
```

El valor indica cómo debe configurarse esa propiedad.

```css
color: #213FC2;
font-size: 1.5rem;
border: 2px solid #50C9E9;
padding: 1rem;
```

Una misma propiedad puede admitir diferentes tipos de valores.

Por ejemplo:

```css
color: blue;
color: #213FC2;
color: rgb(33 63 194);
```

Las tres declaraciones utilizan la propiedad `color`, pero expresan el valor de formas diferentes.

## 1.7. Varias declaraciones en una regla

Una regla puede contener tantas declaraciones como sean necesarias.

```css
.event-card {
  width: 20rem;
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.75rem;
}
```

Es recomendable escribir una declaración por línea porque mejora:

- La lectura.
- La localización de errores.
- La comparación de cambios.
- El trabajo colaborativo.
- El mantenimiento.

También conviene conservar el punto y coma de la última declaración. Aunque en algunos casos pueda omitirse, mantenerlo facilita añadir nuevas propiedades posteriormente.

## 1.8. Comentarios en CSS

Los comentarios permiten documentar la hoja de estilos.

```css
/* Tarjeta utilizada en el listado de eventos */
.event-card {
  padding: 1.5rem;
}
```

CSS utiliza comentarios de bloque delimitados por `/*` y `*/`.

```css
/*
  Este comentario puede ocupar
  varias líneas.
*/
```

Los comentarios pueden utilizarse para:

- Identificar secciones.
- Explicar una decisión poco evidente.
- Documentar una solución temporal.
- Desactivar una declaración durante la depuración.

```css
.event-card {
  padding: 1.5rem;

  /* Se desactiva temporalmente para comprobar el diseño */
  /* box-shadow: 0 0.5rem 1rem rgb(33 63 194 / 20%); */
}
```

CSS no admite los comentarios de una línea `//` utilizados en otros lenguajes.

El siguiente comentario no es válido:

```css
// Este comentario produce un error
```

Los comentarios deben explicar aquello que no resulta evidente. No es necesario describir literalmente cada declaración.

```css
/* Incorrecto: repite exactamente lo que ya indica el código */
color: #213FC2; /* Aplica el color #213FC2 */
```

Resulta más útil explicar la finalidad de una decisión:

```css
/* Mantiene el color corporativo en los títulos de las tarjetas */
color: #213FC2;
```

## 1.9. Primer ejemplo de FestWeb

Partimos de esta estructura HTML:

```html
<article class="event-card">
  <h2 class="event-card__title">Festival SoundWave</h2>
  <p class="event-card__meta">18 de octubre · Valencia</p>
  <a class="event-card__link" href="evento.html" target="_blank" rel="noopener noreferrer">Ver evento</a>
</article>
```

Podemos aplicar una primera presentación mediante CSS:

```css
.event-card {
  padding: 1.5rem;
  color: #213FC2;
  background-color: #C6D8FF;
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

En este ejemplo:

- HTML define la información y su estructura.
- CSS define su apariencia.
- Las clases permiten relacionar las reglas con los elementos.
- La paleta cromática procede de la guía de estilo de FestWeb.

Todavía no hemos estudiado cómo funcionan los diferentes selectores, cómo se calculan los espacios o qué ocurre cuando dos reglas entran en conflicto. Esos conceptos se desarrollarán en los siguientes apartados.


> **CSS convierte las decisiones visuales de una guía de estilo en reglas que el navegador puede interpretar y reutilizar.**

!!! salto-pagina-pdf ""