---
title: A02.02. De la guía de estilo al componente (Simplificada)
---

# A02.02. De la guía de estilo al componente  (Simplificada)

**Duración:** 55 minutos  
**Modalidad:** Trabajo individual guiado  
**Apartados relacionados:** 5, 6 y 7  
**Carácter:** Actividad formativa  

## 1. Punto de partida

En la A02.01 creamos una hoja externa, aplicamos diferentes selectores y analizamos cómo resuelve el navegador los conflictos entre reglas CSS.

En esta actividad utilizaremos:

- La paleta cromática de FestWeb.
- Una escala común de espaciado.
- Unidades relativas.
- El modelo de caja.
- Clases base y modificadoras.

El objetivo será transformar las decisiones de la guía de estilo en un pequeño sistema de componentes reutilizables.

!!! info "Objetivo de la actividad"

    Al finalizar la sesión dispondrás de un catálogo básico con la tipografía, los botones y una tarjeta de evento de FestWeb.

## 2. Material necesario

Utiliza como punto de partida los archivos obtenidos en la A02.01.

La estructura inicial será similar a la siguiente:

```text
festweb/
├── index.html
├── css/
│   ├── estilos.css
│   └── conflictos.css
└── imagenes/
    ├── evento-musica.svg
    ├── evento-deporte.svg
    └── evento-cultura.svg
```

Crea un nuevo documento en la raíz del proyecto:

```text
componentes.html
```

Este documento funcionará como un catálogo en el que podremos comprobar la apariencia de los componentes sin depender de una página concreta.

La estructura del proyecto quedará así:

```text
festweb/
├── index.html
├── componentes.html
├── css/
│   ├── estilos.css
│   └── conflictos.css
└── imagenes/
```

!!! warning "Antes de continuar"

    Comprueba que `componentes.html` está correctamente vinculado con `css/estilos.css`.

```html
<link rel="stylesheet" href="css/estilos.css">
```

## 3. Preparación del catálogo

Añade a `componentes.html` una estructura HTML básica:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta
    name="description"
    content="Catálogo de componentes de la interfaz de FestWeb"
  >
  <title>Componentes de FestWeb</title>
  <link rel="stylesheet" href="css/estilos.css">
</head>

<body>
  <header>
    <h1>Componentes de FestWeb</h1>
    <p>Catálogo visual del sistema de estilos.</p>
  </header>

  <main class="catalogo-componentes">
    <!-- Incorporaremos aquí los diferentes componentes -->
  </main>
</body>
</html>
```

Abre el documento en el navegador.

De momento tendrá una apariencia muy básica. La iremos construyendo durante la actividad.

## 4. Propiedades personalizadas

Las propiedades personalizadas permiten almacenar valores compartidos y reutilizarlos mediante la función `var()`.

En lugar de repetir el mismo código de color en muchas reglas, podemos darle un nombre relacionado con su función.

💻 **Realiza**

Añade al principio de `estilos.css`:

```css
/* 1. Propiedades personalizadas */

:root {
  /* Paleta cromática */
  --color-principal: #50c9e9;
  --color-secundario: #3b82e6;
  --color-fondo: #c6d8ff;
  --color-acento: #a3a313;
  --color-texto: #213fc2;
  --color-advertencia: #e8b718;
  --color-superficie: #ffffff;

  /* Escala de espaciado */
  --espacio-xs: 0.25rem;
  --espacio-sm: 0.5rem;
  --espacio-md: 1rem;
  --espacio-lg: 1.5rem;
  --espacio-xl: 2rem;

  /* Esquinas */
  --radio-sm: 0.375rem;
  --radio-md: 0.75rem;
}
```

!!! note "Nombres semánticos"

    Es preferible utilizar `--color-principal` en lugar de `--azul-claro`. El primer nombre explica la función del color y continuará teniendo sentido aunque la paleta cambie.

👀 **Comprueba**

Busca en tu hoja CSS algún color repetido y sustitúyelo por la propiedad personalizada equivalente.

Por ejemplo:

```css
body {
  color: var(--color-texto);
}
```

## 5. Configuración global y modelo de caja

En el modelo `content-box`, el relleno y el borde se suman al ancho declarado. Con `border-box`, el navegador los incluye dentro del tamaño total de la caja.

Aplicaremos `border-box` a todos los elementos para trabajar con dimensiones más predecibles.

💻 **Realiza**

Añade:

```css
/* 2. Configuración general */

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  background-color: var(--color-fondo);
  color: var(--color-texto);
  font-family: "Poppins", Arial, sans-serif;
  font-size: 1rem;
  line-height: 1.5;
}

