**AWS KMS es un servicio administrado que le facilita la creación y el control de las claves criptográficas que se utilizan para proteger tus datos.**

AWS KMS es un servicio seguro y resiliente que utiliza módulos de seguridad de hardware que han sido validados bajo FIPS 140-2, o están en proceso de ser validados, para proteger sus claves.

## ¿Qué aporta?
Las claves KMS son el recurso principal en AWS KMS. Puedes usar una clave KMS para cifrar, descifrar y volver a cifrar datos.

KMS proporciona la capacidad de crear claves de cifrado simétricas y asimétricas.
![[Pasted image 20260305183306.png]]

## Tipos de claves KMS
**Los CMK ([[CMK - Customer Master Key]]) se pueden dividir en dos tipos generales: administrados por AWS y administrado por el cliente.**

<u>Una CMK administrada por AWS se crea cuando eliges habilitar el cifrado del lado del servidor de un recurso de AWS bajo la CMK administrada por AWS para ese servicio por primera vez (por ejemplo, SSE-KMS).</u> Una CMK administrada por AWS solo se puede utilizar para proteger los recursos dentro del servicio específico de AWS para el que se ha creado. No proporciona el nivel de control granular que proporciona una CMK administrada por el cliente.
Para un mayor control, una práctica recomendada es utilizar una CMK administrada por el cliente en todos los servicios de AWS compatibles y en sus aplicaciones. Un CMK administrado por el cliente se crea bajo petición y debe configurarse en función de su caso de uso explícito.

![[Pasted image 20260309155422.png]]