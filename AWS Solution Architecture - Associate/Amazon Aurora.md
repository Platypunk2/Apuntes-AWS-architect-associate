**Base de datos relacional compatible con MySQL y PostgreSQL, construida para la nube**

Es el hijo "prodigio" de AWS. Es una base de datos **rediseñada específicamente para la nube**, compatible con MySQL y PostgreSQL.

Al utilizar una base de datos global de Amazon Aurora, puedes ejecutar tus aplicaciones distribuidas globalmente mediante una única base de datos Aurora que abarca varias regiones de AWS.


> [!NOTE] Condejo de examen 
> Las preguntas que hablan de migraciones de bases de datos MySQL/PostgreSQL a la nube que requieren alta disponibilidad, resiliencia o múltiples AZ, ¡Aurora debería ser tu primer pensamiento!

- **Rendimiento:**
	AWS afirma que es hasta **5 veces más rápido** que MySQL estándar y **3 veces más rápido** que PostgreSQL.
- **Almacenamiento Inteligente:**
	No usa volúmenes tradicionales. Los datos se replican automáticamente en **6 copias a través de 3 zonas de disponibilidad.** Si un disco falla, ni te enteras.
- **Replicas de Lectura:**
	Puedes tener hasta 15 réplicas y, a diferencia de [[Amazon RDS (Relational Database Service)]], estas sirven para lectura activa y para recuperación ante fallos (failover) en segundos.
- **Auto-scaling de almacenamiento:**
	El almacenamiento crece solo (hasta 128TB actualmente) según lo necesites; no tienes que pre-configurarlo.
	
![[Pasted image 20260303161002.png]]


## Resiliencia de Aurora

Aurora mantiene seis copias de datos, dos copias en cada Zona de Disponibilidad (3 AZ). Esto protege contra fallas AZ +1.

Las réplicas principales y demás réplicas apuntan al mismo almacenamiento subyacente.

## Ventajas
- Lecturas globales con latencia local.
- Clústeres de base de datos Aurora secundarios escalables.
- Replicación rápida de clústeres de base de datos Aurora primarios a secundarios.
- Recuperación de interrupciones en toda la región.

![[Pasted image 20260303161951.png]]