header,
.catalogo-componentes {
  max-width: 70rem;
  margin: 0 auto;
  padding: var(--espacio-lg);
}

.catalogo-componentes {
  background-color: var(--color-superficie);
}

.muestra-componentes {
  margin-bottom: var(--espacio-xl);
}
```

👀 **Comprueba**

Selecciona el elemento `<main>` con el inspector y localiza:

- El ancho del contenido.
- El `padding`.
- El `margin`.
- El valor de `box-sizing`.

❓ **Piensa**

¿El `margin` forma parte del ancho declarado de una caja cuando utilizamos `border-box`?

## 6. Jerarquía tipográfica

Añade dentro de `<main>`:

```html
<section class="muestra-componentes">
  <h2>Tipografía</h2>

  <p class="titulo-pagina">Título principal</p>

  <p class="titulo-seccion">Título de sección</p>

  <p class="titulo-tarjeta">Título de tarjeta</p>

  <p class="texto-contenido">
    Texto utilizado para describir un evento de FestWeb.
  </p>

  <p class="texto-secundario">
    Información auxiliar, fecha o ubicación.
  </p>
</section>
```

Define la jerarquía en `estilos.css`:

```css
/* 3. Tipografía */

.titulo-pagina {
  margin-bottom: var(--espacio-md);
  font-size: 2rem;
  font-weight: 700;
  line-height: 1.2;
}

.titulo-seccion {
  margin-bottom: var(--espacio-sm);
  font-size: 1.5rem;
  font-weight: 700;
  line-height: 1.3;
}

.titulo-tarjeta {
  margin-bottom: var(--espacio-sm);
  font-size: 1.25rem;
  font-weight: 600;
  line-height: 1.3;
}

.texto-contenido {
  font-size: 1rem;
  line-height: 1.5;
}

.texto-secundario {
  color: var(--color-secundario);
  font-size: 0.875rem;
  line-height: 1.4;
}
```

👀 **Comprueba**

- ¿Se distingue claramente la importancia de cada texto?
- ¿Se han utilizado unidades `rem`?
- ¿El texto de contenido mantiene una altura de línea legible?
- ¿Las diferencias dependen únicamente del tamaño?

!!! tip "Jerarquía visual"

    La jerarquía también puede construirse mediante el peso, el color, el espacio y la posición. No es necesario aumentar mucho el tamaño de todos los títulos.

## 7. Componente de botón

Un componente debe separar:

- Las propiedades compartidas.
- Las variantes visuales.
- Los estados de interacción.

La clase `.boton` contendrá las características comunes. Las clases modificadoras cambiarán únicamente las propiedades necesarias.

### 7.1. Código HTML

Añade al catálogo:

```html
<section class="muestra-componentes">
  <h2>Botones</h2>

  <a class="boton boton--principal" href="#">
    Botón principal
  </a>

  <a class="boton boton--secundario" href="#">
    Botón secundario
  </a>

  <button
    class="boton boton--desactivado"
    type="button"
    disabled
  >
    Botón desactivado
  </button>
</section>
```

### 7.2. Clase base

Añade a `estilos.css`:

```css
/* 4. Botones */

.boton {
  display: inline-block;
  padding: var(--espacio-sm) var(--espacio-md);
  border: 2px solid transparent;
  border-radius: var(--radio-sm);
  font: inherit;
  font-weight: 600;
  line-height: 1.2;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  transition:
    background-color 0.2s,
    border-color 0.2s,
    color 0.2s,
    transform 0.2s;
}
```

### 7.3. Variantes

```css
.boton--principal {
  background-color: var(--color-principal);
  border-color: var(--color-texto);
  color: var(--color-texto);
}

.boton--secundario {
  background-color: var(--color-superficie);
  border-color: var(--color-secundario);
  color: var(--color-texto);
}

.boton--desactivado {
  opacity: 0.55;
}
```

### 7.4. Estados

```css
.boton:hover:not(:disabled) {
  background-color: var(--color-secundario);
  color: var(--color-superficie);
}

.boton:focus-visible {
  outline: 3px solid var(--color-advertencia);
  outline-offset: 3px;
}

.boton:active:not(:disabled) {
  transform: translateY(2px);
}

.boton:disabled {
  cursor: not-allowed;
}
```

!!! warning "Estado desactivado"

    El atributo `disabled` funciona en controles como `<button>`, pero no en un enlace `<a>`. No utilices solamente un color apagado para simular que un enlace está desactivado.

👀 **Comprueba**

1. Pasa el puntero sobre los botones.
2. Accede a ellos utilizando la tecla `Tab`.
3. Mantén pulsado el botón principal.
4. Intenta pulsar el botón desactivado.
5. Comprueba que la clase base no se repite dentro de cada variante.

## 8. Componente de etiqueta

Añade dentro del catálogo:

```html
<section class="muestra-componentes">
  <h2>Etiquetas</h2>

  <span class="etiqueta etiqueta--musica">Música</span>
  <span class="etiqueta etiqueta--deporte">Deporte</span>
  <span class="etiqueta etiqueta--cultura">Cultura</span>
