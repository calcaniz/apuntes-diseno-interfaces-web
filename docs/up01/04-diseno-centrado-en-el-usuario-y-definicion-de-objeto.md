Uno de los errores con mayor repercusión en la ingeniería del software consiste en iniciar la fase de maquetación y desarrollo *front-end* basándose exclusivamente en los gustos personales del programador, la intuición del diseñador o la lista de deseos del cliente. Desarrollar una interfaz sin analizar previamente a las personas que utilizarán el proyecto puede conducir al fracaso operativo.

El **diseño centrado en el usuario (DCU)** es un enfoque metodológico que sitúa explícitamente a las personas usuarias, sus necesidades, sus limitaciones y sus contextos de uso en el centro de cada una de las fases del ciclo de vida del producto: análisis, diseño, prototipado e implementación.

El principio fundamental del DCU en el desarrollo de interfaces es la **empatía técnica**. El sistema debe adaptarse al modelo mental del usuario final y no exigir que el usuario aprenda a pensar como el programador que creó el sistema.

### 4.1. Definición y alineación de objetivos web

Todo software web responde a un propósito. Para que una interfaz sea eficiente, es necesario identificar y ponderar tanto el objetivo principal como los secundarios antes de escribir la primera línea de código.

- **Objetivo principal (*core goal*):** es la razón de ser de la aplicación web y la métrica o conversión prioritaria que justifica su desarrollo. Debe ser claro, medible y visible en el diseño.
- **Objetivos secundarios:** son metas complementarias que aportan valor añadido, fidelizan o permiten obtener datos sin entorpecer el flujo del objetivo principal.

### 4.2. Tipologías de usuarios y definición de perfiles

Una interfaz no puede ni debe diseñarse para «todo el mundo», ya que intentar gustar a todos suele dar lugar a una aplicación genérica e ineficiente. El equipo de desarrollo debe clasificar y caracterizar a sus destinatarios:

- **Usuarios novatos o esporádicos:** necesitan interfaces muy guiadas, metáforas claras, mensajes de ayuda explícitos y poca densidad de opciones en pantalla.
- **Usuarios expertos o avanzados:** priorizan la velocidad de ejecución, los atajos, la densidad de información y la posibilidad de personalizar el panel de trabajo.

El modelado mediante **arquetipos** es una técnica de ingeniería de requisitos que consiste en crear perfiles ficticios pero realistas basados en datos de los usuarios del sistema. Un arquetipo incluye:

- **Datos demográficos y contexto:** edad, profesión, dispositivo y entorno de uso.
- **Objetivo:** qué quiere conseguir exactamente dentro de la aplicación.
- **Puntos de dolor (*pain points*):** qué le frustra de las soluciones o sitios web actuales.

!!! salto-pagina-pdf ""

### 4.3. Identificación y jerarquización de acciones principales

Una vez analizados el perfil del usuario y los objetivos del proyecto, deben identificarse las **tareas clave** que la interfaz facilitará con la máxima prioridad visual.

Para garantizar la usabilidad de estas acciones, la interfaz debe aplicar tres reglas en la distribución de elementos:

1. **Regla de los tres clics:** el usuario debería poder alcanzar las funcionalidades o contenidos prioritarios realizando un máximo de tres interacciones desde la página de inicio.
2. **Reducción de la fricción visual:** las acciones principales deben materializarse en componentes destacados, relegando las acciones secundarias a enlaces de menor peso visual.
3. **Prevención y tolerancia a errores:** la interfaz debe ser benévola. Si la acción principal implica riesgo, debe requerir confirmación. Si el usuario comete un error en un formulario, el sistema debe indicar exactamente dónde está el fallo sin borrar los datos ya introducidos.

!!! salto-pagina-pdf ""