---
title: Cascada, herencia y especificidad
---

En CSS, varias reglas pueden modificar la misma propiedad de un elemento.

```css
a {
  color: #3B82E6;
}

.event-card a {
  color: #A3A313;
}

.event-card__link {
  color: #213FC2;
}
```

Las tres reglas podrían aplicarse al mismo enlace. El navegador necesita decidir cuál debe prevalecer.

Para resolver estos conflictos utiliza la **cascada**.

> **Pregunta de partida:**  
> Cuando varias reglas modifican la misma propiedad, ¿cómo decide el navegador cuál debe aplicar?

## 4.1. Funcionamiento de la cascada

La cascada es el algoritmo que determina el valor final de cada propiedad CSS.

Para comprender los conflictos habituales utilizaremos este orden simplificado:

1. Origen e importancia.
2. Especificidad.
3. Orden de aparición.

La especificidad no se comprueba primero. Antes se tiene en cuenta el origen de las reglas y si alguna declaración está marcada como `!important`.

## 4.2. Origen e importancia

Las reglas CSS pueden proceder de diferentes orígenes:

- **Navegador:** estilos predeterminados.
- **Usuario:** preferencias definidas por la persona usuaria.
- **Autor:** estilos creados por el desarrollador.

En las declaraciones normales, los estilos del autor prevalecen sobre los estilos normales del usuario y del navegador.

Cuando aparece `!important`, el orden se invierte para proteger las preferencias importantes del usuario.

| Prioridad { .table-full-container .table-cl-secundario .table-bg-principal } | Tipo de declaración { .table-cl-secundario .table-bg-principal } |
|:---:|---|
| 1 | Declaraciones normales del navegador |
| 2 | Declaraciones normales del usuario |
| 3 | Declaraciones normales del autor |
| 4 | Declaraciones importantes del autor |
| 5 | Declaraciones importantes del usuario |
| 6 | Declaraciones importantes del navegador |

En la mayoría de nuestros ejercicios trabajaremos con reglas creadas por el autor.

## 4.3. Herencia

La herencia permite que determinadas propiedades aplicadas a un elemento padre se transmitan a sus descendientes.

```css
body {
  color: #213FC2;
  font-family: Arial, sans-serif;
}
```

Los textos situados dentro de `<body>` heredarán normalmente el color y la familia tipográfica.

Las propiedades relacionadas con el texto suelen heredarse:

- `color`
- `font-family`
- `font-size`
- `line-height`

!!! salto-pagina-pdf ""

Las propiedades relacionadas con el modelo de caja no suelen heredarse:

- `margin`
- `padding`
- `border`
- `width`
- `height`

Podemos controlar la herencia mediante algunas palabras clave:

