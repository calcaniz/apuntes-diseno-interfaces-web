---
title: A02.01. Laboratorio CSS (Simplificada)
---

# A02.01. Laboratorio CSS (Simplificada)

**Duración:** 55 minutos  
**Modalidad:** Trabajo individual guiado  
**Apartados relacionados:** 1, 2, 3 y 4  
**Carácter:** Actividad formativa  

## 1. Punto de partida

En los primeros apartados de la unidad hemos aprendido que HTML describe la estructura y el contenido de una página, mientras que CSS controla su presentación.

En esta actividad transformaremos progresivamente una página básica de FestWeb:

1. Aplicaremos estilos directamente sobre los elementos.
2. Trasladaremos esos estilos a una hoja interna.
3. Crearemos una hoja CSS externa.
4. Utilizaremos diferentes selectores.
5. Aplicaremos estados de interacción.
6. Resolveremos un conflicto relacionado con la cascada y la especificidad.

!!! info "Objetivo de la actividad"

    Al finalizar la sesión deberás ser capaz de explicar por qué una hoja de estilos externa facilita la reutilización y el mantenimiento del diseño de una página web.

## 2. Material necesario

Utiliza la carpeta inicial proporcionada en la actividad

La estructura será similar a la siguiente:

```text
festweb/
├── index.html
├── css/
│   └── conflictos.css
└── imagenes/
    ├── evento-musica.svg
    ├── evento-deporte.svg
    └── evento-cultura.svg
```

Antes de comenzar:

1. Abre la carpeta completa en Visual Studio Code.
2. Abre `index.html` en el navegador.
3. Identifica visualmente:
    - La cabecera.
    - La navegación.
    - La presentación.
    - Las tarjetas de eventos.
    - El formulario.
4. Revisa las clases y atributos existentes en el HTML.

!!! warning "Importante"

    No modifiques el contenido ni la estructura de `index.html`, excepto cuando se indique expresamente.

## 3. Primera prueba: estilos en línea

Localiza la etiqueta `<body>` y añade temporalmente:

```html
<body style="background-color: #c6d8ff; color: #213fc2;">
```

Localiza el elemento que contiene el lema de FestWeb y añade:

```html
<p
  class="lema"
  style="font-size: 2rem; font-weight: 700; text-align: center;"
>
  Encuentra planes, comparte experiencias
</p>
```

Guarda el archivo y actualiza la página en el navegador.

👀 **Comprueba**

- ¿Ha cambiado el fondo de toda la página?
- ¿Qué elementos han heredado el color definido en `<body>`?
- ¿El estilo del lema afecta a algún otro párrafo?

❓ **Piensa**

¿Qué ocurriría si tuviéramos cincuenta tarjetas y escribiéramos sus estilos directamente dentro de cada elemento?

## 4. Segunda prueba: hoja de estilos interna

Una hoja interna permite agrupar las reglas CSS dentro del propio documento HTML mediante el elemento `<style>`.

1. Elimina los atributos `style` añadidos en el apartado anterior.
2. Dentro de `<head>`, añade:

```html
<style>
  body {
    background-color: #c6d8ff;
    color: #213fc2;
  }

  .lema {
    font-size: 2rem;
    font-weight: 700;
    text-align: center;
  }
</style>
```

3. Guarda los cambios y actualiza la página.

👀 **Comprueba**

La apariencia debería ser prácticamente la misma que en la prueba anterior, pero ahora las decisiones visuales están agrupadas en una zona común.

❓ **Piensa**

¿Podría otra página HTML utilizar directamente estas reglas?

## 5. Tercera prueba: hoja de estilos externa

Una hoja externa permite compartir las mismas reglas entre diferentes páginas. Esta será la opción principal utilizada en FestWeb.

### 5.1. Crear el archivo CSS

Dentro de la carpeta `css`, crea el archivo:

```text
estilos.css
```

Copia en él las reglas que se encontraban dentro del elemento `<style>`:

```css
body {
  background-color: #c6d8ff;
  color: #213fc2;
}

.lema {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
}
```

### 5.2. Vincular la hoja externa

Elimina el elemento `<style>` de `index.html`.

Dentro de `<head>`, añade:

```html
<link rel="stylesheet" href="css/estilos.css">
```

Guarda los dos archivos y actualiza la página.

👀 **Comprueba**

- La apariencia debe mantenerse.
- La pestaña **Network** del navegador no debe mostrar un error `404`.
- Si modificas una regla en `estilos.css`, el cambio debe aparecer al actualizar.

!!! warning "Si los estilos no aparecen"

    Comprueba:

    1. El nombre del archivo.
    2. La extensión `.css`.
    3. La ruta escrita en `href`.
    4. Que el elemento `<link>` se encuentre dentro de `<head>`.
    5. Que el navegador no esté mostrando una versión anterior almacenada.

