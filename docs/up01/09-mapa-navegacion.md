
Un mapa de navegación es una representación gráfica y funcional del ecosistema de pantallas de una aplicación web. Detalla los flujos de interacción o *user flows* y los caminos que un usuario puede seguir para desplazarse de un punto a otro de la interfaz.

Mientras que el inventario responde a **qué hay** y el diagrama jerárquico indica **dónde se ubica**, el mapa de navegación responde a **cómo se llega y cómo se regresa**.

Al diseñarlo deben identificarse y trazarse los siguientes elementos:

1. **Pantallas o nodos principales:** representan los puntos de parada o vistas de la aplicación, como páginas HTML, componentes o vistas. Pueden distinguirse vistas de entrada, de catálogo y de proceso o detalle.
2. **Relaciones y tipos de enlaces:** indican cómo se conectan dos vistas mediante hipervínculos, botones y redirecciones:
    - **Jerárquicos o verticales:** conectan una categoría con una subcategoría o página de detalle.
    - **Transversales u horizontales:** enlazan ramas distintas del árbol jerárquico sin necesidad de volver a la raíz.
    - **Regresivos o de retorno:** permiten deshacer un paso o volver a un nivel superior.
3. **Flujo de usuario (*user flow*):** ruta prioritaria diseñada para guiar al usuario a través de un proceso compuesto por varios pasos interconectados. Por ejemplo: Inicio → Ficha de producto → Añadir a la cesta → Formulario de pago → Confirmación de compra.

### 9.1. Tipos de estructuras de navegación

Dependiendo de la naturaleza del sistema, el mapa adoptará uno o varios patrones:

- **Lineal:** secuencia fija, paso a paso, propia de pasarelas de pago, asistentes de configuración o cuestionarios en línea.
- **Jerárquica:** el usuario navega descendiendo desde la página principal y debe retornar al nodo padre para cambiar de tema. Es habitual en portales informativos.
- **En red:** las vistas clave están interconectadas directamente mediante menús globales o enlaces de contexto. Es habitual en aplicaciones web SaaS y redes sociales.
- **Mixta o híbrida:** combina áreas de navegación en red con pequeños flujos lineales aislados.

!!! salto-pagina-pdf ""

### 9.2. Reglas de accesibilidad y control del flujo

Para evitar que el usuario se sienta atrapado o desorientado, el mapa de navegación debe garantizar dos principios:

- **Garantía de retorno:** toda vista debe ofrecer al menos dos vías claras para salir o retroceder.
- **Acceso directo a rutas críticas:** los enlaces que conducen al objetivo principal del sitio deben permanecer accesibles desde cualquier nodo relevante de la navegación.

!!! salto-pagina-pdf ""