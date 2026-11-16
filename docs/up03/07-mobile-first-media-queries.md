---
title: 5. Mobile first, media queries y comprobación responsive
---

# 5. Mobile first, media queries y comprobación responsive

Un diseño flexible puede adaptarse automáticamente a muchos cambios de tamaño. Sin embargo, en algunos puntos la distribución necesita una modificación más profunda.

Por ejemplo:

- La navegación deja de caber en una sola fila.
- Las tarjetas resultan demasiado estrechas.
- Una zona lateral debe colocarse debajo del contenido.
- Algunos controles necesitan cambiar su distribución.

Las **media queries** permiten aplicar reglas CSS cuando se cumplen determinadas condiciones relacionadas con el dispositivo o con la ventana del navegador.

## 5.1. La estrategia mobile first

La estrategia **mobile first** consiste en diseñar primero para las pantallas más estrechas y añadir progresivamente mejoras para tamaños mayores.

El proceso habitual es:

1. Crear los estilos básicos para móviles.
2. Comprobar que el contenido funciona correctamente.
3. Añadir cambios para tabletas.
4. Ampliar la distribución para escritorios.

```css
/* Estilos base: móvil */

.listado-eventos {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
}

/* Mejora para pantallas más amplias */

@media (min-width: 48rem) {
    .listado-eventos {
        grid-template-columns: repeat(2, 1fr);
    }
}
```

Los estilos situados fuera de la media query corresponden a la versión más sencilla. La media query incorpora la mejora cuando existe espacio suficiente.

!!! note "Idea clave"

    Mobile first no significa diseñar únicamente para móviles. Significa comenzar por la situación más limitada y ampliar progresivamente la interfaz.

## 5.2. Configuración del viewport

Para que el navegador represente correctamente la anchura del dispositivo, el documento HTML debe incluir:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Esta etiqueta indica que:

- La anchura de la página debe coincidir con la anchura del dispositivo.
- La escala inicial debe ser del 100 %.
- El navegador no debe simular una página de escritorio reducida.

Debe colocarse dentro de `<head>`:

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FestWeb</title>
    <link rel="stylesheet" href="css/estilos.css">
</head>
```

## 5.3. Sintaxis de una media query

Una media query comienza con `@media` y contiene las reglas que se aplicarán cuando se cumpla una condición.

```css
@media (min-width: 48rem) {
    .contenedor {
        max-width: 72rem;
        margin-inline: auto;
    }
}
```

En este ejemplo, la regla se aplica cuando la ventana tiene una anchura mínima de `48rem`.

Las condiciones más habituales son:

| Condición { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `min-width` | Aplica estilos desde una anchura mínima. |
| `max-width` | Aplica estilos hasta una anchura máxima. |
| `orientation: portrait` | Detecta una orientación vertical. |
| `orientation: landscape` | Detecta una orientación horizontal. |

Para una estrategia mobile first se utiliza principalmente `min-width`.

## 5.4. Selección de los breakpoints

Un **breakpoint** es el punto en el que se modifica la distribución de la interfaz.

No debe elegirse únicamente porque coincida con un modelo concreto de dispositivo. Debe introducirse cuando el contenido comienza a presentar problemas.

Por ejemplo:

- La navegación ya no cabe correctamente.
- Los botones quedan demasiado juntos.
- Las tarjetas resultan excesivamente anchas.
- Aparecen líneas de texto demasiado largas.
- Se desaprovecha demasiado espacio disponible.

Podemos utilizar algunos valores de referencia:

```css
/* Tabletas y ventanas medianas */

@media (min-width: 48rem) {
}

/* Escritorios */

