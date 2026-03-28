**Mejora la disponibilidad y el rendimiento de los servicios globales**

- Utiliza la red global de AWS desde el borde hasta la región
- El tráfico de clientes ingresa a través de la ubicación de borde más cercana disponible.
- Enrutar al cliente al punto final saludable más cercano.
- No requiere conmutación de DNS, la misma dirección IP a nivel mundial.
- [[Anycast]] IP estático

![[Pasted image 20260226183608.png]]

**AWS Global Accelerator** es básicamente la implementación de "lujo" de **Anycast** dentro de la infraestructura de Amazon.

Es un servicio que mejora la disponibilidad y el rendimiento de tus aplicaciones frente a usuarios locales o internacionales utilizando la red privada de AWS.

## ¿Cómo funciona? (El truco de la IP estática)

Normalmente, cuando expones un servicio en la nube, obtienes una IP o un DNS que puede cambiar o que depende de una región específica. Con Global Accelerator:

1. AWS te asigna **dos direcciones IP estáticas Anycast** que son fijas para siempre.
2. Estas IPs no pertenecen a una ciudad, sino que se "anuncian" desde toda la red global de Amazon (más de 200 puntos de presencia o _Edge Locations_).
3. Cuando un usuario intenta entrar a tu app, se conecta al **punto de presencia de AWS más cercano a su casa**, entrando a la red de fibra óptica privada de Amazon lo antes posible, en lugar de viajar por el internet público (que es más lento y ruidoso).

## Diferencias clave con otras soluciones

Es común confundirlo con [[Amazon CloudFront]] (la CDN de AWS) o con un **Load Balancer** simple. Aquí la diferencia:

- **Frente a CloudFront:** CloudFront está hecho para contenido que se puede cachear (fotos, videos, HTML). Global Accelerator sirve para **todo**, incluyendo protocolos que no son web (como juegos online, VoIP o transferencias de datos masivas por UDP/TCP).

- **Frente al Internet Público:** En el internet normal, tus datos pasan por muchos routers de distintas empresas (saltos). Con Global Accelerator, el dato entra a la red de Amazon en tu ciudad y viaja "por dentro" hasta el servidor, reduciendo el [[Jitter]] y la latencia.