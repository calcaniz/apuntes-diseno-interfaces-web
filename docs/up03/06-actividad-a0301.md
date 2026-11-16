---
title: A03.01. De la interfaz rígida a la composición flexible
---

# 5. A03.01. De la interfaz rígida a la composición flexible

| Duración { .table-full-container .table-cl-secundario .table-bg-principal } | Modalidad { .table-cl-secundario .table-bg-principal } | Evaluación { .table-cl-secundario .table-bg-principal } |
|:---:|:---:|:---:|
| 55 minutos | Individual y guiada | Actividad formativa |

## 5.1. Objetivo

En esta actividad transformaremos una página rígida de FestWeb en una composición flexible utilizando:

- Unidades relativas.
- Contenedores fluidos.
- Imágenes adaptables.
- Flexbox.
- CSS Grid.

Todavía no utilizaremos media queries. La composición deberá adaptarse mediante las características propias de Flexbox y Grid.

## 5.2. Punto de partida

Descarga y descomprime el proyecto inicial proporcionado.

La carpeta contendrá:

```text
A03.01/
├── index.html
├── css/
│   └── estilos.css
└── imagenes/
    ├── evento-musica.webp
    ├── evento-deporte.webp
    └── evento-cultura.webp
```

La página contiene:

- Una cabecera.
- Un logotipo.
- Una navegación.
- Un listado de eventos.
- Tres tarjetas.
- Un grupo de acciones dentro de cada tarjeta.

No modifiques la estructura HTML durante la primera parte de la actividad.

## 5.3. Diagnóstico inicial

Abre `index.html` en el navegador y utiliza el modo dispositivo de DevTools para comprobar la página con estas anchuras:

| Comprobación { .table-full-container .table-cl-secundario .table-bg-principal } | Anchura { .table-cl-secundario .table-bg-principal } | Aspectos que debes observar { .table-cl-secundario .table-bg-principal } |
|---|:---:|---|
| Móvil | `390px` | Desbordamiento, imágenes y navegación |
| Tableta | `768px` | Anchura de las tarjetas y espacios disponibles |
| Escritorio | `1280px` | Distribución general y anchura del contenedor |

Localiza en `estilos.css` las declaraciones responsables de los principales problemas.

!!! question "Puesta en común"

    Antes de modificar el código, identifica:

    1. Un elemento que provoque desplazamiento horizontal.
    2. Una imagen que supere su contenedor.
    3. Un grupo de elementos que debería utilizar Flexbox.
    4. Un listado que debería utilizar CSS Grid.

## 5.4. Preparar el modelo de caja

Añade al comienzo de `estilos.css`:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

Comprueba que el relleno y los bordes quedan incluidos dentro de las dimensiones declaradas.

## 5.5. Crear un contenedor fluido

Localiza la regla `.contenedor` y sustituye su anchura fija:

```css
.contenedor {
    width: 1200px;
    margin-inline: auto;
}
```

por una composición adaptable:

```css
.contenedor {
    width: min(75rem, calc(100% - 2rem));
    margin-inline: auto;
}
```

Comprueba nuevamente la página con una anchura de `390px`.

El contenido deberá mantener un margen mínimo a ambos lados sin superar los `75rem`.

## 5.6. Adaptar las imágenes

Añade una regla general para evitar que las imágenes superen sus contenedores:

```css
img {
    max-width: 100%;
    height: auto;
    display: block;
}
```

Después, aplica una proporción común a las imágenes de los eventos:

```css
.tarjeta-evento__imagen {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
}
```

Comprueba que todas las tarjetas mantienen una apariencia coherente aunque sus imágenes originales tengan tamaños diferentes.

## 5.7. Organizar la cabecera con Flexbox

Convierte el contenido de la cabecera en un contenedor flexible:

```css
.cabecera__contenido {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
}
```

Organiza también los enlaces de navegación:

```css
.navegacion {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}
```

Comprueba que:

- El logotipo, la navegación y el acceso se distribuyen correctamente.
- Los elementos pueden pasar a otra línea.
- No aparece desplazamiento horizontal.

## 5.8. Crear el listado con CSS Grid

Localiza la regla del listado de eventos y elimina las anchuras fijas.

Aplica la siguiente composición:

```css
.listado-eventos {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1.5rem;
}
```

Cambia progresivamente la anchura del navegador y observa cuándo se reorganizan las tarjetas.

No hemos definido tamaños concretos de dispositivos: Grid crea las columnas según el espacio disponible.

## 5.9. Organizar las acciones de las tarjetas

Convierte el grupo de botones de cada tarjeta en un contenedor flexible:

```css
.tarjeta-evento__acciones {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}
```

Permite que los botones ocupen el espacio disponible:

```css
.tarjeta-evento__acciones .boton {
    flex: 1 1 10rem;
    text-align: center;
}
```

Los botones deberán permanecer legibles y pasar a otra línea cuando no dispongan de suficiente espacio.

## 5.10. Reto final

Selecciona una de estas mejoras:

### Opción A. Tarjetas de altura coherente

Convierte cada tarjeta en un contenedor flexible vertical y sitúa las acciones en su parte inferior:

```css
.tarjeta-evento {
    display: flex;
    flex-direction: column;
}

.tarjeta-evento__acciones {
    margin-top: auto;
}
```

### Opción B. Título adaptable

Utiliza `clamp()` para adaptar el título principal:

```css
.presentacion__titulo {
    font-size: clamp(2rem, 5vw, 4rem);
}
```

Explica al docente qué límites has establecido y por qué.

## 5.11. Comprobación final

Antes de terminar, revisa la página con las siguientes anchuras:

| Anchura { .table-full-container .table-cl-secundario .table-bg-principal } | Resultado esperado { .table-cl-secundario .table-bg-principal } |
|:---:|---|
| `390px` | Una columna de tarjetas sin desbordamiento horizontal |
| `768px` | Una o dos columnas según el espacio disponible |
| `1280px` | Varias columnas y contenedor centrado |
| `1600px` | El contenido deja de crecer al alcanzar su anchura máxima |

Comprueba también que:

- Las imágenes mantienen su proporción.
- La navegación puede pasar a otra línea.
- Las tarjetas se reorganizan automáticamente.
- Los botones permanecen visibles y utilizables.
- No se ha utilizado `overflow-x: hidden` para ocultar errores.
- No se han añadido media queries.