@media (min-width: 64rem) {
}
```

Estos valores no son obligatorios. El breakpoint correcto depende de la interfaz y de su contenido.

## 5.5. Adaptación mobile first de FestWeb

En la versión móvil, la cabecera se organiza verticalmente y las tarjetas ocupan una única columna.

```css
.cabecera__contenido {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.navegacion__lista {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.listado-eventos {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1.5rem;
}
```

Cuando aumenta el espacio disponible, podemos reorganizar la cabecera y el listado.

```css
@media (min-width: 48rem) {
    .cabecera__contenido {
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    .navegacion__lista {
        flex-direction: row;
    }

    .listado-eventos {
        grid-template-columns: repeat(2, 1fr);
    }
}
```

En pantallas de escritorio podemos mostrar tres tarjetas.

```css
@media (min-width: 64rem) {
    .listado-eventos {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

La misma estructura HTML funciona en los tres tamaños. Únicamente cambia su presentación mediante CSS.

!!! salto-pagina-pdf ""

## 5. Evitar media queries innecesarias

No todos los cambios necesitan una media query. Flexbox y Grid pueden resolver muchas adaptaciones automáticamente.

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(
        auto-fit,
        minmax(min(100%, 18rem), 1fr)
    );
    gap: 1.5rem;
}
```

Esta cuadrícula:

- Muestra tantas columnas como permite el espacio.
- Evita que una tarjeta mida menos de `18rem`.
- Reduce automáticamente el número de columnas.
- Mantiene una sola columna cuando la pantalla es estrecha.

Las media queries deben reservarse para los cambios estructurales que no puedan resolverse de forma natural.

## 5.7. No ocultar contenido esencial

En una interfaz responsive podemos reorganizar o simplificar algunos elementos, pero no debemos eliminar información imprescindible únicamente para que el diseño resulte más cómodo.

```css
/* Mala práctica */

@media (max-width: 36rem) {
    .datos-importantes {
        display: none;
    }
}
```

Antes de ocultar contenido debemos preguntarnos:

- ¿Lo necesita el usuario para completar la tarea?
- ¿Puede colocarse en otra posición?
- ¿Puede resumirse sin perder información?
- ¿Sigue siendo accesible mediante teclado y tecnologías de apoyo?

Responsive significa adaptar el contenido, no suprimirlo arbitrariamente.

## 5.8. Comprobación con las herramientas del navegador

Chrome permite simular distintos tamaños mediante las herramientas de desarrollo:

1. Abre la página en Chrome.
2. Pulsa `F12`.
3. Activa **Toggle device toolbar**.
4. Selecciona un dispositivo o introduce una anchura manual.
5. Cambia progresivamente el tamaño de la ventana.
5. Comprueba cuándo aparece cada media query.

No debemos probar únicamente tamaños predefinidos. Es importante arrastrar el borde de la simulación y observar el comportamiento intermedio.

Como mínimo, comprobaremos:

| Anchura { .table-full-container .table-cl-secundario .table-bg-principal } | Comprobación { .table-cl-secundario .table-bg-principal } |
|---|---|
| `390px` | Móvil: una columna y controles accesibles. |
| `768px` | Tableta: reorganización de navegación y tarjetas. |
| `1280px` | Escritorio: aprovechamiento del espacio disponible. |

También deben revisarse:

- La ausencia de desplazamiento horizontal.
- La legibilidad de los textos.
- El tamaño de enlaces y botones.
- La adaptación de las imágenes.
- El orden visual del contenido.
- Los estados `hover` y `focus`.
- El funcionamiento con zoom.

!!! salto-pagina-pdf ""

## 5.9. Errores frecuentes

### Diseñar primero el escritorio y reducirlo después

Suele provocar demasiadas excepciones y reglas con `max-width`.

### Utilizar demasiados breakpoints

La hoja de estilos se vuelve difícil de mantener.

### Elegir breakpoints según marcas de dispositivos

La interfaz debe responder a su contenido, no a un catálogo concreto de teléfonos.

### Utilizar anchuras fijas dentro de las media queries

```css
@media (min-width: 48rem) {
    .tarjeta-evento {
        width: 420px;
    }
}
```

Es preferible permitir que Grid o Flexbox distribuyan el espacio disponible.

### Probar únicamente en un tamaño

Una interfaz puede funcionar a `390px` y `1280px`, pero romperse en una anchura intermedia.

## 5.10. Comprueba lo aprendido

Analiza el siguiente código:

```css
.tarjeta-evento {
    padding: 1rem;
}

@media (min-width: 48rem) {
    .tarjeta-evento {
        padding: 1.5rem;
    }
}

@media (min-width: 64rem) {
    .tarjeta-evento {
        padding: 2rem;
    }
}
```

Responde:

1. ¿Qué `padding` tendrá la tarjeta a `390px`?
2. ¿Qué `padding` tendrá a `800px`?
3. ¿Qué `padding` tendrá a `1280px`?
4. ¿Por qué este código sigue una estrategia mobile first?
5. ¿Qué ocurriría si intercambiáramos el orden de las dos media queries?

---

!!! salto-pagina-pdf ""