**Sencillo, sin servidor, sistema de archivos de configuración y olvido**

Amazon EFS es un sistema de archivos compartidos dentro de AWS basado en Network File System (NFS)
- Se puede compartir entre muchas instancias EC2
- Servicio privado, a través de puntos de montaje, dentro de una VPC.

EFS se puede montar en instancias Linux EC2, o incluso servidores locales siempre que se hayan configurado y configurado redes privadas entre la red y AWS.

![[Pasted image 20260303100411.png|697]]

### EFS es:
- Es un file system compartido (NFS)
- Permite que múltiples instancias accedan a los mismos archivos
- Bueno para aplicaciones compartidas, contenedores, [[CMS - Content Management System]]
- No esta optimizado para cargas de alta [[IOPS]] típicas de bases de datos transaccionales críticas