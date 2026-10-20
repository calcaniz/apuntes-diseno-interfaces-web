---
title: A02.03. Sistema de estilos y control de calidad (Simplificada)
---

# A02.03. Sistema de estilos y control de calidad (Simplificada)

## 1. Objetivo

En esta actividad utilizaremos las herramientas de desarrollo del navegador para localizar y corregir problemas relacionados con la aplicación de estilos CSS.

Al finalizar la sesión serás capaz de:

- Comprobar si una hoja de estilos se ha cargado correctamente.
- Identificar por qué un selector no se aplica.
- Interpretar declaraciones sobrescritas o desactivadas.
- Consultar el valor final calculado de una propiedad.
- Examinar el modelo de caja de un elemento.
- Detectar errores de sintaxis.
- Validar una hoja de estilos CSS.

## 2. Punto de partida

Continuaremos trabajando sobre el proyecto de la actividad A02.02.

Necesitarás:

- El documento `componentes.html`.
- La hoja de estilos `styles.css`.
- Un navegador con herramientas de desarrollo.
- Un archivo denominado `control-calidad.md`.

Antes de comenzar, abre `componentes.html` en el navegador y comprueba que los botones, etiquetas y tarjetas se muestran correctamente.

> Durante la sesión introduciremos algunos errores de manera intencionada. Todos deberán quedar corregidos antes de finalizar.

## 3. Preparación del registro

Crea el archivo `control-calidad.md` en la carpeta principal del proyecto e incorpora la siguiente tabla:

```markdown
# Control de calidad CSS

| Comprobación | Problema observado | Solución aplicada |
|---|---|---|
| Carga de la hoja de estilos | | |
| Selector no coincidente | | |
| Declaración sobrescrita | | |
| Modelo de caja | | |
| Error de sintaxis | | |
| Validación final | | |
```

Completarás la tabla a medida que realicemos las comprobaciones.

## 4. Desarrollo guiado

### 4.1. Comprobar la carga de la hoja de estilos

1. Abre las herramientas de desarrollo del navegador.
2. Selecciona la pestaña **Elementos** o **Inspector**.
3. Localiza dentro de `<head>` el elemento `<link>` que conecta el documento con `styles.css`.
4. Modifica temporalmente una letra del nombre o de la ruta del archivo.
5. Actualiza la página y observa qué ocurre.
6. Consulta la pestaña **Red** para comprobar que el navegador no encuentra el archivo.
7. Restaura la ruta correcta y actualiza nuevamente.

Anota en `control-calidad.md`:

- Cómo se manifestaba el problema.
- En qué herramienta lo has detectado.
- Cómo lo has corregido.

### 4.2. Localizar un selector que no coincide

Selecciona en `styles.css` una regla correspondiente a un botón, una etiqueta o una tarjeta.

Modifica temporalmente el nombre de la clase en el selector. Por ejemplo:

```css
.boton--principal {
    background-color: var(--color-principal);
}
```

puede convertirse provisionalmente en:

```css
.boton-principal {
    background-color: var(--color-principal);
}
```

Actualiza la página e inspecciona el elemento afectado.

Comprueba:

- Qué clases aparecen en el atributo `class` del elemento HTML.
- Qué reglas CSS se muestran en el inspector.
- Por qué el nuevo selector no encuentra el elemento.

Corrige el selector y registra la solución.

### 4.3. Interpretar una declaración sobrescrita

Añade temporalmente al final de `styles.css` una nueva regla que modifique una propiedad ya definida:

```css
.boton--principal {
    background-color: grey;
}
```

Inspecciona el botón principal y localiza:

- La declaración que se aplica.
- La declaración que aparece tachada.
- El archivo y la línea donde está definida cada regla.
- El valor final mostrado en la sección de estilos calculados.

Elimina después la regla temporal y explica en `control-calidad.md` por qué una declaración había sustituido a la otra.

### 4.4. Examinar el modelo de caja

Selecciona una tarjeta de evento y abre la sección **Calculado**, **Diseño** o **Modelo de caja** del inspector.

Identifica los valores correspondientes a:

- Contenido.
- Relleno interior.
- Borde.
- Margen.

Modifica temporalmente el `padding` desde el inspector y observa cómo cambia la tarjeta.

> Los cambios realizados directamente desde las herramientas de desarrollo desaparecen al actualizar la página. Para conservarlos deben incorporarse a `styles.css`.

Anota qué propiedad has modificado y qué efecto ha producido.

### 4.5. Detectar un error de sintaxis

Introduce temporalmente el siguiente error en una de las reglas:

```css
.tarjeta-evento {
    border-radius 12px;
}
```

Actualiza la página e inspecciona la regla.

1. Localiza la declaración que el navegador no puede interpretar.
2. Identifica el carácter que falta.
3. Corrige la declaración:

```css
.tarjeta-evento {
    border-radius: 12px;
}
```

Registra el problema y su solución en el documento de control de calidad.

### 4.6. Validar la hoja de estilos

Utiliza el validador CSS indicado por el docente para comprobar `styles.css`.

1. Copia el contenido de la hoja de estilos.
2. Ejecuta la validación.
3. Revisa los errores y advertencias encontrados.
4. Corrige los errores de sintaxis.
5. Repite la validación.

El resultado final no deberá contener errores CSS. Las advertencias deberán revisarse, aunque no siempre implican que el código sea incorrecto.

## 5. Reto final

El docente introducirá uno de estos problemas en el proyecto:

- Una ruta incorrecta hacia la hoja de estilos.
- Una clase HTML que no coincide con su selector.
- Una propiedad CSS escrita incorrectamente.
- Una declaración sustituida por otra regla.

Utiliza las herramientas de desarrollo para:

1. Localizar el elemento afectado.
2. Identificar la causa.
3. Corregir el problema.
4. Explicar qué información del inspector te ha permitido encontrarlo.

## 6. Comprobación final

Antes de terminar, comprueba que:

- `componentes.html` carga correctamente `styles.css`.
- Los botones, etiquetas y tarjetas conservan su apariencia.
- No quedan reglas de prueba añadidas durante la actividad.
- Las clases HTML coinciden con los selectores CSS.
- La hoja de estilos no contiene errores de sintaxis.
- `control-calidad.md` contiene todas las comprobaciones realizadas.

## 7. Errores frecuentes

- Modificar el HTML cuando el problema se encuentra en CSS.
- Confundir una clase con un identificador.
- No actualizar la página después de guardar los cambios.
- Pensar que una declaración tachada contiene un error.
- Realizar una corrección únicamente en el inspector.
- Utilizar `!important` sin investigar primero el origen del conflicto.
- Ignorar los mensajes proporcionados por el validador.
