---
title: Unidades, color y tipografía
---

# 5. Unidades, color y tipografía

Una interfaz web no solo debe funcionar correctamente. También debe presentar la información de forma clara, legible y coherente.

CSS permite controlar el tamaño de los elementos, aplicar una paleta cromática y establecer una jerarquía tipográfica. Estas decisiones deben seguir la guía de estilo definida para el proyecto.

> **Pregunta de partida:**  
> ¿Por qué una página puede resultar difícil de utilizar aunque todos sus textos y botones funcionen correctamente?

## 5.1. Unidades de medida en CSS

Muchas propiedades CSS necesitan un valor numérico acompañado de una unidad:

```css
h1 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

.tarjeta-evento {
  width: 90%;
  padding: 1rem;
}
```

Las unidades pueden dividirse en dos grandes grupos.

### Unidades absolutas

Las unidades absolutas mantienen un tamaño fijo y no dependen directamente de otro elemento.

La más utilizada en pantalla es el píxel:

```css
.logotipo {
  width: 180px;
}

.tarjeta-evento {
  border-radius: 8px;
}
```

El píxel resulta útil para definir bordes, iconos, radios de esquina o tamaños concretos. Sin embargo, utilizar únicamente píxeles puede dificultar la adaptación de la interfaz a diferentes pantallas o preferencias de usuario.

!!! salto-pagina-pdf ""

### Unidades relativas

Las unidades relativas calculan su tamaño tomando como referencia otro valor.

