[[Amazon IAM - Identify and Access Management]]
La principal diferencia es que un **usuario IAM** representa a una persona o aplicación específica con credenciales permanentes (contraseña/ claves API), mientras que un **rol IAM** es un conjunto de permisos temporales sin credenciales fijas que pueden asumir usuarios, servicios o aplicaciones de forma segura. Los usuarios son para acceso a largo plazo, los roles para acceso delegado o temporal.

![[Pasted image 20260309180801.png]]

En el caso del grupo, esta es una colección de usuarios. El grupo no es una "identidad" en sí misma, sino una forma de gestionar permisos para muchas personas a la vez.

# Ejemplo
**"Papeles Pampa S.A."**, una empresa distribuidora de papel que decide digitalizar todo su inventario y facturación usando AWS.

### 1. El Grupo: "Departamento de Ventas"

La empresa tiene 10 vendedores. En lugar de configurar los permisos de cada uno, crean un **Grupo** llamado `Ventas`.

- **Permiso asignado al grupo:** Solo pueden ver (leer) la base de datos de los pedidos de papel.
- **Uso:** Si contratan a un vendedor nuevo, simplemente lo meten al grupo y automáticamente ya tiene acceso a lo que necesita sin configurar nada extra.

### 2. El Usuario: "Carlos_Admin"

Carlos es el jefe de sistemas de Papeles Pampa. Él tiene su propio **Usuario** de IAM con nombre y contraseña únicos.

- **Uso:** Carlos usa sus credenciales para entrar a la consola de AWS todas las mañanas. Como es un usuario con nombre y apellido, la empresa puede ver en los registros (logs) que fue **él** quien creó un nuevo servidor para la página web y no otra persona.

### 3. El Rol: "Acceso-al-Escáner"

Aquí es donde se pone interesante. Papeles Pampa tiene una **aplicación automática** que escanea las facturas físicas y las sube a una "nube" (un bucket de S3) en AWS.

- **El problema:** No quieres poner una contraseña fija dentro del código de la aplicación (porque es inseguro).
- **La solución (Rol):** Creas un **Rol** llamado `Escritor-de-Facturas`. La aplicación "asume" ese rol cuando necesita guardar un archivo.
- **Uso:** El servidor donde corre el programa "se pone el sombrero" de ese rol, guarda el PDF de la factura y listo. No hubo necesidad de usar contraseñas permanentes.