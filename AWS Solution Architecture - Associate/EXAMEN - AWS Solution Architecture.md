Este certificado muestrea conocimientos y habilidades en tecnología de AWS, en una amplia gama de servicios. Se centra en el diseño de soluciones optimizadas para costos y rendimiento.

El certificado cubre conceptos relacionados con computo, base de datos, almacenamiento, *networking* (redes), monitoreo y seguridad.

[https://ingjulianrodriguez.github.io/SimuladorExamenAWS-/](https://ingjulianrodriguez.github.io/SimuladorExamenAWS-/ "https://ingjulianrodriguez.github.io/SimuladorExamenAWS-/")

[[Amazon CloudFront]]
[[Amazon IAM - Identify and Access Management]]
[[Amazon Simple Storage Service (S3)]]
[[Amazon VPC]]
[[Amazon Route 53]]
[[AWS Direct Connect]]
[[AWS Transit Gateway]]
[[Grupos de seguridad y NACL de AWS]]
[[AWS Global Accelerator]]
[[AWS Storage Gateway]]
[[Amazon ElastiCache]]
[[Amazon Elastic File System (EFS)]]
[[Amazon FSx]]
[[Amazon RDS (Relational Database Service)]]
[[Amazon DynamoDB]]
[[Amazon Aurora]]
[[Amazon EC2]]
[[AWS Auto Scaling]]
[[Elastic Load Balancing]]
[[Grupos de ubicación para instancias de Amazon EC2]]
[[Amazon Machine Images (AMI)]]
[[AWS Key Management Service (KMS)]]
[[Amazon CloudTrail]]
[[AWS WAF - Web Application Firewall]]
[[Amazon Shield]]
[[Amazon Firewall Manager]]



| **Servicio / Tema**        | **¿Qué es?**                               | **¿Para qué se usa?**                                                    | **Concepto clave de examen**                      |
| -------------------------- | ------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------- |
| **Amazon CloudFront**      | CDN (Content Delivery Network) global      | Distribuir contenido con baja latencia usando caché en _Edge Locations_. | Reduce latencia y descarga el servidor origen.    |
| **Amazon IAM**             | Gestión de identidades y accesos           | Controlar quién (usuarios/roles) puede hacer qué en AWS.                 | **Principio de menor privilegio**.                |
| **Amazon S3**              | Almacenamiento de objetos                  | Guardar archivos, backups, logs, sitios estáticos.                       | **11 nueves** ($99.999999999\%$) de durabilidad.  |
| **Amazon VPC**             | Red virtual privada en la nube             | Definir subnets, IPs, tablas de rutas, gateways.                         | Aislamiento y control total de red.               |
| **Amazon Route 53**        | Servicio DNS administrado                  | Resolver dominios y enrutar tráfico.                                     | _Routing policies_ (Simple, Latency, Failover).   |
| **AWS Direct Connect**     | Conexión dedicada física                   | Conectar _on-premise_ con AWS de forma privada.                          | Más estable y seguro que una VPN por internet.    |
| **AWS Transit Gateway**    | Hub central de red                         | Conectar múltiples VPCs y redes on-premise.                              | Modelo **Hub-and-Spoke** para simplificar redes.  |
| **Security Groups**        | Firewall a nivel de **instancia**          | Controlar tráfico entrante/saliente de una EC2.                          | **Stateful**: permite el tráfico de retorno auto. |
| **NACL**                   | Firewall a nivel de **subnet**             | Control adicional de tráfico en toda la subred.                          | **Stateless**: debes permitir entrada Y salida.   |
| **AWS Global Accelerator** | Servicio de optimización de red            | Enrutar tráfico por la red global de AWS usando IPs estáticas.           | Mejora la disponibilidad usando **Anycast IP**.   |
| **AWS Storage Gateway**    | Almacenamiento híbrido                     | Conectar aplicaciones _on-premise_ con S3.                               | Puente entre tu oficina física y la nube.         |
| **Amazon ElastiCache**     | Base de datos en memoria (Redis/Memcached) | Acelerar aplicaciones leyendo datos de la RAM.                           | Almacenamiento **In-memory** para baja latencia.  |
| **Amazon EFS**             | Sistema de archivos elástico (NFS)         | Almacenamiento compartido para múltiples instancias **Linux**.           | Escalable automáticamente y montable vía red.     |
| **Amazon FSx**             | Sistemas de archivos especializados        | Ejecutar sistemas nativos como Windows (SMB) o Lustre.                   | Rendimiento extremo o compatibilidad Windows.     |