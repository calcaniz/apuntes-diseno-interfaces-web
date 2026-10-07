---
title: CSS, selectores y estilos homogéneos
---

En la unidad anterior definimos la estructura, la identidad visual y los componentes principales de **FestWeb**. Decidimos qué colores, tipografías y espaciados debía utilizar la interfaz y representamos su apariencia mediante wireframes y prototipos.

Sin embargo, una guía de estilo no modifica por sí misma una página web. Para trasladar esas decisiones al navegador necesitamos un lenguaje capaz de controlar la presentación de los documentos HTML.

Ese lenguaje es **CSS**.

CSS permite definir el color, la tipografía, las dimensiones, los espacios, los bordes y la disposición visual de los elementos de una página. También permite reutilizar las mismas reglas en diferentes pantallas y mantener una apariencia coherente en todo el sitio web.

> **Pregunta de partida:**  
> ¿Cómo podemos transformar la guía de estilo de FestWeb en un sistema de reglas que el navegador pueda aplicar de forma coherente a todas sus páginas?

## ¿Qué aprenderemos?

A lo largo de esta unidad aprenderemos a:

- Comprender la función de CSS dentro de una aplicación web.
- Incorporar estilos en línea, internos y externos.
- Seleccionar elementos HTML mediante diferentes tipos de selectores.
- Comprender cómo funcionan la cascada, la herencia y la especificidad.
- Aplicar unidades, colores y propiedades tipográficas.
- Controlar las dimensiones y los espacios mediante el modelo de caja.
- Crear clases y componentes visuales reutilizables.
- Organizar colores, tipografías y espaciados mediante propiedades personalizadas.
- Inspeccionar los estilos aplicados por el navegador.
- Detectar errores y validar una hoja de estilos.

!!! salto-pagina-pdf ""

## De una decisión visual a una regla CSS

En la guía de estilo de FestWeb establecimos decisiones como estas:

- El azul cian `#50C9E9` será el color principal.
- El azul `#3B82E6` se utilizará como color secundario.
- El color `#C6D8FF` se utilizará en fondos y superficies.
- El color `#213FC2` se utilizará para el texto.
- El color `#A3A313` permitirá destacar determinados elementos.
- El color `#E8B718` se utilizará para advertencias.
- Los títulos utilizarán una tipografía con mayor tamaño y peso.
- Las tarjetas tendrán espacios interiores regulares.
- Los botones cambiarán de apariencia cuando el usuario interactúe con ellos.
- Todos los componentes mantendrán una separación coherente.

CSS permite convertir cada una de estas decisiones en una regla que el navegador puede interpretar.

Por ejemplo:

```css
.button {
  padding: 0.75rem 1rem;
  color: #213FC2;
  background-color: #C6D8FF;
  border: 2px solid #50C9E9;
  border-radius: 0.5rem;
  font-weight: 600;
}
```

Esta regla no describe un botón concreto, sino la apariencia que podrán reutilizar todos los elementos que pertenezcan a la clase `.button`.

El objetivo de la unidad no será modificar elementos de forma aislada, sino construir un **sistema de estilos coherente y reutilizable**.

!!! salto-pagina-pdf ""

## Recorrido de la unidad

| Apartado { .table-full-container .table-cl-secundario .table-bg-principal } | Contenido { .table-cl-secundario .table-bg-principal } |
|---|---|
| [1. Introducción a CSS](02-introduccion-a-css.md) | Función de CSS, proceso de representación y anatomía de una regla. |
| [2. Incorporación y organización](03-incorporacion-y-organizacion.md) | Estilos en línea, hojas internas, hojas externas y buenas prácticas. |
| [3. Selectores CSS](04-selectores-css.md) | Selectores, combinadores, pseudoclases y pseudoelementos. |
| [4. Cascada, herencia y especificidad](05-cascada-herencia-especificidad.md) | Resolución de conflictos entre reglas CSS. |
| [5. Unidades, color y tipografía](06-unidades-color-tipografia.md) | Dimensiones, paleta cromática, fuentes y jerarquía visual. |
| [6. Modelo de caja](07-modelo-de-caja.md) | Contenido, relleno, borde, margen y representación de elementos. |
| [7. Componentes reutilizables](08-componentes-reutilizables.md) | Clases, BEM, propiedades personalizadas y redefinición de estilos. |
| [8. Inspección y validación](09-inspeccion-y-validacion.md) | Herramientas del navegador, depuración y validación CSS. |


> **Diseñar una interfaz no consiste en aplicar estilos elemento a elemento, sino en construir reglas que puedan reutilizarse de forma coherente.**


!!! salto-pagina-pdf ""