CloudFront es una red de entrega de contenido ([[CDN - Content Delivery Network]]). Reduce la latencia para los usuarios finales al aprovechar lo más de 450 puntos de presencia en la red de AWS para entregar contenido a una audiencia global.
  
> **Consejo de examen**
> Cualquier pregunta de examen que aborde la distribución de contenido a una audiencia global (especialmente contenido estático) suele apuntar al uso de Amazon CloudFront.

==**Red de entrega de contenido (CDN) con baja latencia y alta velocidad de transferencia**==

## Resumen del servicio
Servicio web que agiliza la distribución de contenido web estático y dinámico a los usuarios finales. Enruta las solicitudes de contenido a la ubicación perimetral con la latencia más baja para optimizar el rendimiento.

## Casos de uso
* Entregar sitios web rápidos y seguros.
* Acelera la entrega dinámica de contenido y las API.
* Transmitir video en vivo y bajo demanda.
* Distribuir parches y actualizaciones.
![[Pasted image 20260222164652.png]]
El contenido que no es lo suficientemente popular como para almacenarlo en un POP se almacenará en una caché regional de borde para acercar más contenido a los usuarios. Útil para contenido con una caída en popularidad en el tiempo.

## Cómo funciona
Ubicaciones de CloudFront entre el servidor de origen y los [[POP - Point of Presence]], con una caché más grande que los POP individuales. Sirve como punto intermediario para el contenido. Las solicitudes van del usuario, a la ubicación del borde, a las cachés regionales de borde, verificando la disponibilidad de contenido en cada sitio antes de solicitar directamente desde el servidor de origen.

### Cuando un usuario hace una solicitud
1. La petición va al **POP más cercano geográficamente**.
2. Ese POP revisa si tiene el contenido en caché.
3. Si lo tiene → lo entrega inmediatamente.
4. Si no lo tiene → consulta primero la **Regional Edge Cache**
5. Si tampoco está ahí → recién va al **servidor de origen** (por ejemplo, S3, EC2, etc.).