**Cada gateway resuelve un problema distinto de conectividad. La clave es identificar qué quieres conectar y en qué dirección fluye el tráfico.**

Los gateways de AWS se dividen en dos familias que no deben confundirse:

- **Gateways de red:** Controlan el tráfico entre redes
	El internet Gateway y el NAT Gateway son complementarios - el IGW es bidireccional para subnets públicas, el NAT es unidireccional para dar salida a subnets privadas. El Virtual Private Gateway y el Transit Gateway son para conectividad híbrida con tu datacenter, siendo el TGW el que escala cuando tienes múltiples VPCs

- **Gateway de servicio:** Evitan salir a internet para llegar a AWS
	El Gateway Endpoint (gratis, solo S3/DynamoDB) y las Interface Endpoints (PrivateLink) son frecuentemente ignorados pero ahorran tanto costos de NAT como riesgo de seguridad. Si tu Lambda en VPC accede a S3, nunca debería pasar por un NAT Gateway.


> [!Note] API Gateway
> **API Gateway** es diferente a todos: no es infraestructura de red sino una capa de aplicación para gestionar APIs. Se confunde porque lleva "gateway" en el nombre pero opera en capa 7.

---
# Mapa de gateways AWS
**Cada gateway resuelve un problema distinto de conectividad. La clave es identificar qué quieres y en qué dirección fluye el tráfico.**


| GATEWAY                     | ¿PARA QUE SIRVE?                                                      | CUÁNDO USARLO                                                |
| --------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------ |
| **🌐 Internet Gateway**     | Conecta subnets públicas a internet (bidireccional)                   | Servidores web, load balancers, instancias con IP pública    |
| **🔁 NAT Gateway**          | Permite salida a internet desde subnets privadas (unidireccional)     | EC2 privadas que debn descargar update, llamar APIs externas |
| **🔒 Virtual Private GW**   | Conecta tu datacenter o red on-premise a AWS via VPN / Direct Connect | Hybrid cloud, conexión corporativa segura a una sola VPC     |
| **🔀 Transit Gateway**      | Hub central para conectar múltiples VPCs y redes on-premise           | Multi-VPC, multi-cuenta, arquitecturas hub-and-spoke         |
| **⚡ API Gateway**           | Puerta de entrada HTTP/WebSocket para tus APIs y microservicios       | Serverless (Lambda), microservicios REST/GraphQL, WebSockets |
| **🎯 VPC Endpoint / SvcGW** | Acceso privado a servicios AWS sin salir a internet                   | S3, DynamoDB, o cualquier servicio AWS desde una VPC privada |
> [!NOTE] Regla rápida
> - ¿quieres llegar a internet? → Internet GW o NAT.
> - ¿Conectar redes privadas? → VPN/DX + Virtual Private GW o Transit GW.
> - ¿Llamar servicios AWS sin internet? → VPC Endpoint.

---
# Internet Gateway (IGW)
**Conectividad pública**

Es la puerta de entrada/salida entre tu VPC y el internet público. Se adjunta a nivel de VPC (no de subnet). Para que una instancia sea accesible desde internet, necesita: IGW adjunto + subnet público + IP público o Elastic IP + route table apuntando al IGW.

![[Pasted image 20260405130756.png]]

## Casos de uso
- Servidores web y load balancers que deben ser accesibles desde internet
- Bastion hosts para acceso SSH administración
- Instancias que necesitan recibir tráfico entrante del exterior

> [!NOTE]
> Solo poner el IGW no es suficiente: debes configurar la route table de la subnet con 0.0.0.0/0 -> igw-xxxx y asignar una IP pública a la instancia.

---

# NAT Gateway
**Salida privada a internet**

Permite que instancias en subnets **privadas** se conecten hacia internet (para updates, llamar APIs externas, etc.) sin ser accesibles desde internet. Actúa como intermediario: hace Network Address Translation. Siempre vive en una subnet pública y necesita un IGW.

![[Pasted image 20260405131355.png]]

## Casos de uso
- EC2 privadas que necesitan instalar paquetes o descargar updates (yum, apt)
- Lambdas en una VPC que llaman APIs externas (Stripe, Twilio, etc.)
- Aplicaciones backend que deben consultar servicios de terceros sin exponerse


> [!NOTE]
> Si múltiples subnets privadas necesitan acceso a internet, todas apuntan al mismo NAT Gateway en su route table: 0.0.0.0/0 -> nat-xxxx

