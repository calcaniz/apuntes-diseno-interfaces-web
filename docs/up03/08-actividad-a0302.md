---
title: 7. Actividad A03.02. FestWeb mobile first
---

# 7. Actividad A03.02. FestWeb mobile first

**Duración:** 55 minutos  
**Modalidad:** Actividad formativa guiada  
**Realización:** Sesión síncrona  
**Entrega:** No requiere entrega independiente  
**Criterio trabajado:** CE02-i

## 7.1. Objetivo

En la actividad anterior transformamos una interfaz rígida en una composición flexible utilizando unidades relativas, Flexbox y CSS Grid.

Ahora continuaremos trabajando sobre FestWeb para aplicar una estrategia **mobile first**. La interfaz deberá funcionar correctamente en móvil, tableta y escritorio mediante estilos base y media queries.

Al finalizar, FestWeb deberá:

- Mostrar una columna en pantallas estrechas.
- Reorganizar correctamente la cabecera y la navegación.
- Adaptar los botones al espacio disponible.
- Mostrar dos columnas en pantallas medianas.
- Mostrar tres columnas en pantallas grandes.
- Evitar el desplazamiento horizontal.
- Mantener el contenido y las funcionalidades en todos los tamaños.

## 7.2. Material de partida

Utiliza el resultado obtenido en la **A03.01**.

La estructura del proyecto será:

```text
A03.02/
├── index.html
├── css/
│   └── estilos.css
└── imagenes/
    ├── evento-musica.webp
    ├── evento-deporte.webp
    └── evento-cultura.webp
```

No debes crear una página nueva. El objetivo es adaptar mediante CSS la interfaz existente.

## 7.3. Organización de la sesión

| Fase { .table-full-container .table-cl-secundario .table-bg-principal } | Trabajo previsto { .table-cl-secundario .table-bg-principal } | Tiempo { .table-cl-secundario .table-bg-principal } |
|---|---|:---:|
| 1 | Comprobación inicial con DevTools | 5 min |
| 2 | Creación de los estilos base para móvil | 15 min |
| 3 | Adaptación para pantallas medianas | 10 min |
| 4 | Adaptación para escritorio | 10 min |
| 5 | Pruebas y correcciones | 10 min |
| 6 | Puesta en común | 5 min |

## 7.4. Comprobación inicial

Abre `index.html` en Chrome y activa las herramientas de desarrollo.

Comprueba la interfaz en estas anchuras:

- `390px`.
- `768px`.
- `1280px`.

Anota los problemas que encuentres.

Como mínimo, revisa:

- La cabecera.
- La navegación.
- El bloque de presentación.
- El listado de tarjetas.
- Los botones.
- Las imágenes.
- La posible aparición de desplazamiento horizontal.

!!! question "Pregunta inicial"

    ¿La interfaz se adapta de forma continua o únicamente funciona correctamente en el tamaño para el que fue diseñada?

## 7.5. Configuración del viewport

Comprueba que el documento HTML contiene la siguiente etiqueta:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Debe encontrarse dentro de `<head>`.

Sin esta configuración, los navegadores móviles pueden representar la página utilizando una anchura virtual de escritorio.

## 7.6. Estilos base para móvil

Los estilos situados fuera de las media queries corresponderán a la versión móvil.

### Contenedor principal

El contenedor debe ocupar el espacio disponible sin superar su anchura máxima.

```css
.contenedor {
    width: min(100% - 2rem, 75rem);
    margin-inline: auto;
}
```

### Cabecera

En la versión móvil, la cabecera se organizará verticalmente.

```css
.cabecera {
    white-space: normal;
}

.cabecera__contenido {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    gap: 1rem;
}
```

El logotipo se colocará en el centro.

```css
.logotipo {
    align-self: center;
}
```

El botón de acceso, que es hijo directo de `.cabecera__contenido`, ocupará toda la anchura disponible.

```css
.cabecera__contenido > .boton {
    width: 100%;
}
```

### Navegación

