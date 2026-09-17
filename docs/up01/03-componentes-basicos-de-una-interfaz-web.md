
Cuando un usuario accede a una aplicación o sitio web por primera vez, no lee la pantalla palabra por palabra como si fuese un libro, sino que realiza un escaneo visual. Este comportamiento resulta eficiente gracias a la existencia de convenciones de diseño y modelos mentales preexistentes. Las interfaces web se organizan mediante zonas anatómicas relativamente estables y componentes reconocibles.

### 3.1. Anatomía y estructura habitual

La distribución del espacio en una pantalla responde a una jerarquía estructural que ha evolucionado junto con los estándares de la industria y la semántica de HTML5. Una interfaz web estándar se fragmenta en regiones delimitadas, cada una con un rol funcional:

- **Cabecera (*header*):** ubicada normalmente en la parte superior. Su función es la identificación inequívoca. Alberga la identidad corporativa, el acceso a la cuenta del usuario, el carrito de compra en comercios electrónicos y el motor de búsqueda global.
- **Zona de navegación (*navigation*):** es el mapa vial de la aplicación. Puede estar integrada en la cabecera o situada inmediatamente debajo o en un lateral. Reúne los accesos directos a las categorías o secciones principales del sitio.
- **Zona de contenido (*main content*):** es el núcleo de la interfaz y el motivo principal por el que el usuario ha accedido a esa URL. Es una zona dinámica que cambia al navegar por las distintas secciones, mostrando artículos, catálogos de productos, paneles de analítica, etc.
- **Zona de interacción (*interaction area*):** región destinada explícitamente a que el usuario opere sobre el sistema. Puede materializarse en forma de paneles laterales, ventanas modales o secciones incrustadas dentro del contenido. En ella se ubican las herramientas activas de la aplicación.
- **Pie de página (*footer*):** situado en la base de la interfaz. Funciona como cierre estructural y agrupa información secundaria o legal.

### 3.2. Delimitación de roles: navegación, contenido e interacción

Un error habitual entre los programadores con poca experiencia consiste en mezclar las responsabilidades funcionales de las zonas de la pantalla. Para diseñar correctamente, debemos diferenciar la naturaleza de cada una:

- **¿Hacia dónde voy? Navegación:** tiene una naturaleza estática y estructural. Su propósito es cambiar el contexto de la aplicación y modificar el árbol de enrutamiento.
- **¿Qué estoy consumiendo? Contenido:** tiene una naturaleza informativa y perceptiva. Presenta los datos para que el usuario los procese mediante la lectura, la visualización o la escucha.
- **¿Qué estoy haciendo? Interacción:** tiene una naturaleza transaccional y dinámica. Modifica el estado de la aplicación. Implica que el usuario introduce datos, toma decisiones o altera los registros del sistema.


!!! salto-pagina-pdf ""

### 3.3. Componentes habituales de la interfaz

Dentro de cada una de estas zonas disponemos de elementos básicos para construir la interfaz de usuario:

- **Menús:** estructuras jerárquicas que agrupan enlaces de navegación.
- **Botones:** elementos interactivos que desencadenan una acción inmediata en el sistema.
- **Llamadas a la acción (CTA):** botones o enlaces que destacan visualmente porque representan la acción de negocio más importante de la pantalla, como «Comprar» o «Registrarse».
- **Formularios:** conjuntos de campos de entrada destinados a capturar información del usuario de forma estructurada.
- **Buscador:** campo de entrada especializado y conectado a un motor de búsqueda interno para localizar contenidos rápidamente.
- **Tarjetas:** contenedores visuales compactos que agrupan información cohesionada sobre un único elemento.
- **Banners:** espacios informativos destacados, habitualmente gráficos, diseñados para dirigir la atención hacia una campaña o aviso crítico.
- **Migas de pan (*breadcrumbs*):** componente de navegación secundaria que muestra al usuario la ruta de categorías seguida hasta llegar a la página actual.
- **Enlaces:** hipervínculos textuales o gráficos que conectan documentos o recursos del sistema.

### 3.4. Patrones comunes de organización web

La repetición de soluciones efectivas a problemas de diseño ha consolidado una serie de patrones estructurales o *layouts* estándar que los frameworks CSS —como Bootstrap— y las especificaciones nativas —como CSS Grid y Flexbox— permiten implementar:

- **Patrón F:** los usuarios tienden a leer las pantallas saturadas de texto dibujando una letra F: dos pasadas horizontales en la zona superior y un escaneo vertical en el lateral izquierdo.
- **Patrón Z:** típico de las *landing pages* con poco texto y un enfoque visual. El ojo viaja horizontalmente por la cabecera, cruza la pantalla en diagonal hacia la esquina inferior opuesta y finaliza en una línea horizontal donde suele colocarse la CTA principal.
- **Patrón de rejilla de tarjetas:** estándar habitual en plataformas audiovisuales y comercios electrónicos. Organiza el contenido en celdas homogéneas y adaptables, maximizando el volumen de datos visualizables sin saturar el procesamiento del usuario.

!!! salto-pagina-pdf ""