**obtener métricas del sistema operativo en tiempo real**

Es una funcionalidad que permite obtener **métricas del sistema operativo en tiempo real** con mayor granularidad que el monitoreo estándar de CloudWatch, recopilando datos directamente desde un **agente instalado en la instancia**, no desde el hipervisor.

### Diferencia clave con el monitoreo estándar

|                           | Monitoreo Estándar | Enhanced Monitoring            |
| ------------------------- | ------------------ | ------------------------------ |
| **Fuente de métricas**    | Hipervisor         | Agente en el SO                |
| **Granularidad**          | 1 minuto           | 1, 5, 10, 15, 30 o 60 segundos |
| **Métricas del SO**       | Limitadas          | Detalladas                     |
| **Costo**                 | Incluido           | Costo adicional                |
| **Procesos individuales** | ❌                  | ✅                              |

## Servicios de AWS donde está disponible

### 1. Amazon RDS

Es donde más se usa. Permite ver métricas del SO de la instancia de base de datos:

- CPU por proceso
- Memoria libre / usada
- I/O de disco
- Procesos activos del SO
- Swap usage

> Soportado en: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora

---

### 2. Amazon Aurora

Al ser parte de RDS, también tiene Enhanced Monitoring con las mismas capacidades, más métricas específicas del motor Aurora.

---

### 3. Amazon EC2 (mediante CloudWatch Agent)

==En EC2 no se llama exactamente "Enhanced Monitoring", sino que se habilita instalando el **CloudWatch Agent**, que cumple la misma función: recolectar métricas del SO desde adentro de la instancia.==

Lo que agrega sobre el monitoreo básico:

- Uso de memoria (RAM) — que CloudWatch básico **no incluye por defecto**
- Espacio en disco por partición
- Métricas de procesos individuales

---

### 4. Amazon ElastiCache

Tiene Enhanced Monitoring para ver métricas internas del nodo de caché:

- Uso de CPU del motor (separado del CPU del SO)
- Memoria usada por el motor Redis o Memcached
- Conexiones activas

---

### Resumen de disponibilidad

|Servicio|Disponible|Nombre que usa|
|---|---|---|
|**RDS**|✅|Enhanced Monitoring|
|**Aurora**|✅|Enhanced Monitoring|
|**EC2**|✅|CloudWatch Agent|
|**ElastiCache**|✅|Enhanced Monitoring|
|**Redshift**|✅|Enhanced Monitoring (nodos)|

---

### Cuándo activarlo

- Cuando necesitas diagnosticar **problemas de performance** a nivel de SO
- Cuando el monitoreo estándar no es suficientemente granular
- Cuando quieres ver **qué proceso específico** está consumiendo recursos en RDS
- Cuando necesitas métricas de **RAM en EC2** (no disponible en CloudWatch básico)