En el HTML proporcionado, los enlaces son hijos directos del elemento `.navegacion`.

```html
<nav class="navegacion" aria-label="Navegación principal">
    <a href="#">Inicio</a>
    <a href="#">Eventos</a>
    <a href="#">Categorías</a>
    <a href="#">Contacto</a>
</nav>
```

Por tanto, el propio elemento `.navegacion` será el contenedor Flexbox.

```css
.navegacion {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    width: 100%;
    text-align: center;
}
```

Los enlaces deberán disponer de una superficie cómoda para pulsar.

```css
.navegacion a {
    display: block;
    padding: 0.75rem 1rem;
}
```

### Presentación

El bloque de presentación debe ocupar todo el espacio disponible.

```css
.presentacion {
    width: 100%;
    padding-block: 2rem;
}

.presentacion__titulo,
.presentacion__descripcion {
    width: auto;
}
```

El título podrá adaptarse progresivamente al tamaño de la pantalla.

```css
.presentacion__titulo {
    font-size: clamp(2rem, 8vw, 3rem);
}
```

### Acciones de las tarjetas

En móvil, los botones de cada tarjeta se mostrarán verticalmente.

```css
.tarjeta-evento__acciones {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    white-space: normal;
}

.tarjeta-evento__acciones .boton {
    width: 100%;
}
```

### Listado de eventos

La versión móvil mostrará una única columna.

```css
.listado-eventos {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1.5rem;
}
```

Las tarjetas y sus imágenes no deben mantener una anchura fija.

```css
.tarjeta-evento,
.tarjeta-evento__imagen {
    width: 100%;
}

.tarjeta-evento__imagen {
    aspect-ratio: 16 / 10;
    height: auto;
    object-fit: cover;
}
```

## 7.7. Pantallas medianas

Añade una primera media query para pantallas con una anchura mínima de `48rem`.

En pantallas medianas:

1. La navegación se mostrará horizontalmente.
2. Las tarjetas se distribuirán en dos columnas.
3. Los botones de cada tarjeta compartirán una fila.
4. La cabecera de la sección de eventos se organizará horizontalmente.

```css
@media (min-width: 48rem) {
    .navegacion {
        flex-direction: row;
        justify-content: center;
        flex-wrap: wrap;
    }

    .tarjeta-evento__acciones {
        flex-direction: row;
        flex-wrap: wrap;
    }

    .tarjeta-evento__acciones .boton {
        width: auto;
    }

    .eventos__cabecera {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 1rem;
    }

    .listado-eventos {
        grid-template-columns: repeat(2, 1fr);
    }

    .presentacion {
        padding-block: 3rem;
    }
}
```

Comprueba el resultado alrededor de `768px`.

## 7.8. Pantallas grandes

Añade una segunda media query para pantallas con una anchura mínima de `64rem`.

En escritorio:

1. La cabecera se organizará horizontalmente.
2. El logotipo, la navegación y el botón de acceso compartirán una fila.
3. La navegación ocupará el espacio central.
4. El listado mostrará tres columnas.

```css
@media (min-width: 64rem) {
    .cabecera__contenido {
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    .logotipo {
        align-self: auto;
        flex: 0 0 auto;
    }

    .navegacion {
        width: auto;
        flex: 1;
    }

    .cabecera__contenido > .boton {
        width: auto;
        flex: 0 0 auto;
    }

    .listado-eventos {
        grid-template-columns: repeat(3, 1fr);
    }

    .presentacion {
        padding-block: 4rem;
    }
}
```

Comprueba el resultado alrededor de `1280px`.

## 7.7. Pantallas medianas

Añade una primera media query para pantallas con una anchura mínima de `48rem`.

```css
@media (min-width: 48rem) {
    /* Reglas para pantallas medianas */
}
```

Dentro de esta media query:

1. Coloca la navegación en horizontal.
2. Permite que los botones recuperen su anchura automática.
3. Muestra dos columnas de tarjetas.
4. Aumenta el espaciado del bloque de presentación.

