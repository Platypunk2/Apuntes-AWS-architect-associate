**Proporciona almacenamiento de objetos infinitamente escalable y altamente duradero en la nube de AWS**
Almacena objetos en recursos llamados Buckets. que pueden tener un tamaño de hasta 5TB, pero no hay límites totales para el # de objetos almacenados.

Diseñado para proporcionar 99.9999999% de durabilidad y 99.99% de disponibilidad.

Se ofrece a múltiples niveles de precios en función de la frecuencia con la que se necesitan los objetos y la velocidad a la que se requiere que se recuperen.

![[Pasted image 20260223143939.png]]

## Clases de Almacenamiento

Amazon S3 ofrece actualmente una gama de ofertas de clase de almacenamiento para satisfacer las necesidades de nuestros clientes.
Cada clase de almacenamiento está diseñada específicamente para diferentes patrones de acceso a los costos correspondientes.


> **Consejo de examen**
> Amazon S3 es un servicio importante para comprender las compensaciones y los casos de uso para cada clase de almacenamiento. Léelos detenidamente para conocer las pistas que podrían incluirse en la pregunta que resalten una clase de almacenamiento como opción.

![[Pasted image 20260223144825.png]]

![[Pasted image 20260223170437.png]]

# Políticas de bucket S3
**Una política de bucket que permite a un principal (ID de cuenta de AWS 111111111111) leer y escribir en el bucket "sample-bucket-reinvent"**

Tiene la misma sintaxis que la política de IAM pero agrega una declaración principal
```json
{
	"Versión": "2012-10-17",
	"Declaración": [
		{
			"Efecto": "Permitir",
			"Acción":[
				"s3:PutObject",
				"s3:GetObject"
			],
			"Recurso": "arn:aws:s3: :::/sample-bucket-reinvent/* ",
			"Principal": {"AWS":"111111111111"}
		}
	]	
}
```

Los principales válidos para sus políticas de bucket incluyen:
- Cuenta de AWS t usuario root
- Usuarios de IAM
- Usuarios federados (usando identidad web o federación SAML)
- Roles de IAM
- Sesiones de rol asumido
- Servicios de AWS
- Usuarios anónimos (públicos) - no recomendado

[awspolicygen.s3.amazonaws.com/policygen.html](https://awspolicygen.s3.amazonaws.com/policygen.html)

## S3 Transfer Acceleration (S3TA)
**Proporciona cargas y descargas de S3 más rápidas y a larga distancia**

S3 Transfer Acceleration (S3TA) reduce la variabilidad en el enrutamiento de Internet, la congestión y las velocidades que pueden afectar las transferencias y, lógicamente, acorta la distancia a S3 para aplicaciones remotas. S3TA mejora el rendimiento de las transferencias al enrutar el tráfico a través de las ubicaciones perimetrales distribuidas globalmente de Amazon CloudFront y a través de las redes troncales de AWS, y mediante la optimización en el protocolo de red.


> **Consejo de examen**
> S3TA ayuda a reducir la variabilidad de la red al acortar físicamente la distancia entre sus aplicaciones y AWS. Cualquier pregunta que hable de cargas de larga distancia o de encontrar formas de aumentar la transferencia de datos con S3, considere S3TA.

![[Pasted image 20260223181440.png]]