</section>
```

Define la clase base:

```css
/* 5. Etiquetas */

.etiqueta {
  display: inline-block;
  padding: var(--espacio-xs) var(--espacio-sm);
  border-radius: var(--radio-sm);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}
```

Añade las variantes:

```css
.etiqueta--musica {
  background-color: var(--color-principal);
  color: var(--color-texto);
}

.etiqueta--deporte {
  background-color: var(--color-secundario);
  color: var(--color-superficie);
}

.etiqueta--cultura {
  background-color: var(--color-acento);
  color: var(--color-superficie);
}
```

❓ **Piensa**

¿Qué ocurriría si repitiéramos el `padding`, el tamaño tipográfico y las esquinas dentro de cada variante?

## 9. Componente de tarjeta

La tarjeta reutilizará los componentes anteriores en lugar de crear nuevos estilos independientes.

### 9.1. Código HTML

Añade:

```html
<section class="muestra-componentes">
  <h2>Tarjeta de evento</h2>

  <article class="tarjeta-evento">
    <img
      class="tarjeta-evento__imagen"
      src="imagenes/evento-musica.svg"
      alt="Escenario de un festival de música"
    >

    <div class="tarjeta-evento__contenido">
      <span class="etiqueta etiqueta--musica">
        Música
      </span>

      <h3 class="tarjeta-evento__titulo">
        Festival de verano
      </h3>

      <p class="tarjeta-evento__datos">
        18 de julio · Valencia
      </p>

      <p class="tarjeta-evento__descripcion">
        Una jornada de música al aire libre con artistas locales.
      </p>

      <a class="boton boton--principal" href="#">
        Ver evento
      </a>
    </div>
  </article>
</section>
```

### 9.2. Clase base y elementos

Añade a `estilos.css`:

```css
/* 6. Tarjetas */

.tarjeta-evento {
  max-width: 24rem;
  margin: var(--espacio-md) 0;
  overflow: hidden;
  background-color: var(--color-superficie);
  border: 1px solid var(--color-secundario);
  border-radius: var(--radio-md);
}

.tarjeta-evento__imagen {
  display: block;
  width: 100%;
  height: 12rem;
  object-fit: cover;
}

.tarjeta-evento__contenido {
  padding: var(--espacio-lg);
}

.tarjeta-evento__titulo {
  margin:
    var(--espacio-sm)
    0
    var(--espacio-xs);
  font-size: 1.25rem;
  line-height: 1.3;
}

.tarjeta-evento__datos {
  margin:
    0
    0
    var(--espacio-sm);
  color: var(--color-secundario);
  font-size: 0.875rem;
}

.tarjeta-evento__descripcion {
  margin:
    0
    0
    var(--espacio-md);
}
```

👀 **Comprueba el modelo de caja**

Selecciona `.tarjeta-evento` y localiza:

- `max-width`.
- `margin`.
- `border`.
- `border-radius`.
- `overflow`.
- El espacio interior de `.tarjeta-evento__contenido`.

!!! note "Reutilización"

    El botón y la etiqueta incluidos en la tarjeta son instancias de los componentes ya definidos. No deben volver a programarse dentro de `.tarjeta-evento`.

## 10. Pequeño reto individual

Crea dos variantes de la tarjeta.

### 10.1. Tarjeta destacada

Añade una segunda tarjeta con las clases:

```html
<article class="tarjeta-evento tarjeta-evento--destacada">
```

Define una variante que modifique únicamente algunas propiedades:

```css
.tarjeta-evento--destacada {
  border-width: 3px;
  border-color: var(--color-acento);
}
```

### 10.2. Tarjeta agotada

Añade una tercera tarjeta:

```html
<article class="tarjeta-evento tarjeta-evento--agotada">
```

La tarjeta deberá:

- Mantener legible la información.
- Mostrar claramente que no quedan entradas.
- Utilizar un botón con el atributo `disabled`.
- Reutilizar la clase base `.tarjeta-evento`.

Puedes comenzar con:

```css
.tarjeta-evento--agotada {
  opacity: 0.75;
}
```

🧩 **Reto adicional**

Crea una nueva propiedad personalizada para la sombra de los componentes y aplícala a la tarjeta destacada.

