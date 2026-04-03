**Tres herramientas para la transferencia de datos**

# AWS Data Sync
**Transferencia de datos eficiente**

Es un servicio de transferencia de datos **automatizado** que simplifica y acelera el movimiento de datos entre sistemas de almacenamiento on-premises y servicios de AWS (como S3, EFS o FSx).

## Cuándo usarlo

- **Migraciones masivas:** Cuando necesitas mover terabytes o petabytes de datos de forma recurrente.
- **Sincronización continua:** Para replicación de datos, recuperación ante desastres o flujos de trabajo de análisis de datos.
- **Facilidad de gestión:** Si no quieres escribir scripts para manejar reintentos, validación de integridad de datos o programación de tareas.

## Punto clave

DataSync es "inteligente". Solo transfiere los cambios (incremental) y utiliza protocolos optimizados para superar la latencia de la red.

A diferencia de storage gateway, datasync es primeramente un servicio cloud y no necesita el despliegue de un ambiente on-premise de hardware o aplicación.

---

# AWS Storage Gateway
**Integración de almacenamiento hibrido en la nube**

AWS Storage Gateway es el puente perfecto cuando no se quiere "mudar" los datos a la nube, sino que quieres que tus servidores locales sigan trabajando con ellos como si estuvieran en un disco duro de la oficina, pero con el respaldo de AWS.
## Cuándo usarlo

Se usa cuando se necesita un modelo de **almacenamiento hibrido**. Es decir, tus aplicaciones se quedan en tu oficina/centro de datos, pero el almacenamiento real está en AWS.

- **Baja latencia local:** Si tus aplicaciones necesitan acceder a los datos rápido, Storage Gateway guarda una "copia" (caché) de los archivos más usados localmente.
- **Protocolos estándar:** Si tu software antiguo solo entiende de carpetas compartidas (SMB/NFS) o discos iSCSI y no sabe hablar con la API de Amazon S3.
- **Sustitución de cintas (Tape Gateway):** Si quieres dejar de usar cintas físicas de backup y mandarlas a la nube de forma transparente.
- **Extensión de almacenamiento:** Cuando te quedas sin espacio en tus servidores locales y quieres usar la "nube infinita" sin comprar más hardware físico.

## Comparativa: DataSync vs. Storage Gateway

Esta es la confusión más común. La clave es: **¿Los datos se mueven o se comparten?**

|**Característica**|**AWS DataSync**|**AWS Storage Gateway**|
|---|---|---|
|**Propósito**|**Mover** datos (Migración).|**Conectar** datos (Híbrido).|
|**Uso**|Tareas puntuales o programadas para transferir archivos de A a B.|Acceso continuo y en tiempo real a los datos de la nube.|
|**Acceso local**|Una vez transferidos, los datos suelen borrarse del origen o quedar como copia.|Proporciona una unidad de red local que siempre está ahí.|
|**Ejemplo**|"Quiero mover 10TB de fotos a S3 para cerrar mi servidor viejo".|"Quiero que mi servidor de diseño use una carpeta compartida que guarde todo en S3".|

---

# S3 Multipart Upload
**La mejor opción de Amazon S3 para subir archivos grandes**

A diferencia de los otros dos servicios vistos, este no es un servicio independiente, sino una **característica de la API de Amazon S3** que permite subir un solo objeto como un conjunto de partes.
Divide el archivo en varias partes que se suben en paralelo, mejorando la eficiencia y reduciendo el tiempo de carga.
Soporta archivos de hasta 5TB.
Minimiza la pérdida de progreso en caso de fallos, ya que solo es necesario volver a subir las partes fallidas en lugar de todo el archivo.

## Cuándo usarlo

- **Archivos grandes:** Es **obligatorio** para archivos de más de 5GB, pero muy recomendado para cualquier archivo mayor a 100 MB.
- **Redes inestables:** Si falla la conexión, solo tienes que reintentar la subida de la "parte" afectada, no de todo el archivo.
- **Maximizar ancho de banda:** Permite subir partes en paralelo para terminar más rápido.

## Punto clave

Se usa a nivel de desarrollo o mediante la AWS CLI. Si usas la CLI (`aws s3 cp`), AWS gestiona el Multipart Upload de forma automática por ti.

La gran deferencia de está característica de S3 (Multipart Upload) y AWS DataSync es que, este último, se usa para mover grande volúmenes de datos entre entornos on-premise y AWS, pero no es ideal para cargas de archivos individuales en S3.

