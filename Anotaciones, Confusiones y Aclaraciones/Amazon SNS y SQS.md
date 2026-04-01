Pese a tener acrónimos parecidos, estos son dos servicios muy distintos.

# Amazon SNS
**El pregonero (Modelo Pub/Sub)**

SNS es un servicio de **Publicación/Suscrepción**. Cuando un mensaje llega a un "Topic" de SNS el servicio lo reenvía inmediatamente a todos los suscriptores (servidores, correos, funciones Lambda, etc.).
- **Comportamiento**
	"Dispara y olvida". Si un suscriptor no está conectado, podría perder el mensaje (a menos que haya políticas de reintento).
- **Empuje (Push)**
	SNS entrega el mensaje activamente a los destinatarios.

# Amazon SQS
**El buzón (Modelo de Cola)**

SQS es un servicio de **Colas de Mensajería**. Los mensajes se almacenan en una cola hasta que un componente (worker) los solicita, los procesa y luego los borra.
- **Comportamiento**
	Almacenamiento persistente. Si el procesador está ocupado o caído, el mensaje espera pacientemente en la cola.
- **Extracción (Pull/Polling)**
	Los receptores deben preguntar a SQS: "¿Tienes algo para mí?"

---

# Comparativa Directa

|**Característica**|**Amazon SNS**|**Amazon SQS**|
|---|---|---|
|**Modelo**|Pub/Sub (Uno a muchos)|Cola (Uno a uno)|
|**Entrega**|**Push:** El servicio envía el mensaje.|**Pull:** El cliente pide el mensaje.|
|**Persistencia**|No (el mensaje se esfuma tras enviarse).|Sí (se guarda hasta por 14 días).|
|**Consumidores**|Múltiples suscriptores reciben el mismo mensaje.|Solo un consumidor procesa un mensaje específico.|
|**Uso principal**|Notificaciones rápidas y Fan-out.|Desacoplamiento de sistemas y buffer de carga.|

---

# Cuando usar cada uno

### Usa SNS cuando:
- Necesites enviar el mismo mensaje a **múltiples destinos** (ej. avisar a facturación, inventario y envío cuando se completa una compra).
- Requieras respuestas inmediatas o notificaciones críticas (SMS, Email).
- Busques una arquitectura dirigida por eventos.

### Usa SQS cuando:
- Tengas procesos que tardan tiempo en ejecutarse (ej. procesar un video o generar un PDF).
- Necesites un **buffer** para absorber picos de tráfico sin que tu base de datos o servidor colapse.
- Garantizar que cada mensaje se procese exactamente una vez (o al menos una vez).