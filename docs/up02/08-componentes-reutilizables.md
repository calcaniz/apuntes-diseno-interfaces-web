---
title: Componentes reutilizables
---

# 7. Componentes reutilizables

Una interfaz suele repetir elementos con la misma función y apariencia: botones, tarjetas, avisos, formularios o sistemas de navegación.

En lugar de escribir estilos independientes para cada elemento, podemos crear clases reutilizables. Esto permite mantener una interfaz coherente y modificar su diseño con mayor facilidad.

> **Pregunta de partida:**  
> Si FestWeb contiene veinte tarjetas de eventos, ¿deberíamos diseñar cada tarjeta por separado?

## 7.1. ¿Qué es un componente?

Un componente es un elemento de interfaz que reúne una estructura, una apariencia y una función determinadas.

Algunos componentes habituales son:

- Botones.
- Tarjetas.
- Avisos.
- Etiquetas.
- Formularios.
- Menús de navegación.
- Cabeceras y pies de página.

Por ejemplo, una tarjeta de FestWeb puede contener:

```html
<article class="tarjeta-evento">
  <img
    class="tarjeta-evento__imagen"
    src="imagenes/concierto.jpg"
    alt="Escenario del concierto"
  >

  <div class="tarjeta-evento__contenido">
    <span class="tarjeta-evento__categoria">Música</span>
    <h2 class="tarjeta-evento__titulo">Festival de verano</h2>
    <p class="tarjeta-evento__informacion">
      18 de julio · Valencia
    </p>
    <a class="boton boton--principal" href="evento.html">
      Ver evento
    </a>
  </div>
</article>
```

Esta estructura puede repetirse para mostrar diferentes eventos sin necesidad de crear estilos nuevos.

## 7.2. Clases reutilizables

Las clases permiten aplicar las mismas reglas a varios elementos:

```css
.boton {
  display: inline-block;
  padding: 0.75rem 1.25rem;
  border: 2px solid transparent;
  border-radius: 0.5rem;
  font-weight: 700;
  text-decoration: none;
  cursor: pointer;
}
```

La clase `.boton` contiene las características compartidas por todos los botones.

```html
<a class="boton" href="eventos.html">Ver eventos</a>
<button class="boton" type="submit">Guardar</button>
```

Una misma clase puede utilizarse en diferentes etiquetas HTML cuando comparten una presentación o comportamiento visual.

!!! salto-pagina-pdf ""

## 7.3. Clase base y variantes

Un componente puede disponer de una clase base y varias clases modificadoras.

```css
.boton {
  display: inline-block;
  padding: 0.75rem 1.25rem;
  border: 2px solid transparent;
  border-radius: 0.5rem;
  font: inherit;
  font-weight: 700;
  text-decoration: none;
  cursor: pointer;
}

.boton--principal {
  color: #213fc2;
  background-color: #50c9e9;
}

.boton--secundario {
  color: #213fc2;
  background-color: transparent;
  border-color: #213fc2;
}

.boton--advertencia {
  color: #213fc2;
  background-color: #e8b718;
}
```

Para aplicar una variante, se utilizan las dos clases:

```html
<a class="boton boton--principal" href="evento.html">
  Ver evento
</a>

<a class="boton boton--secundario" href="eventos.html">
  Volver al listado
</a>
```

La clase `.boton` define la estructura común y las clases modificadoras cambian únicamente el aspecto necesario.

!!! tip "Evitar duplicaciones"
    Si dos componentes comparten muchas declaraciones, conviene extraerlas a una clase base y mantener en las variantes solo sus diferencias.

!!! salto-pagina-pdf ""

## 7.4. Partes de un componente

Una forma de organizar las clases consiste en relacionar cada parte con el nombre del componente:

```css
.tarjeta-evento {
  max-width: 22rem;
  padding: 1.25rem;
  color: #213fc2;
  background-color: #ffffff;
  border: 2px solid #50c9e9;
  border-radius: 0.75rem;
}

.tarjeta-evento__imagen {
  display: block;
  width: 100%;
  height: 12rem;
  object-fit: cover;
  border-radius: 0.5rem;
}

.tarjeta-evento__titulo {
  margin: 0.75rem 0 0.5rem;
  font-size: 1.25rem;
}

.tarjeta-evento__informacion {
  margin-bottom: 1rem;
  line-height: 1.5;
}
```

Los nombres permiten identificar fácilmente la relación existente entre los elementos:

