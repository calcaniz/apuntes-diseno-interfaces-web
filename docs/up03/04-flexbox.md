---
title: Composición con Flexbox
---

# 3. Composición unidimensional con Flexbox

Flexbox es un sistema de composición que permite distribuir y alinear elementos a lo largo de un eje principal.

Resulta especialmente adecuado para:

- Menús de navegación.
- Cabeceras.
- Grupos de botones.
- Barras de herramientas.
- Alineación de iconos y textos.
- Componentes organizados en una fila o columna.

## 3.1. Contenedor y elementos flexibles

Para utilizar Flexbox debemos aplicar `display: flex` al elemento que contiene los componentes:

```html
<nav class="navegacion">
    <a href="#">Inicio</a>
    <a href="#">Eventos</a>
    <a href="#">Categorías</a>
    <a href="#">Contacto</a>
</nav>
```

```css
.navegacion {
    display: flex;
}
```

El elemento `.navegacion` se convierte en el **contenedor flexible** y sus enlaces pasan a ser **elementos flexibles**.

!!! warning "Relación directa"

    Flexbox solo afecta inicialmente a los hijos directos del contenedor. No modifica automáticamente los elementos situados en niveles inferiores.


!!! salto-pagina-pdf ""

## 3.2. Eje principal y eje transversal

Flexbox utiliza dos ejes:

- **Eje principal:** determina la dirección en la que se distribuyen los elementos.
- **Eje transversal:** es perpendicular al eje principal.

La orientación depende de `flex-direction`:

| Valor { .table-full-container .table-cl-secundario .table-bg-principal } | Eje principal { .table-cl-secundario .table-bg-principal } | Distribución { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| `row` | Horizontal | De izquierda a derecha |
| `row-reverse` | Horizontal | De derecha a izquierda |
| `column` | Vertical | De arriba hacia abajo |
| `column-reverse` | Vertical | De abajo hacia arriba |

```css
.navegacion {
    display: flex;
    flex-direction: row;
}
```

`row` es el valor predeterminado.

!!! salto-pagina-pdf ""

## 3.3. Propiedades del contenedor

Las principales propiedades que se aplican al contenedor flexible son:

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `display` | Activa el contexto Flexbox |
| `flex-direction` | Establece la dirección del eje principal |
| `justify-content` | Distribuye los elementos en el eje principal |
| `align-items` | Alinea los elementos en el eje transversal |
| `flex-wrap` | Permite que los elementos pasen a otra línea |
| `gap` | Define la separación entre elementos |

### Distribución en el eje principal

```css
.navegacion {
    display: flex;
    justify-content: space-between;
}
```

Algunos valores habituales de `justify-content` son:

- `flex-start`
- `center`
- `flex-end`
- `space-between`
- `space-around`
- `space-evenly`

### Alineación en el eje transversal

```css
.cabecera {
    display: flex;
    align-items: center;
}
```

`align-items: center` centra verticalmente los elementos cuando el eje principal es horizontal.

!!! info "Recuerda"

    `justify-content` actúa sobre el eje principal y `align-items` sobre el eje transversal. Si cambia `flex-direction`, también cambia la orientación de los ejes.

## 3.4. Separación y salto de línea

La propiedad `gap` permite establecer una separación uniforme sin utilizar márgenes individuales:

```css
.navegacion {
    display: flex;
    gap: 1rem;
}
```

Cuando los elementos no caben, `flex-wrap` permite que pasen a una nueva línea:

```css
.navegacion {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}
```

Esto evita que los enlaces se compriman excesivamente o desborden su contenedor.

## 3.5. Propiedades de los elementos flexibles

Algunas propiedades se aplican directamente a los hijos:

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `flex-grow` | Indica cuánto puede crecer un elemento |
| `flex-shrink` | Indica cuánto puede reducirse |
| `flex-basis` | Establece su tamaño inicial |
| `flex` | Agrupa crecimiento, reducción y tamaño inicial |
| `align-self` | Modifica la alineación de un elemento concreto |
| `order` | Cambia su posición visual |

La propiedad abreviada `flex` combina tres valores:

```css
.elemento {
    flex: 1 1 15rem;
}
```

Esto significa:

1. Puede crecer.
2. Puede reducirse.
3. Parte de un tamaño inicial de `15rem`.

!!! warning "Contenedor frente a elemento"

    `justify-content`, `align-items` y `flex-wrap` pertenecen al contenedor.  
    `flex`, `align-self` y `order` pertenecen a los elementos flexibles.

## 3.6. Ejemplo de cabecera de FestWeb

```html
<header class="cabecera">
    <a class="logotipo" href="#">FestWeb</a>

    <nav class="navegacion">
        <a href="#">Inicio</a>
        <a href="#">Eventos</a>
        <a href="#">Categorías</a>
    </nav>

    <a class="boton boton--principal" href="#">Acceder</a>
</header>
```

```css
.cabecera {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
    padding: 1rem;
}

.navegacion {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}

.logotipo {
    font-size: 1.5rem;
    font-weight: 700;
}
```

La cabecera distribuye sus tres bloques horizontalmente. Si el espacio disponible disminuye, `flex-wrap` permite que alguno pase a una nueva línea.

## 3.7. Grupo de acciones

Flexbox también puede utilizarse dentro de una tarjeta:

```html
<div class="tarjeta-evento__acciones">
    <a class="boton boton--principal" href="#">Ver evento</a>
    <button class="boton boton--secundario">Guardar</button>
</div>
```

```css
.tarjeta-evento__acciones {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}

.tarjeta-evento__acciones .boton {
    flex: 1 1 10rem;
}
```

Los botones pueden crecer hasta ocupar el espacio disponible y pasar a una nueva línea cuando no caben.

## 3.8. Errores frecuentes

- Aplicar `justify-content` a un elemento que no es contenedor flex.
- Confundir el eje principal con el transversal.
- Utilizar márgenes individuales en lugar de `gap`.
- Mantener `flex-wrap: nowrap` cuando los elementos no caben.
- Cambiar el orden visual sin comprobar el orden lógico del HTML.
- Asignar anchuras fijas que impiden que los elementos se adapten.

!!! warning "Orden visual y accesibilidad"

    La propiedad `order` modifica la posición visual, pero no cambia el orden del contenido en el documento HTML. Debe utilizarse con cuidado para no crear una navegación incoherente mediante teclado o tecnologías de asistencia.

## 3.9. Comprobación

Analiza la siguiente regla:

```css
.navegacion {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
    gap: 1rem;
}
```

Responde:

1. ¿Cuál es el eje principal?
2. ¿En qué dirección se distribuyen los enlaces?
3. ¿Sobre qué eje actúa `justify-content`?
4. ¿Qué efecto produce `align-items: flex-end`?
5. ¿Qué propiedad añadirías para permitir varias líneas?

En el siguiente apartado utilizaremos CSS Grid para crear composiciones organizadas simultáneamente en filas y columnas.


!!! salto-pagina-pdf ""