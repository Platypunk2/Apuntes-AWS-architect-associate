**Amazon FSx** es la solución de AWS para cuando necesitas sistemas de archivos especializados o de altísimo rendimiento que no encajan en el molde de [[Amazon Elastic File System (EFS)]].

En términos simples: **FSx es una familia de sistemas de archivos gestionados** que te permite ejecutar sistemas de archivos populares (como Windows File Server o Lustre) de forma nativa en la nube.

Dependiendo de qué tipo de sistema de archivos necesites, eliges una de estas variantes:

## FSx for Windows File Server
**Almacenamiento de archivos completamente administrado basado en Windows Server**

Amazon FSx para Windows File Server proporciona almacenamiento compartido totalmente administrado basado en Windows Server. Ofrece una amplia gama de capacidades de acceso a datos, administración de datos y administración.

- **Protocolo:** SMB
- **Uso ideal:** Compartir archivos en entornos Windows, Active Directory, aplicaciones de escritorio de Microsoft.
- **Por qué usarlo:** Si tienes una aplicación que requiere almacenamiento compatible con Windows (NTFS), EFS no te servirá; necesitas este FSx

> [!NOTE] Consejo de examen
> Preguntas relacionadas con la migración de archivos de servidores Windows a AWS, acelerando la adopción de migraciones mediante el uso de file systems híbridos con baja latencia.

![[Pasted image 20260303110002.png]]

## FSx for Lustre
**Diseñado para computación de alto rendimiento (HPC)**

- **Velocidad:** Puede procesar datos a cientos de GB/s con latencias sub-milisegundo.
- **Uso ideal:** Machine Learning, renderizado de video, simulaciones financieras.
- **Conexión con S3:** Puede leer datos directamente desde S3, procesarlos a velocidad extrema y guardar el resultado de vuelta en S3.

## FSx for NetApp ONTAP
**Para quienes ya usan almacenamiento NetApp en sus oficinas.**

- **Uso ideal:** Migraciones "híbridas" (parte en tu oficina, parte en AWS) sin cambiar la forma en que gestionas los datos.
- **Ventajas:** Incluye funciones avanzadas de NetApp como de duplicación y compresión de datos.

## FSx for Open ZFS
**Basado en el sistema de archivos de código abierto ZFS.**

- **Uso ideal:** Aplicaciones que necesitan mover grander cantidades de datos con copias de seguridad instantáneas (snapshots) y alta eficiencia.