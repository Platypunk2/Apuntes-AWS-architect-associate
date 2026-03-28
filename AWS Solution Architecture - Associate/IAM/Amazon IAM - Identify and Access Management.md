**Políticas y tecnologías utilizadas para garantizar el acceso adecuado a los recursos tecnológicos**

AWS IAM proporciona un control de acceso preciso en todo AWS. Con IAM, se puede especificar quién puede acceder a qué servicios y recursos, bajo qué condiciones.

## Políticas de IAM
Las políticas de IAM permiten administrar permisos para la fuerza laboral y sistemas para garantizar el acceso con el menor privilegio.

Cuando se habla del "principio de menor privilegio", se refiere que a un usuario/recurso se le debe otorgar la menor cantidad de permisos o privilegios necesarios para completar su rol de trabajo.
==Si un usuario no necesita un derecho de acceso, no debe tener ese derecho de acceso.==
**Este es un componente principal en las prácticas recomendadas de seguridad de AWS y en la comprensión de los accesos.**

> **Pregunta de examen**
> El examen a veces te pedirá que evalúes permisos/documentos de política en respuesta a proporcionar acceso a un usuario. Estas preguntas suponen que entiendes el principio del menor privilegio.

[[Políticas (Más a Detalle)]]

# Usuarios y grupos de IAM
**Los componentes básicos de AWS Identity and Access Managment**

## Usuarios de IAM
Un usuario de IAM es una entidad que se crea en AWS pare representar a la persona, o aplicación, que la utiliza para interactuar con AWS.

## Grupos IAM
Un grupo IAM es una colección de usuarios de IAM. Los grupos de usuarios le permiten especificar permisos para varios usuarios, lo que puede facilitar la administración de los permisos para esos usuarios.

Ejemplo: Podrías tener un grupo de usuarios llamado Administradores y darle a ese grupo de usuarios permisos de administrador típicos.

![[Pasted image 20260222185820.png]]
## AWS Organizations
**Un servicio de administración de cuentas que permite la consolidación y organización de cuentas**

Una forma de consolidar cuentas, asignar permisos a las unidades organizacionales y automatizar la incorporación de nuevos miembros del equipo en función de la función del trabajo.

### Componentes
- **Organizaciones:** una entidad creada para consolidar las cuentas de AWS.
- **Raíz:** contenedor principal para todas las cuentas de su organización
- **Unidad Organizacional (OU)** - Un contenedor para cuentas dentro de una raíz. Una unidad organizacional también puede contener otras unidades organizacionales.
- **Cuenta:** una cuenta en una organización es una cuenta estándar de AWS que contiene recursos e identidades de AWS.
- **Política de control de servicios (SCP)** - Una política que especifica los servicios y acciones que los usuarios y roles pueden usar en las cuentas a las que afecta la SCP.
- **Etiquetado:** prácticas recomendadas para que sus unidades organizativas realicen un seguimiento de sus cuentas y recursos de AWS. Esto ayuda con un monitoreo y registro más granulares de su entorno de AWS.
