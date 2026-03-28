**Utilice AWS Direct Connect para vincular de forma segura su entorno local a AWS**

Conecta directamente tu centro de datos a AWS a través de una conexión estándar de fibra óptica Ethernet de 1 gigabit a 10 gigabits

**Conectividad híbridra**
Los entornos híbridos permiten combinar la elasticidad y los beneficios económicos de AWS y continuar utilizando su infraestructura existente.

**Trabajar con grandes conjuntos de datos**
Transfiere tus datos críticos para el negocio directamente desde su centro de datos, oficina o entorno de colocación hacia y desde AWS, pasando por alto su proveedor de servicios de Internet y eliminando la congestión de la red

![[Pasted image 20260225155820.png]]

## Agregar redundancia a mis circuitos dedicados

- Para redundancia, DX se puede implementar con uno o múltiples:
	- Circuitos
	- Proveedores
	- Gateways de clientes
	- Direct Connect Locations
	- Centros de datos de clientes
- Enrutamiento BGP para redundancia
- AWS VPN también se puede utilizar como ruta de copia de seguridad.

![[Pasted image 20260225172406.png]]

## Direct Connect Locations
**¿Cómo acceder a mis VPC o a AWS Public Services a través de mi DX?**

- VIFs: Interfaz Virtual
- VIFs privados
	- Acceso a la dirección IP de la VPC
- VIFs públicos
	- Acceso al espacio de direcciones IP públicas de AWS
![[Pasted image 20260225201133.png]]

## AWS Direct Connect Gateway
**Cómo conectarse a varias regiones/cuentas de AWS a través de DX**

- Recurso global
- Conectarse a varias VPC.
- Los VPC pueden estar en iguales o diferentes:
	- Regiones
	- Cuentas (mismo ID de pagador)
- Permite el flujo de tráfico de la VPC a la conexión DX
	- Para el tráfico de VPC a VPC, considere usar AWS Transit Gateway
![[Pasted image 20260225201444.png]]