| Valor { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `inherit` | Utiliza el valor del elemento padre |
| `initial` | Recupera el valor inicial de la propiedad |
| `unset` | Hereda si la propiedad es heredable; en caso contrario, utiliza su valor inicial |
| `revert` | Recupera el valor establecido por un origen anterior de la cascada |

Ejemplo:

```css
.event-card {
  color: #213FC2;
}

.event-card__link {
  color: inherit;
}
```

El enlace utilizará el mismo color que la tarjeta.

!!! salto-pagina-pdf ""

## 4.4. Especificidad

Si dos declaraciones pertenecen al mismo origen y tienen la misma importancia, el navegador compara la **especificidad** de sus selectores.

La especificidad puede representarse mediante una tupla:

```text
(A, B, C)
```

- **A:** número de identificadores.
- **B:** número de clases, atributos y pseudoclases.
- **C:** número de etiquetas y pseudoelementos.

| Selector { .table-full-container .table-cl-secundario .table-bg-principal } | Especificidad { .table-cl-secundario .table-bg-principal } |
|---|:---:|
| `h2` | `(0,0,1)` |
| `.event-card` | `(0,1,0)` |
| `.event-card a` | `(0,1,1)` |
| `.event-card__link:hover` | `(0,2,0)` |
| `#featured-event .button` | `(1,1,0)` |

Los valores se comparan de izquierda a derecha.

Por tanto:

```text
(1,0,0) supera a (0,20,20)
```

Un único identificador tiene más peso que cualquier cantidad de clases o etiquetas.

Por este motivo evitaremos utilizar identificadores para aplicar estilos reutilizables.

!!! salto-pagina-pdf ""

## 4.5. Orden de aparición

Si dos reglas tienen el mismo origen, importancia y especificidad, prevalece la que aparece más tarde.

```css
.button {
  border-color: #50C9E9;
}

.button {
  border-color: #3B82E6;
}
```

Ambas reglas utilizan el mismo selector. Por tanto, se aplicará:

```css
border-color: #3B82E6;
```

El orden también afecta a las hojas externas.

```html
<link rel="stylesheet" href="css/base.css">
<link rel="stylesheet" href="css/custom.css">
```

Si ambas hojas contienen reglas con la misma especificidad, las declaraciones de `custom.css` podrán reemplazar a las de `base.css`.

## 4.6. Estilos en línea

Los estilos escritos mediante el atributo `style` tienen prioridad sobre las declaraciones normales incluidas en las hojas del autor.

```html
<a
  class="button"
  href="evento.html"
  style="color: #A3A313;"
>
  Ver evento
</a>
```

```css
.button {
  color: #213FC2;
}
```

En este caso se aplicará el color del atributo `style`.

Esto no significa que los estilos en línea tengan prioridad absoluta. Una declaración importante puede prevalecer sobre un estilo en línea normal.

## 4.7. Uso de `!important`

La marca `!important` aumenta la prioridad de una declaración.

```css
.button {
  color: #213FC2 !important;
}
```

Debe utilizarse únicamente en situaciones excepcionales.

Su abuso puede provocar una cadena de reglas difíciles de sobrescribir:

```css
.button {
  color: #213FC2 !important;
}

.event-card .button {
  color: #A3A313 !important;
}

#featured-event .button {
  color: #3B82E6 !important;
}
```

Antes de utilizar `!important`, debemos comprobar:

1. El orden de las reglas.
2. La clase aplicada al elemento.
3. La especificidad.
4. La herencia.
5. El valor calculado por el navegador.

## 4.8. Ejemplo en FestWeb

Partimos de este enlace:

```html
<article class="event-card">
  <a class="event-card__link" href="evento.html">
    Ver evento
  </a>
</article>
```

Y aplicamos estas reglas:

```css
a {
  color: #3B82E6;
}

.event-card a {
  color: #A3A313;
}

.event-card__link {
  color: #213FC2;
}
```

La especificidad es:

| Selector { .table-full-container .table-cl-secundario .table-bg-principal } | Especificidad { .table-cl-secundario .table-bg-principal } |
|---|:---:|
| `a` | `(0,0,1)` |
| `.event-card a` | `(0,1,1)` |
| `.event-card__link` | `(0,1,0)` |

La regla ganadora es:

```css
.event-card a {
  color: #A3A313;
}
```

Aunque `.event-card__link` identifica directamente el enlace, `.event-card a` tiene mayor especificidad porque combina una clase y una etiqueta.

Para evitar este tipo de conflictos, conviene utilizar selectores sencillos y una organización predecible.

!!! salto-pagina-pdf ""

## 4.9. Inspección de conflictos

Las herramientas de desarrollo del navegador permiten seleccionar un elemento y revisar las reglas que recibe.

En el panel *Styles*:

- Las declaraciones aplicadas aparecen activas.
- Las declaraciones reemplazadas aparecen tachadas.
- El navegador muestra el archivo y la línea de cada regla.
- Podemos activar o desactivar propiedades temporalmente.

Esta información permite resolver conflictos sin añadir selectores más largos o utilizar `!important` innecesariamente.

> **Comprender la cascada permite resolver los conflictos CSS sin aumentar innecesariamente la complejidad de los selectores.**

!!! salto-pagina-pdf ""