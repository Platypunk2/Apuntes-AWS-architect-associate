**Una imagen de máquina de Amazon (AMI) es una imagen soportada y mantenida proporcionada por AWS que proporciona la información necesaria para lanzar una instancia.**

Todas las AMI se categorizan como respaldadas por Amazon EBS o respaldadas por almacén de instancias.

**AMI respaldada por Amazon EBS:**
El dispositivo raíz de una instancia lanzada desde la AMI es un volumen de Amazon Elastic Block Store (Amazon EBS) creado a partir de una instantánea de Amazon EBS.

**AMI respaldada en el almacén de instancias de Amazon:**
El dispositivo raíz de una instancia lanzada desde la AMI es un volumen de almacén de instancias creado a partir de una plantilla almacenada en Amazon S3.

![[Pasted image 20260305174754.png]]

## Cuándo usar una AMI
Debes especificar una AMI al lanzar una instancia. Puedes iniciar varias instancias desde una única AMI cuando necesites varias instancias con la misma configuración.

# Metadatos de instancia EC2
**Los metadatos de instancia son datos sobre tu instancia que puedes usar para configurar o administrar la instancia en ejecución**

## Cómo recuperar Metadatos de instancias
Debido a que los metadatos de tu instancia están disponibles desde la instancia en ejecución, no es necesario que utilice la consola de [[Amazon EC2]] ni la CLI de AWS. Esto puede ser útil cuando escribes scripts para ejecutarlos desde tu instancia. Por ejemplo, puedes acceder a la dirección IP local de su instancia desde los metadatos de la instancia para administrar una conexión a una aplicación externa.

## ¿A qué se puede acceder con los metadatos de instancia?
También puedes usar metadatos de instancia para acceder a los datos de usuario que especificó al lanzar tu instancia. Por ejemplo, puede especificar parámetros para configurar tu instancia, o incluir un script simple. Puedes crear AMIs genéricas y usar datos de usuario para modificar los archivos de configuración suministrados en el momento del lanzamiento.

![[Pasted image 20260305181400.png]]

