---
title: Unidades contenedores y recursos adaptables
---

# 2. Unidades, contenedores y recursos adaptables

Una interfaz responsive necesita dimensiones capaces de adaptarse al espacio disponible. Para conseguirlo, combinaremos unidades relativas, límites de anchura y recursos que puedan reducirse sin perder sus proporciones.

## 2.1. Unidades de medida

CSS permite expresar las dimensiones utilizando diferentes unidades:

| Unidad { .table-full-container .table-cl-secundario .table-bg-principal } | Referencia { .table-cl-secundario .table-bg-principal } | Uso habitual { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| `px` | Tamaño fijo en CSS | Bordes, sombras y pequeños detalles |
| `%` | Tamaño del contenedor | Anchuras y distribuciones fluidas |
| `em` | Tamaño de fuente del elemento o contexto | Componentes que deben escalar conjuntamente |
| `rem` | Tamaño de fuente del elemento raíz | Tipografía y espaciados generales |
| `vw` | Porcentaje del ancho del viewport | Elementos relacionados con la anchura de la ventana |
| `vh` | Porcentaje de la altura del viewport | Secciones relacionadas con la altura de la ventana |

No existe una única unidad adecuada para todos los casos. Una interfaz suele combinar diferentes unidades según la función de cada propiedad.

!!! example "Aplicación habitual"

    Podemos utilizar:

    - `px` para un borde.
    - `rem` para el relleno de una tarjeta.
    - `%` para la anchura de un contenedor.
    - `vw` para adaptar progresivamente un título.

```css
.tarjeta-evento {
    width: 100%;
    padding: 1rem;
    border: 1px solid #cccccc;
    border-radius: 0.75rem;
}
```

## 2.2. Diferencia entre `em` y `rem`

La unidad `em` depende del tamaño de fuente del elemento o de su contexto.

```css
.boton {
    font-size: 1rem;
    padding: 0.75em 1.5em;
}
```

Si aumenta el tamaño del texto del botón, su relleno también aumentará proporcionalmente.

La unidad `rem` depende del tamaño de fuente del elemento raíz `html`:

```css
h1 {
    font-size: 2.5rem;
}

.seccion {
    margin-block: 3rem;
}
```

Esto facilita la creación de una escala tipográfica y de espaciado coherente en toda la interfaz.

!!! salto-pagina-pdf ""

## 2.3. Contenedores fluidos

Un contenedor completamente fijo puede desbordar en pantallas pequeñas:

```css
.contenedor {
    width: 1200px;
}
```

Una alternativa consiste en combinar una anchura relativa con un límite máximo:

```css
.contenedor {
    width: 90%;
    max-width: 75rem;
    margin-inline: auto;
}
```

Este contenedor:

- Ocupa el 90 % del espacio disponible.
- Nunca supera los `75rem`.
- Se mantiene centrado horizontalmente.

!!! info "Anchura y límite"

    `width` establece la anchura deseada, mientras que `max-width` impide que el elemento continúe creciendo cuando dispone de demasiado espacio.

También podemos reservar un margen constante alrededor del contenido:

```css
.contenedor {
    width: min(75rem, calc(100% - 2rem));
    margin-inline: auto;
}
```

De esta forma, el contenedor conserva un margen mínimo de `1rem` a cada lado.


!!! salto-pagina-pdf ""

## 2.4. Modelo de caja

Para que el relleno y el borde se incluyan dentro de la anchura declarada, utilizaremos:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

Sin `border-box`, un elemento con `width: 100%` podría superar la anchura de su contenedor al añadirle relleno o bordes.

## 2.5. Imágenes y vídeos adaptables

Una imagen con dimensiones fijas puede superar la anchura disponible:

```css
img {
    width: 800px;
}
```

Para permitir que se reduzca cuando sea necesario:

```css
img,
video {
    max-width: 100%;
    height: auto;
    display: block;
}
```

Con estas reglas:

- El recurso no supera la anchura de su contenedor.
- Mantiene su proporción original.
- Evita el espacio inferior propio de los elementos en línea.

### Imágenes de las tarjetas de FestWeb

Podemos establecer una proporción común para todas las imágenes:

```css
.tarjeta-evento__imagen {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
}
```

`aspect-ratio` reserva una proporción constante y `object-fit: cover` permite cubrir el espacio recortando la parte que no cabe.


## 2.6. Tipografía adaptable con `clamp()`

La función `clamp()` permite establecer un valor mínimo, uno adaptable y uno máximo:

```css
h1 {
    font-size: clamp(2rem, 5vw, 4rem);
}
```

El título:

- Nunca será menor de `2rem`.
- Crecerá en relación con el viewport.
- Nunca superará los `4rem`.

!!! warning "Unidades de viewport"

    No conviene utilizar únicamente `vw` para el texto, porque podría llegar a ser demasiado pequeño o demasiado grande. `clamp()` permite establecer límites seguros.

## 2.7. Control del desbordamiento

La aparición de una barra horizontal suele indicar que algún elemento supera la anchura disponible.

Debemos localizar el elemento responsable mediante DevTools y revisar:

- Su anchura.
- Sus márgenes.
- Su relleno.
- El tamaño de sus imágenes.
- Su posicionamiento.

Cuando el desplazamiento horizontal sea necesario, debe aplicarse únicamente al componente correspondiente.

### Ejemplo de tabla adaptable

```html
<div class="tabla-responsive">
    <table>
        <!-- Contenido de la tabla -->
    </table>
</div>
```

```css
.tabla-responsive {
    overflow-x: auto;
}
```

La página no se desplaza horizontalmente, pero la tabla puede hacerlo cuando no dispone de suficiente espacio.

## 2.8. Ejemplo completo en FestWeb

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}

.contenedor {
    width: min(75rem, calc(100% - 2rem));
    margin-inline: auto;
}

.tarjeta-evento {
    width: 100%;
    padding: 1rem;
    border: 1px solid #cccccc;
    border-radius: 0.75rem;
}

.tarjeta-evento__imagen {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
    display: block;
}

.tarjeta-evento__titulo {
    font-size: clamp(1.25rem, 3vw, 1.75rem);
}
```

Estas reglas todavía no distribuyen las tarjetas en columnas, pero garantizan que los componentes y sus recursos puedan adaptarse al espacio disponible.

!!! salto-pagina-pdf ""

## 2.9. Comprobación

Explica qué función cumple cada declaración:

```css
.contenedor {
    width: 90%;
    max-width: 1200px;
    margin-inline: auto;
}
```

Después, responde:

1. ¿Qué ocurre cuando la ventana tiene menos de 1200 píxeles?
2. ¿Qué ocurre cuando dispone de más de 1200 píxeles?
3. ¿Por qué una imagen debería utilizar `max-width: 100%`?
4. ¿Qué ventaja ofrece `clamp()` frente a utilizar únicamente `vw`?

En el siguiente apartado utilizaremos Flexbox para distribuir y alinear elementos en una dimensión.

!!! salto-pagina-pdf ""