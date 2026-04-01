**Resolver problemas de escalabilidad y disponibilidad**

Estos dos servicios resuelven problemas de escalabilidad y disponibilidad en niveles distintos.

La diferencia fundamental es el alcance geográfico.

---

## RDS Multi-AZ
**La Llanta de Repuesto (Alta Disponibilidad)**

Cuando activas Multi-AZ en una RDS tradicional, AWS crea una copia exacta de tu base de datos en una **Zona de Disponibilidad (AZ)** distinta dentro de la **misma región.**

- **Cómo funciona:** La replicación es **síncrona.** Cuando escribes un dato, se guarda en ambas zonas antes de confirmar que se completó.

- **Failover:** Si la instancia principal falla, RDS cambia automáticamente a la secundaria (tarda 1-2 minutos) y no tienes que cambiar tu código, ya que el nombre del servidor (endpoint) sigue siendo el mismo.

- **Propósito:** Sobrevivir a fallos de hardware o caídas de una zona de datos específica.

## Aurora Global Database
**El Espejo Mundial (Disponibilidad Global)**

Aurora Global permite que una sola base de datos se extienda a través de **múltiples regiones** (ej. una en EE.UU. y otra en Europa).

- **Cómo funciona:** La replicación es **asíncrona** y extremadamente rápida (generalmente menos de 1 segundo de latencia). Utiliza el hardware de almacenamiento de Aurora para enviar datos sin cargar la CPU de la base de datos.

- **Lecturas locales:** Puedes tener hasta 16 réplicas en cada región secundaria, lo que permite que los usuarios en Europa lean datos con latencia mínima, aunque la base de datos principal esté en EE.UU.

- **Propósito:** Recuperación ante desastres a nivel regional (DR) y lecturas globales de baja latencia.

--- 

|**Característica**|**RDS Multi-AZ**|**Aurora Global Database**|
|---|---|---|
|**Alcance**|Una sola Región (múltiples zonas).|Múltiples Regiones.|
|**Tipo de Replicación**|Síncrona (máxima consistencia).|Asíncrona (mínima latencia).|
|**Uso de la secundaria**|Es solo un "respaldo" (no puedes leer de ella).|Puedes usar las secundarias para **lectura**.|
|**Objetivo**|Alta Disponibilidad (HA).|Recuperación ante Desastres (DR) y Lectura Global.|
|**Costo**|Aproximadamente el doble (pagas 2 instancias).|Mayor (pagas instancias + transferencia de datos entre regiones).|

