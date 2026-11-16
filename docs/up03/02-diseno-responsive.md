---
title: Fundamentos del diseño responsive
---

# 1. Fundamentos del diseño responsive

El **diseño web responsive**, también denominado *Responsive Web Design* o RWD, es un enfoque que permite adaptar la distribución y presentación de una interfaz al espacio disponible en la ventana del navegador. Su objetivo es que los contenidos mantengan su legibilidad, jerarquía y facilidad de interacción en teléfonos móviles, tabletas, portátiles y pantallas de escritorio.

!!! info "Idea clave"

    Una interfaz responsive no se limita a reducir el tamaño de sus elementos. También modifica su distribución para aprovechar el espacio disponible y conservar la facilidad de uso.

## 1.1. Evolución de la maquetación web

Las interfaces web pueden responder de diferentes maneras al tamaño de la pantalla:

| Modelo { .table-full-container .table-cl-secundario .table-bg-principal } | Comportamiento { .table-cl-secundario .table-bg-principal } | Principal limitación { .table-cl-secundario .table-bg-principal } |
|---|---|---|
| **Fijo** | Utiliza dimensiones establecidas principalmente en píxeles. | Puede provocar desplazamiento horizontal en pantallas pequeñas. |
| **Fluido** | Utiliza porcentajes y unidades relativas para ocupar el espacio disponible. | Puede generar elementos demasiado anchos o estrechos en tamaños extremos. |
| **Adaptable** | Selecciona una composición predeterminada para determinados intervalos. | Puede producir cambios bruscos entre las distintas composiciones. |
| **Responsive** | Combina composiciones flexibles, recursos adaptables y media queries. | Requiere planificar y comprobar el comportamiento de los componentes. |


## 1.2. Problemas de una interfaz rígida

Una interfaz diseñada únicamente para escritorio puede presentar:

- Desplazamiento horizontal.
- Textos o botones fuera de sus contenedores.
- Imágenes más anchas que la pantalla.
- Navegaciones cuyos enlaces se amontonan.
- Columnas demasiado estrechas.
- Áreas de interacción difíciles de utilizar.
- Grandes espacios vacíos en pantallas anchas.

### Ejemplo de interfaz rígida

```css
.contenedor {
    width: 1200px;
}

.listado-eventos {
    display: grid;
    grid-template-columns: repeat(3, 380px);
    gap: 30px;
}
```

Esta composición necesita más de 1200 píxeles de anchura. Si se abre en una pantalla móvil de 390 píxeles, el contenido no cabe y aparece una barra de desplazamiento horizontal.

!!! warning "No ocultes el problema"

    Utilizar `overflow-x: hidden` sobre toda la página puede ocultar la barra de desplazamiento, pero no corrige el elemento que está provocando el desbordamiento.


!!! salto-pagina-pdf ""

## 1.3. El viewport

El **viewport** es la zona del navegador en la que se visualiza el documento web.

Para que los navegadores móviles utilicen el ancho real del dispositivo, debemos incluir esta etiqueta dentro de `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Sus valores indican:

- `width=device-width`: utiliza el ancho disponible en el dispositivo.
- `initial-scale=1`: establece la escala inicial de visualización.

### Documento HTML básico

```html
<!doctype html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>FestWeb</title>
</head>
<body>
    <h1>Próximos eventos</h1>
</body>
</html>
```

Sin una configuración correcta del viewport, las reglas responsive pueden no comportarse como esperamos en dispositivos móviles.

## 1.4. Principios del diseño responsive

Una interfaz responsive combina normalmente cuatro elementos:

1. **Composiciones flexibles:** los contenedores y componentes se adaptan al espacio disponible.
2. **Recursos adaptables:** las imágenes y vídeos no superan la anchura de sus contenedores.
3. **Puntos de ruptura:** la distribución cambia cuando el contenido deja de mostrarse correctamente.
4. **Comprobación continua:** la interfaz se revisa en distintos tamaños y orientaciones.

!!! example "Aplicación en FestWeb"

    En una pantalla móvil, las tarjetas de eventos podrán mostrarse en una sola columna. Cuando aumente el espacio disponible, podrán reorganizarse en dos o tres columnas sin modificar el contenido HTML.

## 1.5. Diseñar a partir del contenido

Los cambios de composición no deben depender exclusivamente de las dimensiones de modelos comerciales de teléfonos o tabletas.

Debe introducirse un punto de ruptura cuando:

- El contenido deja de caber.
- Los textos pierden legibilidad.
- Los controles quedan demasiado juntos.
- La navegación deja de funcionar correctamente.
- Aparecen espacios vacíos desproporcionados.

Por tanto, el contenido es el que determina cuándo debe cambiar la interfaz.

## 1.6. Comprobación

Observa el siguiente estilo:

```css
.tarjeta-evento {
    width: 500px;
}
```

Responde:

1. ¿Qué ocurrirá si el contenedor dispone únicamente de 360 píxeles?
2. ¿Qué problema podría aparecer en la página?
3. ¿Sería suficiente ocultar el desbordamiento?
4. ¿Qué tipo de dimensión resultaría más adecuada?

En el siguiente apartado veremos cómo utilizar unidades relativas, límites de anchura y recursos adaptables para resolver este tipo de problemas.


!!! salto-pagina-pdf ""