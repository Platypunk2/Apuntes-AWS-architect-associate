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

### NAT Gateway (AWS managed)
- Alta disponibilidad automática
- Escala hasta 45 Gbps
- Sin administración
- Más caro (~$0.045/hr + data)

### NAT Instance (EC2 manual)
- Más barato
- Configurable como proxy
- Tú gestionas HA y patches
- Cuello de botella de ancho de banda

---

# Virtual Private Gateway (VGW)
**Conectividad híbrida**

Es el endpoint de AWS en una conexión VPN Site-to-Site o AWS Direct Connect hacia tu datacenter o red on-premise. Se adjunta a una sola VPC. Piénsalo como la "puerta de entrada privada" de tu VPC hacia el mundo corporativo.

![[Pasted image 20260405145623.png]]

## Casos de uso
- Conectar tu oficina o datacenter a AWS de forma privada y encriptada (VPN Site-to-Site)
- AWS Direct Connect: fibra dedicada entre tu datacenter y AWS (más estable y rápido que VPN)
- Extensión de tu red corporativa hacia recursos en una VPC específica.

> [!NOTE]
> **Limitación clave:** Un VGW solo se puede adjuntar a una VPC. Si tienes 10 VPCs y necesitas conectar todas a tu datacenter, necesitas 10 VGWs o, mejor, un **Transit Gateway**

---
# Transit Gateway (TGW)
**Hub de conectividad**

Es un router central en la nube. Permite conectar múltiples VPCs, cuentas AWS y redes on-premise entre sí a través de un único punto de control. Reemplaza la arquitectura de VPC peering en mall (que se vuelve inmanejable con muchas VPCs).

![[Pasted image 20260405154235.png]]

## Casos de uso
- Conectar 3+ VPCs entre sí (VPC peering se vuelve cuadrático, TGW es lienal)
- Arquitecturas multi-cuenta AWS Organizations con red compartida
- Conectar on-premise a múltiples VPCs a través de un único punto de entrada
- Centralizar servicios de red (firewall, DNS, NAT compartido)

### VPC Peering
- Sin costo de gateway
- Bajo latencia
- No transitivo: A↔B, B↔C ≠ A↔C
- Inmanejable con 5+ VPCs

### Transit Gateway
- Enrutamiento transitivo
- Multi-cuenta. multi-región
- Costo adicional (~$0.05/hr + datos)
- Latencia ligeramente mayor

---

# API Gateway
**Capa de aplicación**

No es un gateway de red, sino un servicio managed para crear, publicar y proteger APIs HTTP, REST y WebSocket. Es la capa de entrada para tus microservicios y funciones Lambda. Maneja autenticación, throttling, caché, transformación de requests y más

![[Pasted image 20260405155122.png]]

## Tipos de API Gateway

### HTTP API
- Más barato y rápido
- Solo para HTTP/REST básico
- Ideal para Lambda + OIDC/JWT

### REST API
- Más features (caché, transforms)
- Más caro y complejo
- Ideal cuando necesitas todo

### WebSocket API
- Conexiones persistentes
- Chat en tiempo real, notificaciones
- Lambda gestiona las conexiones

### Private API
- Solo accesible desde tu VPC
- Usa Interface VPC Endpoint
- APIs internas de microservicios

> [!NOTE] ¿API Gateway vs ALB
> Usa API Gateway cuando necesitas auth, throttling, transformaciones o es serverless. Usa Application Load Balancer cuando tienes container/EC2 y necesitas routing simple a alto throughput con menor costo por request.


---

# VPC Endpoint & Gateway Endpoint
**Acceso privado a servicios AWS**

Permiten que tu VPS privada acceda a servicios AWS (S3, DynamoDB, SQS, etc.) sin que el tráfico salga a internet. Evitas el NAT Gateway para acceder a servicios AWS, ahorrando costo y mejorando seguridad.

## Tipos de Endpoints

### Gateway Endpoint
- Solo para S3 y DynamoDB
- Gratis
- Entrada en la route table
- No usa IPs privadas

### Interface Endpoint (PrivateLink)
- Para casi cualquier servicio AWS
- ~$0.01/hr + $0.01/GB
- Crea ENI con IP privada en tu subnet 
- Funciona con DNS privado

![[Pasted image 20260405163139.png]]

## Casos de uso
- Lambdas en VPC que acceden a S3 o DynamoDB -> Gateway Endpoint (gratis)
- Instancias privadas que usan SSM, Secrets Manager, ECR -> Interface Endpoint
- Cumplimiento de seguridad: tráfico sensible nunca sale a internet
- Ahorro de costos: evitar NAT Gateway para tráfico a servicios AWS