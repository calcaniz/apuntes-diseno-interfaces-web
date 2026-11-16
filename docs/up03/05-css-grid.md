---
title: Composición con CSS Grid
---

# 4. Composición bidimensional con CSS Grid

CSS Grid es un sistema de composición que permite organizar elementos simultáneamente en filas y columnas.

Resulta especialmente adecuado para:

- Listados de tarjetas.
- Galerías de imágenes.
- Estructuras generales de página.
- Paneles de información.
- Composiciones con varias filas y columnas.

## 4.1. Contenedor y elementos de la cuadrícula

Para utilizar Grid debemos aplicar `display: grid` al elemento contenedor:

```html
<section class="listado-eventos">
    <article class="tarjeta-evento">Evento 1</article>
    <article class="tarjeta-evento">Evento 2</article>
    <article class="tarjeta-evento">Evento 3</article>
</section>
```

```css
.listado-eventos {
    display: grid;
}
```

El elemento `.listado-eventos` se convierte en el **contenedor Grid** y sus hijos directos pasan a ser elementos de la cuadrícula.

## 4.2. Filas y columnas

Las columnas se definen mediante `grid-template-columns`:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```

La unidad `fr` representa una fracción del espacio disponible. En este ejemplo, el contenedor se divide en tres columnas iguales.

También podemos utilizar diferentes proporciones:

```css
.layout {
    display: grid;
    grid-template-columns: 2fr 1fr;
}
```

La primera columna ocupará el doble de espacio que la segunda.

Las filas pueden definirse mediante `grid-template-rows`:

```css
.layout {
    display: grid;
    grid-template-rows: auto 1fr auto;
}
```

## 4.3. Separación entre elementos

La propiedad `gap` define la separación entre filas y columnas:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
}
```

La función `repeat()` evita repetir manualmente el mismo valor:

```css
grid-template-columns: repeat(3, 1fr);
```

equivale a:

```css
grid-template-columns: 1fr 1fr 1fr;
```

También podemos establecer separaciones diferentes:

```css
.listado-eventos {
    row-gap: 2rem;
    column-gap: 1rem;
}
```

!!! salto-pagina-pdf ""

## 4.4. Cuadrículas adaptables

Una cuadrícula con tres columnas fijas puede quedar demasiado estrecha en pantallas pequeñas:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}
```

Podemos permitir que Grid determine automáticamente cuántas columnas caben:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1.5rem;
}
```

Esta declaración utiliza:

- `repeat()`: repite la definición de las columnas.
- `auto-fit`: crea tantas columnas como puedan caber.
- `minmax()`: establece un tamaño mínimo y uno máximo.
- `16rem`: anchura mínima deseada.
- `1fr`: permite que las columnas crezcan y ocupen el espacio disponible.

!!! example "Comportamiento esperado"

    Según el espacio disponible, el listado podrá mostrar:

    - Una columna en pantallas pequeñas.
    - Dos columnas en pantallas medianas.
    - Tres o más columnas en pantallas grandes.

Todo ello puede conseguirse sin utilizar todavía media queries.

!!! salto-pagina-pdf ""

## 4.5. Propiedades del contenedor

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `display: grid` | Activa el contexto de cuadrícula |
| `grid-template-columns` | Define el número y tamaño de las columnas |
| `grid-template-rows` | Define el número y tamaño de las filas |
| `gap` | Establece la separación entre elementos |
| `justify-items` | Alinea los elementos horizontalmente dentro de sus celdas |
| `align-items` | Alinea los elementos verticalmente dentro de sus celdas |
| `place-items` | Agrupa `align-items` y `justify-items` |

### Ejemplo de alineación

```css
.galeria {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    place-items: center;
    gap: 1rem;
}
```

Todos los elementos se alinearán en el centro de sus celdas.

!!! salto-pagina-pdf ""

## 4.6. Propiedades de los elementos

Los elementos de una cuadrícula pueden ocupar varias filas o columnas:

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `grid-column` | Establece las columnas que ocupa un elemento |
| `grid-row` | Establece las filas que ocupa un elemento |
| `justify-self` | Alinea horizontalmente un elemento concreto |
| `align-self` | Alinea verticalmente un elemento concreto |
| `place-self` | Agrupa `align-self` y `justify-self` |

```css
.elemento-destacado {
    grid-column: span 2;
}
```

El elemento ocupará el espacio correspondiente a dos columnas.

!!! warning "Elementos destacados"

    Antes de hacer que un elemento ocupe varias columnas debemos comprobar que la cuadrícula dispone de suficiente espacio. En pantallas pequeñas puede ser necesario devolverlo a una sola columna mediante una media query.


!!! salto-pagina-pdf ""

## 4.7. Ejemplo de listado de FestWeb

```html
<section class="listado-eventos">
    <article class="tarjeta-evento">
        <h2>Festival de música</h2>
        <p>Valencia · 20 de junio</p>
    </article>

    <article class="tarjeta-evento">
        <h2>Carrera popular</h2>
        <p>Alzira · 28 de junio</p>
    </article>

    <article class="tarjeta-evento">
        <h2>Exposición de arte</h2>
        <p>Gandia · 5 de julio</p>
    </article>
</section>
```

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1.5rem;
}

.tarjeta-evento {
    padding: 1rem;
    border: 1px solid #cccccc;
    border-radius: 0.75rem;
    background-color: #ffffff;
}
```

Las tarjetas tendrán la misma anchura dentro de cada fila y se reorganizarán automáticamente cuando cambie el espacio disponible.

!!! salto-pagina-pdf ""

## 4.8. Flexbox frente a Grid

Flexbox y Grid no son sistemas excluyentes. Pueden utilizarse conjuntamente.

| Criterio { .table-full-container .table-cl-secundario .table-bg-principal } | Flexbox { .table-cl-secundario .table-bg-principal } | CSS Grid { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| Dimensión | Una dimensión | Dos dimensiones |
| Organización | Fila o columna | Filas y columnas |
| Enfoque | Distribución del contenido | Estructura de la composición |
| Casos habituales | Navegaciones, botones y alineaciones | Tarjetas, galerías y layouts |
| Uso en FestWeb | Interior de los componentes | Distribución general de componentes |

### Uso combinado

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1.5rem;
}

.tarjeta-evento__acciones {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}
```

Grid distribuye las tarjetas y Flexbox organiza los botones dentro de cada una.

!!! salto-pagina-pdf ""

## 4.9. Errores frecuentes

- Aplicar propiedades Grid a un elemento que no es contenedor.
- Crear demasiadas columnas en pantallas pequeñas.
- Utilizar anchuras fijas dentro de columnas flexibles.
- Confundir las propiedades del contenedor con las de sus hijos.
- Utilizar Grid para una alineación sencilla que podría resolverse con Flexbox.
- Hacer que un elemento ocupe varias columnas sin comprobar tamaños pequeños.

## 4.10. Comprobación

Analiza la siguiente regla:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(18rem, 1fr));
    gap: 2rem;
}
```

Responde:

1. ¿Qué función cumple `auto-fit`?
2. ¿Cuál es la anchura mínima deseada para cada columna?
3. ¿Qué ocurre cuando aumenta el espacio disponible?
4. ¿Qué separación existe entre las tarjetas?
5. ¿Utilizarías Flexbox o Grid para distribuir los botones internos de cada tarjeta?

En la primera actividad guiada aplicaremos las unidades relativas, Flexbox y CSS Grid para transformar una interfaz rígida de FestWeb.

!!! salto-pagina-pdf ""