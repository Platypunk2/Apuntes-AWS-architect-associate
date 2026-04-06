### Amazon S3 Standard

- **Disponibilidad:** 99.99% | **Durabilidad:** 99.999999999% (11 nueves)
- **Zonas de disponibilidad (AZ):** ≥ 3
- **Latencia:** milisegundos
- **Uso ideal:** Datos de acceso frecuente, sitios web, aplicaciones activas, big data
- **Costo:** El más alto en almacenamiento, sin costo por recuperación

---

### Amazon S3 Standard-IA (Infrequent Access)

- **Disponibilidad:** 99.9% | **Durabilidad:** 99.999999999% (11 nueves)
- **Zonas de disponibilidad:** ≥ 3
- **Latencia:** milisegundos
- **Uso ideal:** Backups, datos de recuperación ante desastres, archivos que se acceden ocasionalmente
- **Costo:** Más barato en almacenamiento que Standard, pero **cobra por cada GB recuperado**
- **Mínimo de almacenamiento:** 30 días y 128 KB por objeto

---

### Amazon S3 One Zone-IA

- **Disponibilidad:** 99.5% | **Durabilidad:** 99.999999999% (dentro de una sola AZ)
- **Zonas de disponibilidad:** Solo **1** ⚠️
- **Latencia:** milisegundos
- **Uso ideal:** Datos secundarios, thumbnails, datos que se pueden regenerar fácilmente
- **Costo:** ~20% más barato que Standard-IA, también cobra por recuperación
- **Riesgo:** Si la AZ falla o se destruye, **los datos se pierden**

---

## Resumen comparativo

|Característica|Standard|Standard-IA|One Zone-IA|
|---|---|---|---|
|AZs|≥ 3|≥ 3|1|
|Disponibilidad|99.99%|99.9%|99.5%|
|Costo almacenamiento|$$$|$$|$|
|Costo recuperación|✗|✓|✓|
|Acceso frecuente|✅|❌|❌|
|Resiliencia a falla de AZ|✅|✅|❌|

## Regla general para elegir

- **Acceso frecuente** → **Standard**
- **Acceso poco frecuente + datos críticos** → **Standard-IA**
- **Acceso poco frecuente + datos reproducibles** → **One Zone-IA**
