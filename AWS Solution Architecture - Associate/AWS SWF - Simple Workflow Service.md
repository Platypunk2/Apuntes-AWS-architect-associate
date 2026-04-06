**Facilita la coordinación del trabajo distribuido en múltiples componentes de una aplicación**

Se puede utilizar para integrar flujos de trabajo entre servidores on-premise y AWS.


Amazon Simple Workflow Service (Amazon SWF) ayuda a los desarrolladores a diseñar, ejecutar y escalar trabajos en segundo plano que tienen pasos paralelos o secuenciales. Puede pensar en Amazon SWF como un rastreador de estados y un coordinador de tareas totalmente gestionado en la nube.

En caso de que los pasos de la aplicación empleen más de 500 milisegundos para finalizar, necesite hacer un seguimiento del estado del procesamiento así como reintentar una operación si una tarea falla, Amazon SWF puede ayudarle.

---
Es un servicio de AWS que permite **coordinar tareas** entre múltiples componentes de una aplicación, garantizando que se ejecuten en el **orden correcto**, sin perder el estado del proceso aunque algún paso falle o tarde mucho tiempo.

### Conceptos clave

|Concepto|Qué es|
|---|---|
|**Workflow**|El proceso completo de principio a fin|
|**Activity Task**|Una tarea individual dentro del workflow|
|**Decider**|El cerebro: decide qué tarea ejecutar a continuación|
|**Worker**|El que ejecuta la tarea (puede estar en AWS o on-premise)|
|**Domain**|Contenedor lógico que agrupa los workflows|

---

### Características importantes

- Garantiza que **cada tarea se ejecute exactamente una vez**
- Mantiene el **estado del workflow** aunque pasen días o meses
- Los workers pueden estar **en cualquier lugar**: EC2, Lambda, servidores físicos, etc.
- Timeout configurable de hasta **1 año**
