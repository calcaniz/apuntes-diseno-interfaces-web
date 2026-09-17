
La falta de normalización en la interfaz genera una sensación de falta de coherencia técnica: botones con distintos radios de curvatura, fuentes desproporcionadas, discrepancias cromáticas y duplicación de código CSS. Para evitarlo, el diseño de interfaces se apoya en tres instrumentos esenciales: la guía de estilo, las plantillas de diseño y los componentes.

### 13.1. Guía de estilo

Una **guía de estilo (*style guide*)** es la documentación que recoge y estandariza las reglas visuales e interactivas de una aplicación web. Su propósito trasciende la mera presentación de colores y fuentes: actúa como un contrato de interfaz que garantiza:

- **Consistencia sistemática:** todos los integrantes de los equipos de diseño y desarrollo aplican el mismo criterio.
- **Mantenibilidad y escalabilidad:** una modificación puede propagarse de manera uniforme por toda la aplicación.
- **Eficiencia en el *handoff*:** reduce la ambigüedad y las consultas durante la traducción del prototipo a HTML, CSS y componentes JavaScript.

Una guía de estilo completa para una aplicación web moderna debe estructurarse en bloques técnicos:

- **Tokens de diseño:** valores atómicos reutilizables en CSS que almacenan decisiones visuales.
    - **Colores:** variables para los colores principal, secundario, de acento, de fondo y de texto. Por ejemplo: `--color-primary: #005659`.
    - **Espaciado y rejilla:** adopción de un sistema basado, por ejemplo, en múltiplos de 8 px: 4, 8, 16, 24, 32 y 48 px. Las separaciones, márgenes y rellenos se ajustan al sistema para mantener la armonía de la composición.
    - **Sombras y elevación:** niveles de profundidad mediante `box-shadow`, como `--shadow-sm` y `--shadow-md`, que expresan la superposición de tarjetas o ventanas modales.
- **Iconografía y gráficos:** estandarización de conjuntos de iconos para que compartan grosor de trazo, tamaño de la caja delimitadora y estilo visual.

Un error habitual consiste en documentar únicamente la apariencia de un elemento. Un componente de interfaz también debe reaccionar visualmente a las acciones del usuario y a los cambios del sistema.

!!! ejemplo "Componente: botón"
    **Variantes funcionales**

    - **Primary:** acción principal, como comprar una entrada.
    - **Secondary:** acciones secundarias, como ver más o filtrar.
    - **Danger:** acciones destructivas, como cancelar una reserva.

    **Estados de interacción**

    - **Reposo (*default*):** estado base en espera de interacción.
    - **Hover:** el puntero pasa sobre el botón.
    - **Foco (*focus*):** el botón queda seleccionado mediante el teclado y muestra un indicador accesible.
    - **Activo (*active*):** momento exacto de la pulsación o clic.
    - **Desactivado (*disabled*):** la acción no está disponible.
    - **Carga (*loading*):** muestra un indicador de proceso asíncrono.

Para evitar interpretaciones ambiguas durante el desarrollo, la guía de estilo debe incorporar normas explícitas:

- **Sí (*do*):** utilizar un único botón principal por bloque visual o formulario para mantener una jerarquía clara.
- **No (*don't*):** alterar arbitrariamente el color del texto del botón y crear combinaciones que incumplan el contraste WCAG AA.

### 13.2. Plantillas de diseño: estructuras y zonas variables

Una plantilla de diseño es una estructura de maquetación reutilizable que define la distribución espacial de los elementos comunes en un grupo de páginas con el mismo propósito funcional. Las plantillas articulan la pantalla separando los componentes estructurales de las zonas de contenido dinámico.

En FestWeb podemos utilizar, por ejemplo:

1. **Plantilla de portada:** enfocada al descubrimiento de eventos. Incorpora un bloque *hero* de gran impacto visual, secciones horizontales de eventos y banners de categorías.
2. **Plantilla de listado o catálogo:** enfocada a la búsqueda activa. Utiliza una disposición asimétrica con una barra lateral de filtros (`<aside>`) y una cuadrícula adaptable de tarjetas de eventos.
3. **Plantilla de detalle de evento:** enfocada a la conversión. Prioriza los datos operativos, la galería visual y la llamada a la acción.

El diseño visual modular mediante guías de estilo y plantillas se corresponde directamente con el paradigma de desarrollo orientado a componentes, como el que ofrece Vue mediante archivos SFC (*Single-File Components*) con extensión `.vue`.