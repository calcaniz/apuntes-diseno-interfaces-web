
El color y la tipografía constituyen los dos pilares fundamentales del sistema visual. Lejos de ser decisiones basadas en gustos subjetivos, la selección cromática y tipográfica responde a criterios de usabilidad, legibilidad, accesibilidad y psicología cognitiva.

Un uso deficiente del color o de la tipografía destruye la jerarquía visual, incrementa la tasa de rebote y puede inhabilitar la aplicación para personas con diversidad funcional. Por el contrario, un sistema cromático estructurado y una escala tipográfica coherente permiten transformar un diseño estático en un producto interactivo claro, profesional y funcional.

### 11.1. El color

El color en una interfaz no es un elemento decorativo: comunica estados, prioriza elementos y transmite la identidad de marca. Para trabajar con él es necesario comprender tres propiedades:

- **Tono (*hue*):** define la familia del color —rojo, azul o verde— según su posición en el círculo cromático. En modelos como HSL se mide en grados de 0° a 360°.
- **Saturación (*saturation*):** mide la intensidad o pureza del color, desde el color puro —100 %— hasta una escala de grises desaturada —0 %—.
- **Luminosidad (*lightness*):** indica la cantidad de luz que refleja el color, desde el negro absoluto —0 %— hasta el blanco puro —100 %—.

En el desarrollo web moderno puede resultar conveniente utilizar modelos como HSL u OKLCH, ya que facilitan la creación programática de variantes claras y oscuras ajustando parámetros de luminosidad o saturación.

### 11.2. Armonías y construcción de la paleta cromática

Para construir una paleta cromática profesional podemos apoyarnos en diferentes armonías:

- **Monocromática:** utiliza variaciones de luminosidad y saturación de un único tono. Aporta orden, pero requiere cuidado para no perder contraste.
- **Análoga:** utiliza colores contiguos del círculo cromático, como azul, azul violáceo y violeta. Produce composiciones armoniosas y de bajo impacto visual.
- **Complementaria:** utiliza tonos opuestos en el círculo cromático, como azul y naranja. Genera un gran contraste visual y resulta adecuada para CTA y botones primarios.
- **Triádica:** utiliza tres tonos equidistantes en el círculo cromático. Ofrece contraste manteniendo el equilibrio si se emplea un tono dominante y dos de acento.

!!! salto-pagina-pdf ""

### 11.3. Clasificación funcional de los colores

En una interfaz, cada color debe tener un rol funcional dentro del sistema de diseño:

1. **Color principal:** representa la identidad de la marca y ocupa aproximadamente el 60 % del uso cromático. Se aplica en elementos destacados como la navegación, las cabeceras o los botones primarios.
2. **Color secundario:** complementa al principal y puede ocupar alrededor del 30 % del uso. Se utiliza en elementos de apoyo, filtros secundarios o divisores.
3. **Colores neutros:** constituyen la base estructural de la pantalla: fondos, tarjetas, bordes y textos. Una paleta neutra puede utilizar grises con un ligero matiz del color principal para lograr cohesión.
4. **Color de acento:** color de alto contraste reservado para llamadas a la acción prioritarias, estados activos y notificaciones. Puede representar aproximadamente el 10 % del uso.
5. **Colores funcionales o semánticos:** colores utilizados para comunicar estados del sistema sin necesidad de lectura, como éxito, peligro, advertencia o información.

### 11.4. Contraste cromático y accesibilidad

El contraste inadecuado es uno de los errores de usabilidad más graves. Las WCAG establecen relaciones mínimas de contraste de luminancia entre el texto o los componentes y su fondo.

| Nivel { .table-bg-principal .table-cl-secundario } | Texto normal { .table-bg-principal .table-cl-secundario } | Texto grande { .table-bg-principal .table-cl-secundario } | Componentes { .table-bg-principal .table-cl-secundario } |
|---|:---:|:---:|:---:|
| Mínimo | 4,5:1 | 3:1 | 3:1 |
| Reforzado | 7:1 | 4,5:1 | 4,5:1 |

!!! salto-pagina-pdf ""

### 11.5. Tipografías

La tipografía es la herramienta principal para transmitir información en la Web. A diferencia del papel, las pantallas imponen restricciones de resolución, renderizado por píxeles y diversidad de dispositivos. Las principales familias tipográficas son:

- **Sans serif:** carecen de remates en los extremos. Son habituales en interfaces digitales y cuerpos de texto por su legibilidad en pantallas.
- **Serif:** presentan pequeños remates ornamentales. Se asocian con la tradición, la elegancia y la prensa. Pueden utilizarse en títulos de gran tamaño o sitios de contenido editorial.
- **Monoespaciadas:** todos los caracteres ocupan el mismo ancho. Son adecuadas para mostrar código fuente, datos numéricos alineados o tablas técnicas.
- **Display o decorativas:** poseen una fuerte personalidad. Deben reservarse para títulos de impacto o logotipos y evitarse en textos continuos y botones.

Para estructurar el contenido, la tipografía utiliza una escala modular donde cada nivel jerárquico tiene asignadas propiedades específicas de tamaño, peso, altura de línea y espaciado entre letras.

| Jerarquía { .table-bg-principal .table-cl-secundario } | HTML { .table-bg-principal .table-cl-secundario } | Tamaño recomendado { .table-bg-principal .table-cl-secundario } | Peso { .table-bg-principal .table-cl-secundario } | Altura de línea { .table-bg-principal .table-cl-secundario } |
|---|:---:|---|---|:---:|
| Título principal | `h1` | 2,25–3 rem (36–48 px) | Bold (700–800) | 1,1–1,2 |
| Subtítulo | `h2` | 1,5–2 rem (24–32 px) | Semibold (600) | 1,2–1,3 |
| Encabezado de tarjeta | `h3` | 1,25–1,5 rem (20–24 px) | Medium (500) | 1,3–1,4 |
| Cuerpo de texto | `p` | 1 rem (16 px) | Regular (400) | 1,5–1,6 |
| Texto secundario | `small` | 0,875 rem (14 px) | Regular (400) | 1,4–1,5 |
| Botones y etiquetas | `button` / `label` | 0,875–1 rem (14–16 px) | Medium / Semibold | 1–1,2 |

Existen dos reglas básicas en la tipografía web:

1. **Regla de las dos familias:** no utilizar más de dos familias tipográficas distintas en un mismo proyecto.
2. **Ajuste de la altura de línea:** el cuerpo del texto debe tener un interlineado aproximado del 150–160 % —por ejemplo, `line-height: 1.5`— para facilitar el salto de línea durante la lectura.

!!! salto-pagina-pdf ""