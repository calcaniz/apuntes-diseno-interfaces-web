# 8. El diagrama jerárquico

Un diagrama jerárquico es una representación gráfica organizada en forma de árbol que muestra la relación de dependencia, la profundidad y el orden lógico de todos los nodos que componen una aplicación web.

Cumple principalmente las siguientes funciones:

1. **Plano de desarrollo:** guía la creación de las rutas de la aplicación y la estructura de directorios del proyecto.
2. **Valoración del alcance:** permite al equipo y al cliente verificar que ningún contenido o funcionalidad se ha quedado fuera antes de iniciar la fase de maquetación.
3. **Control de la complejidad:** muestra de forma inmediata si la aplicación está creciendo de manera descompensada o ineficiente.

Para construir un diagrama jerárquico con rigor técnico deben aplicarse conceptos de la teoría de grafos y árboles de datos:

- **Página raíz (*root*):** nodo superior de la jerarquía y punto de entrada principal desde el que ramifican las demás dependencias.
- **Relación padre-hijo (*parent-child*):** expresa una dependencia lógica. Un nodo padre engloba conceptualmente a sus nodos hijos.
- **Relación entre nodos hermanos (*siblings*):** nodos situados en el mismo nivel jerárquico, que comparten el mismo nodo padre y poseen un peso funcional similar.
- **Nivel de profundidad:** distancia en clics o saltos desde la página raíz hasta un nodo determinado.

Según su relevancia, podemos distinguir los siguientes niveles:

- **Nivel 1. Sección:** grandes bloques temáticos o funcionales directamente accesibles desde la navegación principal.
- **Nivel 2. Subsección:** divisiones especializadas dentro de una sección.
- **Nivel 3. Página final o de detalle:** vista atómica donde se consume el contenido específico o se ejecuta una acción concreta.

Un aspecto crítico consiste en controlar la profundidad del árbol. Deben evitarse dos extremos:

- **Estructuras excesivamente profundas:** obligan al usuario a realizar muchos clics para llegar al contenido.
- **Estructuras excesivamente planas:** muestran demasiadas opciones en el primer nivel, saturan el menú principal y provocan sobrecarga cognitiva.

!!! salto-pagina-pdf ""

Para auditar la calidad del diagrama antes de pasar al prototipado podemos utilizar estos criterios:

- **Claridad:** ¿se entiende la estructura de un vistazo sin confusión de dependencias?
- **Coherencia:** ¿cada sección agrupa exclusivamente contenidos o funciones interrelacionadas?
- **Profundidad:** ¿la información crítica se encuentra en un máximo de tres niveles?
- **Etiquetado:** ¿los nombres de los nodos son claros, inequívocos y familiares para el usuario?
- **Completitud:** ¿incluye todos los contenidos y funciones recogidos en el inventario?

!!! salto-pagina-pdf ""
