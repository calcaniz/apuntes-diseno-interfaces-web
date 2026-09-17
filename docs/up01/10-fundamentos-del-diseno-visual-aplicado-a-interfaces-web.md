
En el desarrollo de aplicaciones web es habitual caer en el simplismo de considerar el diseño visual como un elemento meramente ornamental o un añadido estético que se aplica al final del proyecto. En el diseño de interfaces, la composición visual es una herramienta funcional de comunicación técnica y arquitectura cognitiva.

El diseño visual no busca únicamente que una pantalla resulte bonita, sino que sea perceptible, legible, jerarquizada e intuitiva. La posición, el tamaño, el contraste y la distribución del espacio condicionan la velocidad con la que la persona usuaria procesa la información y la precisión con la que ejecuta las acciones.

### 10.1. El diseño visual como medio de comunicación

Desde una perspectiva técnica, el diseño visual funciona como el lenguaje no verbal de la interfaz. Su misión es convertir las prioridades de negocio y la funcionalidad del sistema en estímulos visuales que el cerebro humano pueda interpretar automáticamente, reduciendo la carga cognitiva.

Para entender su papel debemos analizar tres dimensiones:

1. **Estética:** es el aspecto formal, el acabado gráfico, la armonía cromática y el tono del producto. Genera la primera impresión, transmite profesionalidad y apela a la dimensión emocional.
2. **Funcionalidad:** garantiza que la interfaz cumpla las tareas para las que ha sido programada. Se centra en el funcionamiento de los botones, la integridad de los datos en los formularios y la lógica de navegación.
3. **Comunicación visual:** conecta las dos dimensiones anteriores. Utiliza principios de percepción para dirigir la vista hacia las acciones críticas, estructurar el contenido sin necesidad de añadir texto y confirmar el estado de las transacciones.

!!! salto-pagina-pdf ""

### 10.2. Composición y principios de distribución en pantalla

La composición es la ordenación intencionada de los elementos dentro de la interfaz. Una composición sólida se apoya en cuatro principios:

1. **Equilibrio simétrico y asimétrico:** se refiere a la distribución del peso visual de los componentes.
    - **Simétrico:** los elementos se distribuyen de forma equivalente a ambos lados de un eje central. Transmite formalidad, estabilidad y orden, aunque puede resultar monótono.
    - **Asimétrico:** los elementos presentan pesos diferentes, pero se compensan mediante el uso estratégico del color, el tamaño o el espacio en blanco.
2. **Alineación y creación de ejes visuales:** la alineación crea conexiones invisibles entre elementos distantes y establece orden y estructura. Los elementos alineados en un mismo eje se perciben como parte de un bloque funcional. La falta de alineación genera desorden y obliga al ojo a realizar desplazamientos erráticos.
3. **Proximidad y agrupación:** los elementos que están físicamente cerca se perciben como pertenecientes al mismo grupo o categoría funcional. Por ejemplo, la etiqueta de un formulario (`<label>`) debe estar visualmente más cerca de su campo (`<input>`) que del campo anterior o posterior.
4. **Repetición y consistencia:** repetir patrones de diseño ayuda a la persona usuaria a aprender el funcionamiento de la aplicación tras la primera interacción.

### 10.3. La jerarquía visual

La jerarquía visual permite controlar la prevalencia de los componentes para que la persona usuaria lea e interprete el contenido en el orden de importancia previsto. Para establecer niveles de jerarquía sin saturar la pantalla se utilizan cuatro mecanismos:

- **Tamaño y escala:** los elementos de mayor dimensión atraen la atención en primer lugar. Por ejemplo, los títulos principales (`<h1>`) deben tener mayor tamaño que los subtítulos (`<h2>`).
- **Peso visual y contraste:** los elementos más oscuros, con fuentes en negrita o colores saturados, pesan más que los claros o finos. Los CTA pueden utilizar un color sólido de alto contraste y los botones secundarios únicamente un borde.
- **Posición en pantalla:** en nuestro contexto de lectura, la vista suele desplazarse de arriba abajo y de izquierda a derecha. El logotipo y la identificación suelen situarse en la esquina superior izquierda.
- **Aislamiento y espacio:** un elemento rodeado de espacio en blanco gana peso visual, aunque sea de tamaño reducido.

!!! salto-pagina-pdf ""

### 10.4. El espacio en blanco

El espacio en blanco o *negative space* no es espacio vacío o desaprovechado; es uno de los recursos activos más potentes del diseño de interfaces. Se define como la distancia que separa componentes, bloques de contenido, márgenes y líneas de texto.

Su uso correcto reduce la saturación visual, define las relaciones funcionales y aumenta la legibilidad, por ejemplo mediante el interlineado y los márgenes entre párrafos.

### 10.5. Errores frecuentes en la composición web

| Error habitual { .table-bg-principal .table-cl-secundario } | Causa { .table-bg-principal .table-cl-secundario } | Consecuencia { .table-bg-principal .table-cl-secundario } | Solución { .table-bg-principal .table-cl-secundario } |
|---|---|---|---|
| Falta de jerarquía | Todos los textos y botones tienen un tamaño, color o peso similar | La persona usuaria no sabe dónde mirar primero ni cuál es la acción principal | Aplicar una distribución cromática coherente y escalar los tamaños tipográficos mediante un factor multiplicador claro |
| Saturación visual | Ausencia de espacio en blanco y densidad excesiva de información y banners | Sobrecarga cognitiva y abandono prematuro de la página | Eliminar elementos superfluos e incrementar los márgenes y el `padding` de los contenedores |
| Alineaciones inconsistentes | Elementos desalineados respecto a la rejilla base | Sensación de falta de profesionalidad y dificultad para seguir los ejes de lectura | Utilizar un sistema de rejilla consistente |
| Uso inadecuado del contraste | Texto gris sobre fondo gris claro o botones primarios con baja saturación | Incumplimiento de las pautas de accesibilidad y problemas de legibilidad | Garantizar una relación de contraste mínima de 4,5:1 para el texto normal |

!!! salto-pagina-pdf ""