**Puedes cifrar tanto los volúmenes de arranque como de datos de una instancia EC2 ([[Amazon EC2]])**

## Concepto clave
AL crear un volumen EBS cifrado y adjuntarlo a un tipo de instancia admitido, **se cifran los siguientes tipos de datos:**
- **Datos en reposo** dentro del volumen.
- Todos los datos **se mueven entre** el volumen y la instancia.
- Todas las **instantáneas creadas a** partir del volumen.
- Todos los **volúmenes** creados a partir de esas instantáneas.

## Otras consideraciones
Utiliza el cifrado de Amazon EBS como una solución de cifrado directa para tus recursos de EBS asociados con sus instancias EC2.

Cuando creas un recurso EBS cifrado, se cifra mediante la clave KMS ([[AWS Key Management Service (KMS)]]) predeterminada de tu cuenta para el cifrado de EBS, a menos que especifiques una clave administrada por el cliente diferente en los parámetros de creación de volumen o la asignación de dispositivos de bloque para la AMI o la instancia.

El uso de su propia clave KMS te brinda más flexibilidad, incluida la capacidad de crear, rotar y deshabilitar claves KMS.