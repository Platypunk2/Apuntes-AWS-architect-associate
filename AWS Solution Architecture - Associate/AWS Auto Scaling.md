**Supervisa y ajusta automáticamente la capacidad para mantener un rendimiento estable y predecible al menor costo posible.**

El **AWS Auto Scaling** es el servicio que permite que tu infraestructura "respire". Su función principal es ajustar automáticamente la cantidad de recursos (como instancias de EC2) para mantener un rendimiento óptimo al menor costo posible.

Imagina que tienes una tienda online: el Auto Scaling añade servidores cuando hay un Black Friday y los apaga cuando todos se van a dormir.

- **Servicio de Escalamiento**
	Administra flotas de spot, escala tareas de ECS, tablas de DynamoDB, réplicas de Aurora y otros recursos necesarios para que una aplicación escale de manera efectiva.
- **Escalamiento Predictivo**
	Predice el tráfico futuro, incluidos los picos que ocurren regularmente, y proporciona el número correcto de instancias EC2 antes de los cambios previstos.

## Grupos de Auto Scaling de Amazon EC2
**Colección de instancias de [[Amazon EC2]] que se tratan como una agrupación lógica.**

Permite el uso de funciones de Auto Scaling de EC2, como reemplazos de comprobación de estado y políticas de escalado. El grupo lanza suficientes instancias para cumplir con la capacidad deseada y se mantiene mediante la realización de comprobaciones periódicas de estado. El grupo Auto Scaling es el grupo definido de instancias que es administrado por las políticas de Auto Scaling de EC2.

Se pueden lanzar instancias bajo demanda, instancias puntuales o ambas. Se deben definir plantillas para los grupos, teniendo en cuenta múltiples Zonas de Disponibilidad.

![[Pasted image 20260304175530.png]]
