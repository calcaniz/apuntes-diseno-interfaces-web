---
title: Inspección y validación del CSS
---

# 8. Inspección y validación del CSS

Durante el desarrollo de una interfaz es habitual encontrar estilos que no se aplican, propiedades sobrescritas o elementos que ocupan más espacio del esperado.

Las herramientas de desarrollo del navegador permiten inspeccionar la página, localizar el origen del problema y probar posibles soluciones antes de modificar los archivos.

> **Pregunta de partida:**  
> Si una regla CSS está correctamente escrita, ¿por qué puede no aparecer en la página?

## 8.1. Herramientas de desarrollo del navegador

Los navegadores actuales incorporan herramientas para analizar el HTML, el CSS y el funcionamiento de una página.

Podemos abrirlas mediante:

- La opción **Inspeccionar** del menú contextual.
- La tecla `F12`.
- La combinación `Ctrl + Mayús + I`.

Los nombres pueden variar ligeramente según el navegador, pero normalmente encontraremos:

| Panel { .table-full-container .table-cl-secundario .table-bg-principal } | Utilidad { .table-cl-secundario .table-bg-principal } |
|---|---|
| Elementos o Inspector | Examinar el HTML y las reglas CSS |
| Estilos | Consultar y modificar las declaraciones aplicadas |
| Calculado | Comprobar el valor final de cada propiedad |
| Modelo de caja | Analizar contenido, relleno, borde y margen |
| Consola | Consultar errores y mensajes |
| Red | Revisar la carga de archivos y recursos |

## 8.2. Inspeccionar un elemento

Para analizar un componente de FestWeb:

1. Pulsa con el botón derecho sobre el elemento.
2. Selecciona **Inspeccionar**.
3. Comprueba la etiqueta HTML seleccionada.
4. Revisa las reglas CSS que se aplican.
5. Observa si alguna declaración aparece tachada.
6. Consulta los estilos calculados y el modelo de caja.

Una declaración tachada indica normalmente que otra regla tiene prioridad:

```css
.boton {
  background-color: #50c9e9;
}

nav a {
  background-color: #3b82e6;
}
```

Si un enlace utiliza la clase `.boton` y se encuentra dentro de `nav`, ambas reglas compiten. El inspector permite identificar cuál ha resultado ganadora y desde qué archivo procede.

## 8.3. Probar cambios desde el navegador

El panel de estilos permite modificar temporalmente las propiedades:

```css
.tarjeta-evento {
  padding: 1.5rem;
  border: 2px solid #50c9e9;
}
```

Desde el inspector podemos:

- Activar o desactivar declaraciones.
- Cambiar valores.
- Añadir propiedades.
- Probar colores.
- Examinar pseudoclases como `:hover`.
- Comprobar diferentes tamaños de pantalla.

!!! warning "Cambios temporales"
    Las modificaciones realizadas desde las herramientas del navegador desaparecen al actualizar la página. Cuando encontremos la solución, debemos copiarla al archivo CSS correspondiente.

## 8.4. Estilos calculados

Un elemento puede recibir estilos desde diferentes reglas, mediante herencia o a través de los valores predeterminados del navegador.

El panel de estilos calculados muestra el resultado final:

```css
color: rgb(33, 63, 194);
font-size: 16px;
padding: 20px;
```

Este panel resulta útil cuando:

- No sabemos de dónde procede una propiedad.
- Una regla ha sido sobrescrita.
- Una medida relativa se ha transformado en píxeles.
- Un elemento hereda un estilo no esperado.
- El navegador aplica un estilo predeterminado.

Por ejemplo, aunque escribamos:

```css
.tarjeta-evento {
  padding: 1.25rem;
}
```

El valor calculado podría mostrarse como `20px` si el tamaño raíz es de `16px`.

## 8.5. Análisis del modelo de caja

Las herramientas del navegador representan gráficamente:

- El contenido.
- El `padding`.
- El `border`.
- El `margin`.
- Las dimensiones finales del elemento.

Si una tarjeta ocupa más espacio del esperado, debemos comprobar:

