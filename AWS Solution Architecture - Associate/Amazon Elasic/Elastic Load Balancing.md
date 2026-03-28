**Elastic Load Balancing (ELB) distribuye automáticamente el tráfico entrante de aplicaciones entre múltiples destinos y dispositivos virtuales en una o más zonas de disponibilidad (AZ)**

![[Pasted image 20260304195850.png]]
## Capacidades clave
- **Seguridad**
	Uso con VPC, crea y administra grupos de seguridad asociados con un ELB para obtener opciones adicionales de red y seguridad. Configura como un balanceador de carga de internet o de cara interna.

- **Alta disponibilidad**
	Distribuye el tráfico a través de una o varias AZ. Escala automáticamente su capacidad de manejo de solicitudes en respuesta al tráfico de aplicaciones entrante.

- **Alto rendimiento**
	Maneja el tráfico a medida que crece, a millones de solicitudes por segundo y patrones de tráfico repentinos y volátiles.

- **Comprobaciones de salud**
	Solo encamina el tráfico a objetivos saludables. Proporciona información sobre los servicios respaldados por ELB y las métricas sobre las patrones de tráfico para los servicios que se ejecutan en instancias.

![[Pasted image 20260304195903.png]]


---
**Distribuye el tráfico de red para mejorar la escalabilidad de tus aplicaciones**

Distribuye automáticamente el tráfico entrante de aplicaciones entre múltiples destinos, como instancias de Amazon EC2 ([[Amazon EC2]]), contenedores, direcciones IP, funciones Lambda y dispositivos virtuales.

![[Pasted image 20260312165652.png]]
## Disponibilidad
Elastic Load Balancing forma parte de la red de AWS, con conocimiento nativo de los límites de falla, como las zonas de disponibilidad, para mantener tus aplicaciones disponibles en toda la región.

## Monitoreo
Supervisa el estado de tus aplicaciones y su rendimiento en tiempo real con las métricas, el registro y el seguimiento de solicitudes de Amazon CloudWatch.

---
## Application Load Balancer (ALB)
- Capa 7
- Objetivos: IP, instancia, AWS Lambda
- Termina los flujos
- Oyentes: HTTP, HTTPS, gRPC
- Front end: IP virtual
![[Pasted image 20260312170015.png]]

## Network Load Balancer (NLB)
- Capa 4
- Objetivos:
	- IP
	- Instancia
	- balanceador de carga de aplicaciones
- Termina los flujos
- Oyentes: TCP, UDP, TLS
- Front end: IP virtual
![[Pasted image 20260312173157.png]]


## Gateway Load Balancer (GLB)
- Balanceo de carga de capa 3 y puerta de enlace de capa 4
- Objetivos:
	- IP
	- Instancia
- Paso transparente de flujos
- Oyente: IP
- Entrada a la tabla de ruta
![[Pasted image 20260312173327.png]]

Beneficios de la arquitectura:
- Escala y reduce costos.
- Confiabilidad.
- Reduce la complejidad y despliega más rápido.
- Como servicio.
- Utilice los mismo dispositivos de red en AWS y entornos híbridos.