| Clase { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `.tarjeta-evento` | Componente principal |
| `.tarjeta-evento__imagen` | Imagen de la tarjeta |
| `.tarjeta-evento__titulo` | Título del evento |
| `.tarjeta-evento__informacion` | Fecha y lugar |

!!! salto-pagina-pdf ""

Este sistema se aproxima a la metodología **BEM**, que diferencia bloques, elementos y modificadores:

```text
bloque
bloque__elemento
bloque--modificador
```

No es obligatorio utilizar BEM, pero sí mantener una convención clara y constante.

## 7.5. Estados de un componente

Los componentes pueden cambiar de apariencia según la interacción del usuario.

```css
.boton--principal:hover {
  background-color: #3b82e6;
}

.boton:focus-visible {
  outline: 3px solid #213fc2;
  outline-offset: 3px;
}

.boton:active {
  transform: translateY(1px);
}
```

Los estados más habituales son:

| Estado { .table-full-container .table-cl-secundario .table-bg-principal } | Significado { .table-cl-secundario .table-bg-principal } |
|---|---|
| `:hover` | El puntero se encuentra sobre el elemento |
| `:focus-visible` | El elemento recibe el foco de teclado |
| `:active` | El elemento está siendo activado |
| `:disabled` | Un control se encuentra deshabilitado |

!!! salto-pagina-pdf ""

El foco visible no debe eliminarse sin proporcionar una alternativa:

```css
/* No recomendado */
.boton:focus {
  outline: none;
}
```

Los usuarios que navegan mediante teclado necesitan saber qué elemento tiene el foco.

## 7.6. Componentes frente a selectores demasiado específicos

Podríamos definir un botón mediante un selector dependiente de su posición:

```css
main section article div a {
  color: #213fc2;
  background-color: #50c9e9;
}
```

Este selector resulta difícil de reutilizar. Además, dejará de funcionar si cambia la estructura HTML.

Es preferible utilizar una clase:

```css
.boton--principal {
  color: #213fc2;
  background-color: #50c9e9;
}
```

De esta manera, el estilo depende de la función del elemento y no de su posición exacta dentro del documento.

!!! salto-pagina-pdf ""

## 7.7. Organización de los estilos

Los estilos pueden ordenarse por componentes para facilitar su localización:

```css
/* 1. Propiedades personalizadas */
:root {
  --color-principal: #50c9e9;
  --color-secundario: #3b82e6;
  --color-fondo: #c6d8ff;
  --color-texto: #213fc2;
}

/* 2. Reglas generales */
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  color: var(--color-texto);
  background-color: var(--color-fondo);
}

/* 3. Botones */
.boton {
  /* Estilos comunes */
}

.boton--principal {
  /* Variante principal */
}

/* 4. Tarjetas */
.tarjeta-evento {
  /* Estilos del componente */
}
```

En proyectos más grandes, los estilos también pueden distribuirse en varios archivos:

```text
css/
    estilos.css
    componentes/
        botones.css
        tarjetas.css
        formularios.css
```

La organización elegida debe ser comprensible y mantenerse durante todo el proyecto.

!!! salto-pagina-pdf ""

## 7.8. Reutilización en FestWeb

FestWeb puede utilizar los mismos componentes en diferentes pantallas:

- Una tarjeta de evento en el inicio y en el listado.
- Un botón principal para consultar o guardar un evento.
- Un botón secundario para volver atrás o cancelar.
- Una etiqueta para mostrar la categoría.
- Un aviso para comunicar información importante.

```html
<article class="tarjeta-evento">
  <span class="etiqueta etiqueta--musica">Música</span>
  <h2 class="tarjeta-evento__titulo">Festival de verano</h2>
  <p class="tarjeta-evento__informacion">18 de julio · Valencia</p>
  <a class="boton boton--principal" href="festival-verano.html">
    Ver evento
  </a>
</article>
```

Para mostrar otro evento solo cambia el contenido:

```html
<article class="tarjeta-evento">
  <span class="etiqueta etiqueta--deporte">Deporte</span>
  <h2 class="tarjeta-evento__titulo">Carrera popular</h2>
  <p class="tarjeta-evento__informacion">25 de julio · Gandía</p>
  <a class="boton boton--principal" href="carrera-popular.html">
    Ver evento
  </a>
</article>
```

Ambas tarjetas mantienen la misma estructura visual porque reutilizan las mismas clases.

---

> *Diseñar un componente una sola vez permite mantener la coherencia cada vez que se vuelve a utilizar.*

!!! salto-pagina-pdf ""