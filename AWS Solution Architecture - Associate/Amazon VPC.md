**Aprovisiona una sección lógicamente aislada de la nube de AWS**
- Controla tu entorno de redes virtuales
	- Subredes
	- Tablas de enrutamiento
	- Grupos de Seguridad
	- ACL de red
- Controla si tus instancias acceden a Internet y cómo
- Conéctate a tu red local a través de VPN o Direct Connect

**Aprovisiona una sección lógicamente aislada de la nube de AWS**

![[Pasted image 20260223183504.png]]

## VPC IP Addressing
**Trae tu propio plan de direccionamiento.**

- ¡Planifica tu espacio de direcciones de IP antes de crearlo!
- Considera la expansión futura de la región de AWS.
- Considera la conectividad futura a las redes corporativas.
- Considera el diseño de subred.
- Las VPC pueden ser entre /16 y /28
- El [[CIDR - Classless Inter-Domain Routing]], no se puede modificar una vez creado.
	- Pero puede agregar nuevos CIDR para expandir el direccionamiento IP de VPC.
- Espacios de IP superpuestos = ¡futuro dolor de cabeza!


![[Pasted image 20260223184643.png]]

## Segmentación de redes dentro de una VPC
**Subredes de VPC**

- Puedes agregar una o más subredes en cada Zona de Disponibilidad.
- AZs proporciona aislamientos de fallas.
- Las subredes se asignan como un subconjunto del rango CIDR de VPC
![[Pasted image 20260224180539.png]]
- Cada subred puede tener una tabla de enrutamiento única.
- Las tablas de de enrutamiento dirigen el tráfico fuera de la VPC, hacia:
	- Internet Gateway
	- Virtual Private Gateway
	- VPC Endpoints
	- Direct Connect
	- VPC [[Peering]]
	- AWS Transit Gateway
- Las subredes se llaman "Subredes públicas" cuando se conectan a Internet Gateway.

## Conectar VPC a Internet
**Internet Gateway**

- Componente de VPC de alta disponibilidad, redundante y escaldo horizontalmente.
- Conecta tus subredes de VPC a Internet.
- Debe ser referenciado en la tabla de enrutamiento.
- Realiza NAT entre direcciones IP públicas y privadas.

![[Pasted image 20260224182421.png]]

**Dirección IP elástica**
- Dirección IPv4 pública estática, asociada a su cuenta de AWS.
- Se puede asociar con una instancia o interfaz de su red.
- Se puede reasignar a otra instancia en tu cuenta
- Útil para redundancia cuando los balanceadores de carga no son una opción.
 ![[Pasted image 20260225102215.png]]

**NAT Gateway**
- Habilitar la conexión de salida a Internet.
- Sin conexión entrante - útil para actualizaciones de OS/paquetes, acceso a servicios web públicos.
- Totalmente administrado por AWS.
- Altamente disponible.
- Ancho de banda de hasta 100 Gbps
- Soporta protocolos TCP, UDP e ICMP
- Las ACL de red se aplican al tráfico de la puerta de enlace NAT ([[NAT - Network Address Translation]]).
![[Pasted image 20260225103116.png]]

## VPC Compartida
**Una cuenta usando la VPC de otra**

- EL propietario de VPC puede crear y editar componentes de VPC.
- Los participantes de VPC pueden lanzar recursos en sus subredes asignadas.
- Cada participante paga sus propios recursos y costos de transferencia de datos.
- Basado en AWS Resource Access Manager, bajo AWS Organizations.
![[Pasted image 20260225104915.png]]

## Grupos de Seguridad
**Filtrado de tráfico a instancias**

- VPC Firewall virtual con estado.
- Reglas definidas por clientes entrantes y salientes.
- Inspección a nivel de instancia/interfaz:
	- Micro segmentación.
	- Obligatorio, todas las instancias tienen un grupo de seguridad asociado.
- Se puede hacer referencia cruzada.
	- Funciona a través de VPC Peering
- Solo admite reglas de permitir.
	- Implícito negar todo al final.

![[Pasted image 20260225120955.png]]

## Listas de control de acceso a la red (NACL)
**Filtrado de tráfico a nivel de subred ([[NACL - Network Access Control List]])** 

- Entrante y Saliente.
- Inspección a nivel de subred.
- Nivel opcional de seguridad.
- Por defecto, permite todo el tráfico.
- Sin estado.
- Basado en puertos IP y TCP/UDP.
- Admite reglas de permitir y denegar.
- Negar todo al final.

![[Pasted image 20260225123624.png]]

## NACL v/s Grupo de Seguridad
[[Grupos de seguridad y NACL de AWS]]

Ambos funcionan como "muros" para controlar el tráfico, operan en niveles diferentes y tienen reglas de juego distintas.

El **Security Group (SG)** es como el guardia de seguridad en la puerta de tu oficina, mientras que el **Network ACL (NACL)** es como el control de acceso en la entrada principal del edificio completo.

|**Característica**|**Security Group (SG)**|**Network ACL (NACL)**|
|---|---|---|
|**Nivel de operación**|Instancia (Capa de Host/ENI)|Subred (Capa de Red)|
|**Estado (Statefulness)**|**Stateful**: Si permites entrada, la salida se permite automáticamente.|**Stateless**: Debes configurar reglas de entrada y salida explícitamente.|
|**Reglas de Denegación**|Solo permite reglas de "Permitir". Todo lo demás se deniega por defecto.|Permite reglas de **Permitir** y **Denegar**.|
|**Orden de evaluación**|Se evalúan todas las reglas antes de decidir.|Se evalúan en orden numérico (la regla más baja manda).|
|**Aplicación**|Se aplica a una instancia (EC2, RDS, etc.).|Se aplica a todas las instancias dentro de una subred.|
Esta es la diferencia más importante a nivel técnico:

- **Security Group (Stateful):** Si abres el puerto 80 para recibir tráfico web, el SG "recuerda" esa conexión y permite que la respuesta salga hacia el usuario sin que tengas que configurar nada más.
- **NACL (Stateless):** No tiene memoria. Si permites tráfico entrante por el puerto 80, también debes crear una regla de salida (generalmente abriendo los puertos efímeros) para que la respuesta pueda volver al cliente. De lo contrario, el paquete se bloquea al salir.

## VPC Endpoints: interfaz y punto final
**Conéctese de forma privada a los servicios públicos de AWS**

- Conecta tu VPC a:
	- Servicios de AWS compatibles.
	- Servicios de punto final de VPC con tecnología PrivateLink.
- No requiere IPs públicas ni conectividad a Internet
- El tráfico no sale de la red de AWS.
- Escalado horizontalmente, redundante y de alta disponibilidad.
- Control de acceso robusto

![[Pasted image 20260225143242.png]]

## VPC Peering
**Conexión directa a otras VPC**

- Escalable y alta disponibilidad.
- Peering entre cuentas.
- Regiones de AWS iguales o diferentes.
- Tráfico bidireccional.
- Se puede hacer referencia a los grupos de seguridad remota.
- Política de enrutamiento con tablas de ruta; no todas las subredes necesitan conectarse entre sí.
- Sin enrutamiento transitivo, requiere malla completa para interconectar varias VPC.
- No hay soporte para direcciones IP superpuestas.

![[Pasted image 20260225143257.png]]
