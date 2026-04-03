
Severless es un modelo de nube donde el proveedor gestiona automáticamente la infraestructura, permitiendo a los desarrolladores enfocarse solo en el código. Se caracteriza por el escalado automático, pago por uso (recursos consumidos) y ejecución basadas en eventos, Ideal para microservicios y APIs eficientes.
En un modelo tradicional, tú alquilas una "parcela" (un servidor) y te encargas de regar el pasto, arreglar la cerca y pagar la luz, sin importar si hay gente viviendo ahí o no. En **Serverless**, es como pedir un café: tú solo pides lo que necesitas, lo consumes y pagas exactamente por esa taza, sin preocuparte de quién compró la cafetera o quién limpia el local.

Para que un servicio sea considerado "Serverless", generalmente cumple con estas cuatro características:

1. **Sin administración de infraestructura:** No configuras sistemas operativos ni instalas parches de seguridad.
2. **Escalado automático:** El servicio crece o se detiene solo según la demanda (de 0 a mil usuarios en segundos).
3. **Pago por uso:** Si nadie usa tu aplicación, el costo es **cero**. Pagas por milisegundos de ejecución o cantidad de datos.
4. **Alta disponibilidad:** La tolerancia a fallos viene integrada por el proveedor.


## Ejemplos de Servicios AWS

Amazon Web Services es el pionero en esta área. Aquí tienes los más importantes divididos por categorías:

- **Cómputo:** **AWS Lambda**. Es el rey del serverless. Subes tu código (Python, Node.js, etc.) y se ejecuta solo cuando ocurre un evento (como subir una foto o hacer clic en un botón).
- **Bases de Datos:** **Amazon DynamoDB**. Una base de datos NoSQL que escala automáticamente para manejar millones de solicitudes sin que tengas que gestionar clusters.
- **Almacenamiento:** **Amazon S3**. Guardas archivos sin preocuparte por el espacio en disco; escala de forma infinita.
- **Integración:** **Amazon EventBridge** o **SNS/SQS**. Para comunicar diferentes partes de tu app mediante mensajes y eventos.