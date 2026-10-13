---
title: El modelo de caja
---

# 6. El modelo de caja

Los elementos de una página web se representan como cajas rectangulares. Comprender cómo se calcula y distribuye el espacio de estas cajas es fundamental para controlar correctamente el diseño de una interfaz.

> **Pregunta de partida:**  
> Si un elemento tiene una anchura de 300 píxeles, ¿por qué puede terminar ocupando más espacio del esperado?

## 6.1. ¿Qué es el modelo de caja?

El modelo de caja de CSS describe el espacio que ocupa cada elemento HTML.

Está formado por cuatro zonas:

1. **Contenido (`content`):** texto, imagen o contenido del elemento.
2. **Relleno (`padding`):** espacio entre el contenido y el borde.
3. **Borde (`border`):** línea que rodea el contenido y el relleno.
4. **Margen (`margin`):** separación exterior respecto a otros elementos.

```css
.tarjeta-evento {
  width: 20rem;
  padding: 1.5rem;
  border: 2px solid #50c9e9;
  margin: 1rem;
}
```

En este ejemplo:

- `width` establece la anchura del contenido.
- `padding` crea espacio dentro de la tarjeta.
- `border` delimita visualmente la tarjeta.
- `margin` la separa de otros elementos.

!!! salto-pagina-pdf ""

## 6.2. Contenido

Las propiedades `width` y `height` permiten establecer la anchura y la altura de un elemento:

```css
.imagen-evento {
  width: 100%;
  height: 12rem;
}
```

No siempre es conveniente asignar una altura fija. Si el contenido necesita más espacio, podría desbordarse o quedar recortado. Podemos establecer límites con:

```css
.contenido-principal {
  width: 90%;
  max-width: 75rem;
  min-height: 20rem;
}
```

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `width` | Establece la anchura |
| `height` | Establece la altura |
| `max-width` | Limita la anchura máxima |
| `min-width` | Define la anchura mínima |
| `max-height` | Limita la altura máxima |
| `min-height` | Define la altura mínima |

Una estructura habitual consiste en utilizar una anchura flexible junto con una anchura máxima:

```css
.contenedor {
  width: 90%;
  max-width: 75rem;
  margin: 0 auto;
}
```

De esta forma, el contenido puede reducirse en pantallas estrechas sin crecer indefinidamente en pantallas grandes.

!!! salto-pagina-pdf ""

## 6.3. Relleno interior

El `padding` crea espacio entre el contenido y el borde del elemento.

```css
.aviso {
  padding: 1rem;
}
```

También puede configurarse cada lado de manera independiente:

```css
.aviso {
  padding-top: 1rem;
  padding-right: 1.5rem;
  padding-bottom: 1rem;
  padding-left: 1.5rem;
}
```

La forma abreviada permite escribir los cuatro valores en una sola declaración:

```css
.aviso {
  padding: 1rem 1.5rem;
}
```

Cuando se indican dos valores:

- El primero se aplica arriba y abajo.
- El segundo se aplica a izquierda y derecha.


## 6.4. Bordes

Un borde se define mediante su grosor, estilo y color:

```css
.tarjeta-evento {
  border: 2px solid #50c9e9;
}
```

Estas propiedades también pueden escribirse por separado:

```css
.tarjeta-evento {
  border-width: 2px;
  border-style: solid;
  border-color: #50c9e9;
}
```

La propiedad `border-radius` permite redondear las esquinas:

```css
.tarjeta-evento {
  border-radius: 0.75rem;
}
```

En FestWeb podemos utilizar el borde para diferenciar componentes sin depender únicamente del color de fondo.

## 6.5. Márgenes

El `margin` establece el espacio exterior de un elemento:

```css
.tarjeta-evento {
  margin-bottom: 1.5rem;
}
```

También puede utilizarse la forma abreviada:

```css
.tarjeta-evento {
  margin: 1rem 0;
}
```

En este caso, se aplica:

- `1rem` arriba y abajo.
- `0` a izquierda y derecha.

Para centrar horizontalmente un elemento con una anchura limitada podemos utilizar:

```css
.contenedor {
  width: 90%;
  max-width: 75rem;
  margin: 0 auto;
}
```

El valor `auto` reparte automáticamente el espacio disponible entre los márgenes izquierdo y derecho.

!!! note "Margin y padding"
    `padding` crea espacio dentro del elemento. `margin` crea separación entre el elemento y las cajas que lo rodean.

!!! salto-pagina-pdf ""

## 6.6. Cálculo del tamaño de una caja

Por defecto, CSS aplica el modelo `content-box`. Esto significa que `width` y `height` solo definen el tamaño del contenido.

```css
.caja {
  width: 300px;
  padding: 20px;
  border: 5px solid #213fc2;
}
```

La anchura total será:

```text
300px + 20px + 20px + 5px + 5px = 350px
```

Los márgenes ocupan espacio adicional, pero no forman parte del tamaño interno de la caja.

Este comportamiento puede provocar que un elemento ocupe más espacio del esperado.

## 6.7. La propiedad `box-sizing`

La propiedad `box-sizing` modifica la forma de calcular el tamaño.

Con `border-box`, la anchura indicada incluye el contenido, el relleno y el borde:

```css
.caja {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid #213fc2;
}
```

Ahora la anchura total de la caja se mantiene en `300px`.

Es habitual aplicar esta configuración a todos los elementos:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

!!! tip "Práctica recomendada"
    Utilizar `border-box` facilita el cálculo de las dimensiones y evita muchos problemas de desbordamiento.

!!! salto-pagina-pdf ""

## 6.8. Desbordamiento del contenido

Cuando el contenido no cabe dentro de una caja, se produce un desbordamiento. La propiedad `overflow` permite decidir cómo debe comportarse:

```css
.descripcion-evento {
  max-height: 10rem;
  overflow: auto;
}
```

| Valor { .table-full-container .table-cl-secundario .table-bg-principal } | Comportamiento { .table-cl-secundario .table-bg-principal } |
|---|---|
| `visible` | El contenido se muestra fuera de la caja |
| `hidden` | El contenido sobrante se oculta |
| `auto` | Añade desplazamiento cuando resulta necesario |
| `scroll` | Muestra siempre barras de desplazamiento |

Ocultar contenido con `overflow: hidden` debe hacerse con cuidado, ya que puede impedir que el usuario acceda a información importante.

!!! salto-pagina-pdf ""

## 6.9. Aplicación a FestWeb

Podemos aplicar el modelo de caja a una tarjeta de evento:

```css
:root {
  --color-principal: #50c9e9;
  --color-fondo: #c6d8ff;
  --color-texto: #213fc2;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

.tarjeta-evento {
  width: 100%;
  max-width: 22rem;
  margin-bottom: 1.5rem;
  padding: 1.25rem;
  color: var(--color-texto);
  background-color: #ffffff;
  border: 2px solid var(--color-principal);
  border-radius: 0.75rem;
}

.tarjeta-evento__imagen {
  display: block;
  width: 100%;
  height: 12rem;
  object-fit: cover;
  border-radius: 0.5rem;
}

.tarjeta-evento__contenido {
  padding-top: 1rem;
}
```

Cada propiedad desempeña una función concreta:

- `max-width` limita el crecimiento de la tarjeta.
- `margin-bottom` la separa del siguiente elemento.
- `padding` evita que el contenido quede pegado al borde.
- `border` delimita el componente.
- `border-radius` suaviza sus esquinas.
- `box-sizing` facilita el cálculo de su anchura.
---

> *Controlar el modelo de caja significa controlar el espacio que ocupa cada elemento de la interfaz.*


!!! salto-pagina-pdf ""