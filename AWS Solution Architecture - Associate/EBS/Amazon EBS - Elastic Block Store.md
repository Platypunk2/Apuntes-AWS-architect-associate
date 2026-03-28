![[Pasted image 20260310105011.png]]

Amazon EBS es un servicio de almacenamiento en bloque de alto rendimiento, seguro y escalable, diseñado para utilizarse con instancias de [[Amazon EC2]]. Funciona como discos duros virtuales persistentes que se adjuntan a servidores en la nube, permitiendo almacenar datos, bases de datos o sistemas de archivos con alta disponibilidad.

**Características clave de Amazon EBS:**

- **Almacenamiento Persistente:** Los datos permanecen disponibles independientemente de la vida útil de la instancia EC2, lo que significa que los datos no se borran aunque apague el servidor.
- **Alta Disponibilidad y Durabilidad:** Los volúmenes se replican automáticamente dentro de una zona de disponibilidad para proteger contra fallos de componentes.
- **Tipos de Volúmenes:** Ofrece opciones basadas en **SSD** (para cargas de trabajo transaccionales rápidas, como bases de datos) y **HDD** (para streaming grande de datos).
- **[Instantáneas](https://www.google.com/search?newwindow=1&client=opera-gx&sca_esv=de893e36d6b67b5c&sxsrf=ANbL-n5Ju1drCxAANkE1CjMCQgpDzKEEOQ%3A1773143299897&q=Instant%C3%A1neas&source=lnms&fbs=ADc_l-bpk8W4E-qsVlOvbGJcDwpn60DczFdcvPnuv8WQohHLTaf9fS4tJ71bi2aHS-Pmeg0IA2nDWC3A9mnYKHxHonOwrj9iWEd2qhtK5hq7tRJECSZ4ZgB8hqsqyEcc1BM40YBE3R6OpCbmLbxvqt3OdT8H-KJkVTH2laqqkqhguhA4URB8MeRD2nzR8c93M5bV2Je_DpYUpUuXfTUlp0MUZxCAH7AM9drbVG38Nq7Jc9f2PILziao&sa=X&ved=2ahUKEwjHkdLYvJWTAxWTr5UCHTVMLAsQgK4QegQIAxAE&biw=1878&bih=956&dpr=1) (Snapshots):** Permite crear copias de seguridad incrementales puntuales de los datos, las cuales se almacenan en Amazon S3 ([[Amazon Simple Storage Service (S3)]]).
- **Elasticidad:** Se puede aumentar la capacidad, cambiar el tipo de volumen o ajustar el rendimiento sin interrumpir el funcionamiento de la aplicación.
- **Cifrado:** Amazon EBS permite cifrar los volúmenes en reposo, los datos en tránsito y las instantáneas utilizando claves gestionadas por el usuario o AWS.

**Proporciona almacenamiento duradero a nivel de bloques para su uso con instancias EC2**

## ¿Qué hace?
Almacenamiento conectado a la red que persiste independientemente de la instancia y actúa como un disco duro físico, similar a la unidad de disco local en una máquina física. Una vez implementado en una AZ, se replica automáticamente para evitar la pérdida de datos y se puede adjuntar a cualquier instancia en la misma AZ.

En volumen EBS individual solo se puede conectar a una instancia EC2. Sin embargo, una instancia puede tener múltiples volúmenes de EBS conectados a ella.

![[Pasted image 20260311135134.png]]
### Ejemplo Práctico: Un Servidor Web de Producción

Imagina que tienes una instancia EC2 corriendo un sitio de comercio electrónico. Así es como se vería la configuración de sus volúmenes:

| **Tipo de Volumen** | **Nombre (Mount Point)** | **Función**                                     | **¿Por qué por separado?**                                                                    |
| ------------------- | ------------------------ | ----------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Volumen A**       | `/dev/sda1` (Root)       | Contiene el Sistema Operativo (Linux/Windows).  | Si el sistema falla, puedes borrarlo sin perder tus datos de ventas.                          |
| **Volumen B**       | `/dev/sdf` (Datos)       | Contiene la base de datos de los clientes.      | Permite hacer snapshots (respaldos) de los datos sin incluir archivos del sistema.            |
| **Volumen C**       | `/dev/sdg` (Logs)        | Guarda todos los registros de acceso y errores. | Evita que, si los logs llenan el disco, el sistema operativo se bloquee por falta de espacio. |
Aunque esa instancia tiene 3 volúmenes conectados, el **Volumen B** no puede estar conectado simultáneamente a una segunda instancia EC2 para que ambas escriban datos al mismo tiempo. Es como un cable USB: solo puede estar enchufado a un puerto a la vez.

---
**Hay cinco tipos de volúmenes de EBS que están disponibles para cargas de trabajo**

| Uso general (SSD)                                                                                                                     | IOPS aprovisionadas (SSD)                                                            | HDD optimizado para rendimiento                                                                             | HDD en Frío                                                                                                    | EBS Magnético                  |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| Volumen de SSD de uso general que equilibra el precio y el rendimiento para una amplia variedad de cargas de trabajo transaccionales. | El volumen de SSD de mayor rendimiento diseñado para aplicaciones de misión crítica. | Volumen de disco duro de bajo costo diseñado para cargas de trabajo de alto rendimiento y acceso frecuente. | Volumen de disco duro de menor costo diseñado para cargas de trabajo a las que se accede con menos frecuencia. | HDD de la generación anterior. |
| gp2, gp3                                                                                                                              | io1, io2                                                                             | st1                                                                                                         | sc1                                                                                                            | estándar                       |

---
# EBS --- Uso general (SSD)

**El almacén de bloques de propósito general adecuado para la mayoría de las cargas de trabajo transaccionales.**

## Visión general
Los volúmenes de propósito general (gp) son los más adecuados para una amplia gama de cargas de trabajo (el caballo de batalla de talla única). El nombre de API para este tipo de volumen es gp (2 o 3).

## Tamaño de volumen e OPS
El tamaño del volumen gp varía de 1 GiB a 16TiB de tamaño. El volumen gp2 también se puede configurar para acomodar hasta 16,000 IOPS de rendimiento.

![[Pasted image 20260311165634.png]]

---
# EBS: IOP aprovisionadas (SSD)
**Volúmenes de SSD de alto rendimiento para aplicaciones de misión crítica.**
## Visión general
Los volúmenes de IOP aprovisionados (io) son los más adecuados para cargas de trabajo de misión crítica donde se requiere un rendimiento sostenido de IOPS. Estos tipos de volúmenes se utilizan con mayor frecuencia en soporte de cargas de trabajo de bases de datos.

## Tamaño de volumen e IOPS
El tamaño del volumen io varía de 4 GiB a 16 TiB de tamaño. Los volúmenes io1 e io2 también se pueden configurar para acomodar hasta 64,000 IOPS de rendimiento. El volumen más nuevo de io2 Block Express puede soportar hasta 256,000 IOPS (Esto es MUCHO IOPS).

![[Pasted image 20260311171203.png]]

---
# EBS: rendimiento optimizado (HDD)
**Volúmenes de HDD de bajo costo diseñados para cargas de trabajo de alto rendimiento y de acceso frecuente.**

## Visión general
Los volúmenes optimizados (st) son los más adecuados para cargas de trabajo de alto rendimiento y de acceso frecuente. Algunos ejemplos de casos de uso incluyen almacenes por volumen en soporte de data lakes o data warehouses.

## Tamaño de volumen e IOPS
El tamaño del volumen st1 varía de 125 GiB a 16 TiB de tamaño. El volumen st1 se puede configurar para soportar hasta 500 MiB/s por volumen.

![[Pasted image 20260311171650.png]]

---
# EBS - HDD en frío
**Volumen de disco duro de menor costo diseñado para cargas de trabajo a las que se accede con menos frecuencia.**

## Visión general
Los Volúmenes de disco duro en frío (sc) son los almacenes de bloques de menor costo que son los más adecuados para cargas de trabajo de datos a los que se accede con poca frecuencia. Algunos ejemplos de casos de uso incluyen servidores de archivos y almacenamiento orientado al rendimiento para datos a los que se accede con poca frecuencia.

## Tamaño de volumen e IOPS
El tamaño del volumen sc1 varía de 125 GiB a 16 TiB de tamaño. El volumen sc1 se puede configurar para soportar hasta 250 MiB/s por volumen.

![[Pasted image 20260311172213.png]]

--- 
# EBS - Magnético
**Solución de almacenamiento HDD de generación anterior.**

## Visión general
Los volúmenes magnéticos de EBS están respaldados por unidades de disco duro (HDD) y se pueden usar para cargas de trabajo con conjuntos de datos más pequeños donde se accede a los datos con poca frecuencia o cuando la consistencia del rendimiento no es de importancia primordial.

## Tamaño de volumen e IOPS
El tamaño del volumen magnético varía de 1 GiB a 1 TiB de tamaño. El volumen magnético se puede configurar para soportar 40 - 200 MiB/s por volumen.

![[Pasted image 20260311172646.png]]