| Unidad { .table-full-container .table-cl-secundario .table-bg-principal } | Referencia { .table-cl-secundario .table-bg-principal } | Uso habitual { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| `%` | Tamaño del elemento contenedor | Anchuras y dimensiones flexibles |
| `em` | Tamaño de letra del elemento o de su contexto | Espaciados relacionados con un componente |
| `rem` | Tamaño de letra del elemento raíz | Tipografía y espaciados generales |
| `vw` | Anchura de la ventana del navegador | Elementos relacionados con la pantalla |
| `vh` | Altura de la ventana del navegador | Secciones o portadas |

```css
html {
  font-size: 16px;
}

h1 {
  font-size: 2rem;
}

.contenido {
  width: 90%;
  max-width: 75rem;
}
```

Si el tamaño raíz es de `16px`, un valor de `2rem` equivale inicialmente a `32px`. Al estar relacionado con el tamaño raíz, puede adaptarse mejor a las preferencias configuradas por el usuario.

!!! tip "Recomendación"
    Utiliza `rem` para el tamaño del texto y los espaciados generales, porcentajes para anchuras flexibles y píxeles cuando necesites medidas pequeñas y concretas.

## 5.2. El color en CSS

CSS permite representar los colores de distintas formas.

```css
.ejemplo {
  color: blue;
  color: #213fc2;
  color: rgb(33, 63, 194);
  color: hsl(228, 71%, 45%);
}
```

Los formatos más habituales son:

| Formato { .table-full-container .table-cl-secundario .table-bg-principal } | Ejemplo { .table-cl-secundario .table-bg-principal } | Características { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| Nombre | `blue` | Fácil de leer, pero ofrece poco control |
| Hexadecimal | `#213FC2` | Muy utilizado en guías de estilo |
| RGB | `rgb(33, 63, 194)` | Define la cantidad de rojo, verde y azul |
| RGBA | `rgb(33 63 194 / 50%)` | Permite incorporar transparencia |
| HSL | `hsl(228, 71%, 45%)` | Representa tono, saturación y luminosidad |

!!! salto-pagina-pdf ""

## 5.3. Paleta cromática de FestWeb

FestWeb utilizará la paleta definida previamente en su guía de estilo:

| Función { .table-full-container .table-cl-secundario .table-bg-principal } | Color { .table-cl-secundario .table-bg-principal } | Código { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| Principal | Azul claro | `#50C9E9` |
| Secundario | Azul | `#3B82E6` |
| Fondo | Azul muy claro | `#C6D8FF` |
| Acento | Verde oliva | `#A3A313` |
| Texto | Azul oscuro | `#213FC2` |
| Advertencia | Amarillo | `#E8B718` |

Para evitar repetir los códigos en todo el documento, podemos guardarlos como propiedades personalizadas de CSS:

```css
:root {
  --color-principal: #50c9e9;
  --color-secundario: #3b82e6;
  --color-fondo: #c6d8ff;
  --color-acento: #a3a313;
  --color-texto: #213fc2;
  --color-advertencia: #e8b718;
}
```

Después se utilizan mediante la función `var()`:

```css
body {
  color: var(--color-texto);
  background-color: var(--color-fondo);
}

.boton-principal {
  color: var(--color-texto);
  background-color: var(--color-principal);
}
```

Si posteriormente cambia un color de la guía de estilo, solo será necesario modificar su valor en `:root`.

## 5.4. Propiedades tipográficas

La tipografía influye directamente en la legibilidad y en la jerarquía visual de la interfaz.

Las principales propiedades tipográficas son:

| Propiedad { .table-full-container .table-cl-secundario .table-bg-principal } | Función { .table-cl-secundario .table-bg-principal } |
|---|---|
| `font-family` | Establece la familia tipográfica |
| `font-size` | Define el tamaño del texto |
| `font-weight` | Controla el grosor |
| `font-style` | Aplica estilos como la cursiva |
| `line-height` | Define la separación entre líneas |
| `letter-spacing` | Modifica la separación entre caracteres |
| `text-align` | Alinea el texto |
| `text-decoration` | Añade o elimina decoraciones |
| `text-transform` | Transforma el uso de mayúsculas y minúsculas |

!!! salto-pagina-pdf ""

Ejemplo:

```css
body {
  font-family: "Inter", Arial, sans-serif;
  font-size: 1rem;
  line-height: 1.6;
  color: var(--color-texto);
}

h1 {
  font-size: 2.25rem;
  font-weight: 700;
  line-height: 1.2;
}

h2 {
  font-size: 1.5rem;
  font-weight: 600;
}

.texto-auxiliar {
  font-size: 0.875rem;
}
```

En `font-family` es recomendable indicar varias alternativas:

```css
font-family: "Inter", Arial, sans-serif;
```

El navegador intentará utilizar `Inter`. Si no está disponible, empleará `Arial` y, como última alternativa, cualquier tipografía del sistema perteneciente a la familia `sans-serif`.

!!! salto-pagina-pdf ""

## 5.5. Jerarquía tipográfica

La jerarquía tipográfica permite distinguir la importancia y la función de cada texto.

Puede construirse modificando:

- El tamaño.
- El grosor.
- El color.
- El espaciado.
- La posición.
- La familia tipográfica.

En FestWeb podríamos definir la siguiente jerarquía:

```css
.titulo-pagina {
  font-size: 2.25rem;
  font-weight: 700;
}

.titulo-seccion {
  font-size: 1.5rem;
  font-weight: 600;
}

.titulo-evento {
  font-size: 1.25rem;
  font-weight: 600;
}

.texto-contenido {
  font-size: 1rem;
  line-height: 1.6;
}

.texto-auxiliar {
  font-size: 0.875rem;
  line-height: 1.4;
}
```

No es necesario que cada texto tenga un diseño completamente diferente. Una jerarquía eficaz utiliza pocos niveles y mantiene reglas consistentes en toda la interfaz.

!!! salto-pagina-pdf ""

## 5.6. Legibilidad y contraste

El texto debe diferenciarse claramente del fondo sobre el que aparece.

Las pautas WCAG establecen, con carácter general, una relación mínima de contraste de:

- **4,5:1** para texto de tamaño normal.
- **3:1** para texto grande.

No debemos valorar el contraste únicamente por su apariencia. Es necesario comprobarlo mediante una herramienta de análisis.

Dentro de la paleta de FestWeb:

- El texto `#213FC2` sobre fondo blanco presenta un contraste adecuado.
- El texto `#213FC2` sobre el fondo `#C6D8FF` también resulta adecuado.
- El texto blanco sobre `#50C9E9` no alcanza el contraste necesario para texto normal.
- El texto blanco sobre `#3B82E6` tampoco alcanza el valor recomendado para texto normal.

Por tanto, no debemos suponer que un texto blanco siempre funciona correctamente sobre un fondo de color.

```css
.aviso {
  color: var(--color-texto);
  background-color: var(--color-advertencia);
  padding: 1rem;
  border-left: 0.25rem solid var(--color-texto);
}
```

!!! warning "Contraste y función"
    Un color puede formar parte de la identidad visual y, al mismo tiempo, no ser adecuado para todas las combinaciones de texto y fondo.


!!! salto-pagina-pdf ""

## 5.7. Aplicación a una tarjeta de FestWeb

Podemos combinar unidades relativas, colores y propiedades tipográficas para diseñar una tarjeta de evento coherente:

```css
.tarjeta-evento {
  width: 100%;
  max-width: 22rem;
  padding: 1.25rem;
  color: var(--color-texto);
  background-color: #ffffff;
  border: 2px solid var(--color-principal);
  border-radius: 0.75rem;
}

.tarjeta-evento__categoria {
  color: var(--color-secundario);
  font-size: 0.875rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05rem;
}

.tarjeta-evento__titulo {
  margin: 0.5rem 0;
  font-size: 1.25rem;
  line-height: 1.3;
}

.tarjeta-evento__informacion {
  font-size: 1rem;
  line-height: 1.5;
}

.tarjeta-evento__boton {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.75rem 1.25rem;
  color: var(--color-texto);
  background-color: var(--color-principal);
  border-radius: 0.5rem;
  font-weight: 700;
  text-decoration: none;
}
```

Todas las tarjetas podrán utilizar estas mismas reglas, manteniendo una apariencia homogénea.


---

> *Una identidad visual coherente no depende de utilizar muchos estilos, sino de aplicar correctamente un conjunto reducido de decisiones.*

!!! salto-pagina-pdf ""