```css
@media (min-width: 48rem) {
    .navegacion__lista {
        flex-direction: row;
        justify-content: center;
        flex-wrap: wrap;
    }

    .presentacion__acciones,
    .tarjeta-evento__acciones {
        flex-direction: row;
        flex-wrap: wrap;
    }

    .boton {
        width: auto;
    }

    .listado-eventos {
        grid-template-columns: repeat(2, 1fr);
    }

    .presentacion {
        padding: 2rem;
    }
}
```

Comprueba el resultado alrededor de `768px`.

## 7.8. Pantallas grandes

Añade una segunda media query para pantallas con una anchura mínima de `64rem`.

```css
@media (min-width: 64rem) {
    /* Reglas para pantallas grandes */
}
```

En escritorio:

1. La cabecera se organizará horizontalmente.
2. La marca, la navegación y el acceso compartirán la misma fila.
3. El listado mostrará tres columnas.
4. El bloque de presentación podrá aumentar su espaciado.

```css
@media (min-width: 64rem) {
    .cabecera__contenido {
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    .listado-eventos {
        grid-template-columns: repeat(3, 1fr);
    }

    .presentacion {
        padding: 3rem;
    }
}
```

Comprueba el resultado a `1280px`.

## 7.9. Revisión de la cascada

Ordena las media queries de menor a mayor anchura:

```css
/* Estilos base para móvil */

/* Pantallas medianas */
@media (min-width: 48rem) {
}

/* Pantallas grandes */
@media (min-width: 64rem) {
}
```

Este orden permite que las reglas para pantallas grandes redefinan correctamente los estilos anteriores.

No coloques la media query de `48rem` después de la de `64rem`, ya que podría sobrescribir algunos cambios de escritorio.

## 7.10. Pruebas finales

Utiliza DevTools para comprobar la interfaz en las siguientes anchuras:

| Anchura { .table-full-container .table-cl-secundario .table-bg-principal } | Resultado esperado { .table-cl-secundario .table-bg-principal } |
|---|---|
| `390px` | Cabecera vertical, botones amplios y una columna. |
| `768px` | Navegación horizontal y dos columnas. |
| `1280px` | Cabecera horizontal y tres columnas. |

Después, arrastra lentamente el borde de la simulación y comprueba los tamaños intermedios.

La actividad estará correctamente realizada cuando:

- No aparezca desplazamiento horizontal.
- Ningún texto quede cortado.
- Las imágenes mantengan sus proporciones.
- Los botones puedan utilizarse cómodamente.
- La navegación permanezca visible.
- Las tarjetas cambien de una a dos y tres columnas.
- Los breakpoints se activen en el orden previsto.
- No se haya ocultado contenido esencial.

## 7.11. Errores que deben evitarse

No resuelvas la actividad:

- Añadiendo una anchura fija diferente para cada dispositivo.
- Creando una media query para cada modelo de teléfono.
- Ocultando la navegación o información importante.
- Modificando el HTML cuando el problema puede resolverse con CSS.
- Utilizando `!important` para forzar las redefiniciones.
- Duplicando todas las reglas dentro de cada media query.

Las media queries deben contener únicamente las propiedades que realmente cambian.

## 7.12. Ampliación

Si terminas antes, sustituye las media queries del listado por una cuadrícula automática:

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

Compara ambos sistemas:

- Columnas definidas mediante media queries.
- Columnas automáticas mediante `auto-fit` y `minmax()`.

Indica qué solución se adapta mejor cuando la ventana tiene tamaños intermedios.

## 7.13. Puesta en común

Al finalizar la sesión, responde oralmente:

1. ¿Qué estilos forman la versión móvil?
2. ¿Por qué se utiliza `min-width`?
3. ¿Cuándo cambia la cabecera de vertical a horizontal?
4. ¿Qué ocurre con las tarjetas en cada breakpoint?
5. ¿Qué problemas pueden resolverse sin utilizar media queries?
6. ¿Por qué las media queries se ordenan de menor a mayor?

---