## 6. Aplicación de selectores

A partir de este momento trabajaremos únicamente sobre `css/estilos.css`.

Añade un comentario antes de cada grupo de reglas para indicar qué tipo de selector estás utilizando.

### 6.1. Selector de etiqueta

Modifica todos los títulos de segundo y tercer nivel:

```css
/* Selector agrupado de etiquetas */
h2,
h3 {
  color: #213fc2;
}
```

### 6.2. Selector de clase

Define la apariencia básica de todas las tarjetas:

```css
/* Selector de clase */
.tarjeta-evento {
  background-color: #ffffff;
  border: 1px solid #3b82e6;
  border-radius: 0.75rem;
  margin: 0.5rem;
  padding: 1rem;
}
```

### 6.3. Combinación de clases

Modifica únicamente las tarjetas que posean simultáneamente las clases `tarjeta-evento` y `destacada`:

```css
/* Un mismo elemento debe poseer las dos clases */
.tarjeta-evento.destacada {
  border-width: 3px;
}
```

!!! note "Observa el selector"

    En `.tarjeta-evento.destacada` no hay ningún espacio. Las dos clases deben pertenecer al mismo elemento.

### 6.4. Selector de atributo

Identifica visualmente los campos obligatorios del formulario:

```css
/* Elementos que contienen el atributo required */
[required] {
  border-left: 4px solid #e8b718;
}
```

👀 **Comprueba**

Utiliza el inspector del navegador para verificar qué elementos coinciden con cada selector.

## 7. Estados de interacción

Los enlaces y botones deben informar visualmente sobre su estado.

Añade las siguientes reglas:

```css
/* Apariencia básica del botón */
.boton {
  display: inline-block;
  background-color: #50c9e9;
  border: 2px solid #213fc2;
  border-radius: 0.5rem;
  color: #213fc2;
  padding: 0.75rem 1rem;
  text-decoration: none;
}

/* Estado al situar el puntero */
.boton:hover {
  background-color: #3b82e6;
  color: #ffffff;
}

/* Estado de navegación mediante teclado */
.boton:focus-visible {
  outline: 3px solid #e8b718;
  outline-offset: 3px;
}

/* Estado durante la pulsación */
.boton:active {
  transform: translateY(2px);
}
```

👀 **Comprueba**

1. Sitúa el puntero sobre el botón.
2. Haz clic y mantén el botón pulsado.
3. Utiliza la tecla `Tab` para acceder al botón.
4. Comprueba que el foco de teclado sea claramente visible.

!!! warning "Accesibilidad"

    No elimines el contorno del foco mediante `outline: none` si no proporcionas una alternativa claramente visible.

## 8. Cascada, herencia y especificidad

Abre el archivo proporcionado:

```text
css/conflictos.css
```

Vincúlalo después de la hoja principal:

```html
<link rel="stylesheet" href="css/estilos.css">
<link rel="stylesheet" href="css/conflictos.css">
```

El orden es importante: las reglas de `conflictos.css` se procesarán después de las reglas de `estilos.css`.

### 8.1. Conflicto de especificidad

Añade temporalmente estas reglas a `conflictos.css`:

```css
.presentacion .boton {
  background-color: #3b82e6;
}

.boton {
  background-color: #50c9e9;
}
```

Aunque `.boton` aparece después, la primera regla puede prevalecer porque su selector es más específico.

👀 **Comprueba**

1. Selecciona el botón con el inspector.
2. Localiza la propiedad `background-color`.
3. Observa qué declaración aparece tachada.
4. Identifica la regla que finalmente se aplica.

### 8.2. Conflicto por orden

Añade:

```css
.tarjeta-evento {
  border-color: #50c9e9;
}

.tarjeta-evento {
  border-color: #213fc2;
}
```

Las dos reglas tienen la misma especificidad. En este caso prevalece la última.

❓ **Responde**

- ¿Por qué gana la segunda regla?
- ¿Qué diferencia hay respecto al conflicto anterior?
- ¿Qué color definido en `body` se hereda en otros elementos?

!!! danger "No utilices esta solución"

    No resuelvas los conflictos añadiendo `!important`. Primero debes comprender qué regla gana y por qué.

## 9. Pequeño reto individual

Realiza estas modificaciones:

1. Utiliza un selector descendiente para seleccionar los enlaces situados dentro de la navegación.
2. Añade un estilo para los controles deshabilitados mediante `:disabled`.
3. Utiliza `::before` o `::after` para añadir un elemento exclusivamente decorativo.
4. Añade un comentario que explique qué elementos selecciona cada regla.

El pseudoelemento no deberá contener información necesaria para comprender la página.