```css
.tarjeta-evento {
  width: 300px;
  padding: 20px;
  border: 2px solid #50c9e9;
}
```

También conviene revisar si se ha aplicado:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

El inspector permite modificar cada medida y observar inmediatamente cómo afecta a la distribución de la página.

## 8.6. Errores frecuentes

### El archivo CSS no se carga

Debemos comprobar que la ruta indicada en el HTML sea correcta:

```html
<link rel="stylesheet" href="css/estilos.css">
```

En el panel de red o en la consola puede aparecer un error si el archivo no se encuentra.

### El selector no coincide

```html
<article class="tarjeta-evento">
```

```css
.tarjeta_eventos {
  border: 2px solid #50c9e9;
}
```

Los nombres no coinciden: el HTML utiliza `tarjeta-evento` y el CSS `tarjeta_eventos`.

### Falta un signo de puntuación

```css
.tarjeta-evento {
  color: #213fc2
  background-color: #ffffff;
}
```

Falta el punto y coma después de `color`. Esto puede provocar que el navegador ignore parte de la regla.

### Una propiedad está sobrescrita

```css
.boton {
  color: #213fc2;
}

a {
  color: #3b82e6;
}
```

Debemos consultar el inspector para comprobar qué regla tiene prioridad y evitar aumentar innecesariamente la especificidad.

### Se utiliza una propiedad no válida

```css
.tarjeta-evento {
  text-color: #213fc2;
}
```

La propiedad correcta es `color`:

```css
.tarjeta-evento {
  color: #213fc2;
}
```

### El valor no incluye una unidad

```css
.tarjeta-evento {
  padding: 20;
}
```

Salvo cuando el valor es `0`, las medidas normalmente necesitan una unidad:

```css
.tarjeta-evento {
  padding: 20px;
}
```

## 8.7. Validación del CSS

La validación comprueba si el código respeta la sintaxis y las especificaciones de CSS.

Podemos utilizar el **servicio de validación CSS del W3C** introduciendo:

- La dirección de una página publicada.
- El contenido del archivo CSS.
- El archivo CSS directamente.

El validador puede mostrar:

- **Errores:** declaraciones o construcciones que no cumplen la sintaxis.
- **Advertencias:** situaciones que conviene revisar, pero que no siempre impiden el funcionamiento.

Por ejemplo:

```css
.boton {
  background-colour: #50c9e9;
}
```

El validador detectará que `background-colour` no es una propiedad CSS válida. La declaración correcta es:

```css
.boton {
  background-color: #50c9e9;
}
```

!!! note "Validar no significa diseñar bien"
    Un archivo puede superar la validación y, aun así, presentar problemas de legibilidad, contraste, organización o coherencia visual.

## 8.8. Proceso de depuración

Cuando un estilo no funciona, podemos seguir este procedimiento:

1. Seleccionar el elemento con el inspector.
2. Comprobar que la clase aparece en el HTML.
3. Verificar que el archivo CSS se ha cargado.
4. Localizar la regla en el panel de estilos.
5. Revisar si la declaración está tachada o contiene un error.
6. Consultar el valor calculado.
7. Probar una corrección desde el navegador.
8. Aplicar la solución en el archivo CSS.
9. Validar nuevamente el código.
10. Actualizar la página y comprobar el resultado.

Es preferible identificar la causa del problema antes de añadir selectores más específicos o utilizar `!important`.

!!! salto-pagina-pdf ""

## 8.9. Revisión de FestWeb

Antes de considerar terminada una página de FestWeb, debemos comprobar:

- Que todos los archivos CSS se cargan correctamente.
- Que no aparecen errores en la consola.
- Que los selectores coinciden con el HTML.
- Que no existen declaraciones anuladas sin una razón clara.
- Que las dimensiones y los espaciados son coherentes.
- Que los componentes reutilizan las clases previstas.
- Que el foco de teclado es visible.
- Que el código CSS supera la validación.
- Que la página mantiene su legibilidad en diferentes tamaños de pantalla.
---

> *Inspeccionar y validar el código no es una tarea final: forma parte del proceso habitual de desarrollo.*