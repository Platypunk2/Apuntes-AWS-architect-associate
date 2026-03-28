**Una solución de almacenamiento en la nube híbrida que proporciona acceso local al almacenamiento en la nube**

Storage Gateway proporciona un mecanismo para conectar recursos locales a cantidades casi infinitas de almacenamiento en la nube. Hay tres tipos de gateways:
- Puerta de enlace de archivos, puerta de enlace de volumen y puerta de enlace de cinta.

Normalmente, para subir algo a **Amazon S3**, necesitarías usar una API, el CLI de AWS o un SDK (programación). Con Storage Gateway, tus servidores "ven" a S3 como si fuera un disco duro local, una carpeta compartida en la red o una unidad de cinta magnética.
## Casos de uso

Storage Gateway tiene varios casos de uso. Como arquitecto de soluciones y en el examen, esos incluyen:
- Migraciones (Mover copias de seguridad a la nube).
- Modernización (Utilice recursos compartidos de archivos locales respaldados por almacenamiento en la nube).
- Reinvención continua (acceso de baja latencia para aplicaciones locales a datos en la nube).
![[Pasted image 20260226191457.png]]

# AWS Storage Gateway - Tipos
**Una solución de almacenamiento en la nube híbrida que proporciona acceso local al almacenamiento en la nube**

- **S3 File Gateway**
	Acceso a archivos nativos a S3 para copias de seguridad, archivos e ingesta para lagos de datos.
- **FSx File Gateway**
	Acceso nativo a Amazon FSx para recursos compartidos de archivos de grupo locales y directorios particulares.
- **Tape Gateway**
	Reemplazo directo para infraestructura de cinta física respaldada por almacenamiento en la nube con almacenamiento en caché local.
- **Volume Gateway**
	Bloquea el almacenamiento local respaldado por almacenamiento en la nube con almacenamiento en caché local, instantáneas de EBS y clones, integrado con AWS Backup.

![[Pasted image 20260226194029.png]]
