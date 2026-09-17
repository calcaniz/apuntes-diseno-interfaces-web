
Cuando ya disponemos del mapa de navegación, pasar directamente al código HTML y CSS suele provocar modificaciones constantes, pérdidas de tiempo y refactorizaciones. La ingeniería del software y el diseño de experiencia de usuario resuelven este problema mediante la representación progresiva de la interfaz.

Este proceso de abstracción permite validar la estructura, la disposición de los elementos, los flujos de interacción y la arquitectura visual desde las primeras fases del proceso.

### 12.1. Mapa de navegación y diseño de pantallas

El mapa de navegación define la visión macroscópica de la aplicación: qué pantallas existen y cómo se conectan. Los wireframes definen la visión microscópica de cada nodo: cómo se organizan internamente los contenidos, controles y zonas de una página.

En el ciclo de diseño se emplean cuatro representaciones con propósitos y costes de elaboración diferentes:

- **Boceto (*sketch*):** dibujo rápido a mano alzada sobre papel o pizarra. Su objetivo es explorar ideas, realizar una lluvia de ideas y descartar tempranamente los esquemas menos adecuados.
- **Wireframe:** esquema estructural en escala de grises y sin detalle estético. Permite validar la jerarquía de la información, el diseño de la rejilla y la presencia de componentes clave sin distracciones visuales.
- **Mockup:** representación estática con el acabado visual final: colores, tipografías e imágenes. Permite definir y validar la estética, el sistema de diseño y la coherencia de marca.
- **Prototipo:** modelo dinámico e interactivo con enlaces, animaciones y transiciones. Simula la experiencia real, permite realizar pruebas de usabilidad y validar microinteracciones.

Debemos evitar aumentar la fidelidad visual demasiado pronto. Añadir colores, imágenes finales o fuentes decorativas en fases iniciales puede distraer al cliente y al equipo de las decisiones fundamentales de arquitectura y usabilidad.

### 12.2. Niveles de fidelidad de los wireframes

Los wireframes pueden clasificarse en tres niveles:

1. **Baja fidelidad:** se elaboran en papel o con herramientas digitales básicas. Utilizan cajas con bordes simples, texto simulado y esquemas sin alineación milimétrica. Su coste de producción es reducido, permiten descartar opciones sin frustración e iterar muchas distribuciones en pocos minutos. Como contrapartida, transmiten con dificultad el comportamiento real y las interacciones complejas.
2. **Media fidelidad:** se diseñan con herramientas vectoriales como Figma o Penpot. Emplean una escala de grises, tipografía estándar legible y cajas proporcionales alineadas a una rejilla. Son habituales para definir *layouts* porque ofrecen claridad estructural sin distracciones cromáticas, aunque requieren destreza con la herramienta.
3. **Alta fidelidad:** incluyen la tipografía definitiva, la paleta real, iconos vectoriales precisos y fotografías o datos representativos. Funcionan como especificación para que el equipo traduzca la pantalla a HTML y CSS, pero presentan un coste de elaboración mayor y más resistencia al cambio si se detecta un fallo estructural.

### 12.3. Prototipos

Una vez creados los wireframes o mockups de las pantallas, el siguiente paso es conectarlos para crear un prototipo navegable. Podemos distinguir:

- **Prototipo estático:** conjunto de capturas o archivos exportados en PNG o PDF para una revisión rápida, pero insuficiente para probar la usabilidad.
- **Prototipo interactivo:** incorpora puntos de activación que conectan las pantallas. Permite validar flujos de trabajo, detectar «callejones sin salida» y reducir costes antes de iniciar el desarrollo.

### 12.4. Herramientas disponibles

Existen múltiples aplicaciones para crear wireframes y prototipos. El desarrollador debe conocer las alternativas y aplicar criterios objetivos de selección.

| Criterio { .table-bg-principal .table-cl-secundario } | Figma { .table-bg-principal .table-cl-secundario } | Penpot { .table-bg-principal .table-cl-secundario } | diagrams.net { .table-bg-principal .table-cl-secundario } |
|---|---|---|---|
| Licencia y modelo | Propietario | Código abierto | Código abierto |
| Enfoque principal | UI/UX profesional y prototipado | UI/UX profesional basado en estándares web | Diagramación estructural, mapas y flujos |
| Tecnología nativa | Propietaria | SVG y CSS | XML y SVG |
| Trabajo colaborativo | Excelente | Excelente | Limitado |
| Sistema de componentes | Muy avanzado | Avanzado | No orientado a sistemas de diseño |
| Inspección para código | Modo desarrollador | Inspección de código CSS nativa y gratuita | Exportación básica |

!!! salto-pagina-pdf ""
