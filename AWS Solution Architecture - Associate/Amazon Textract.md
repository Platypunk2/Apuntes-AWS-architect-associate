**Servicio de machine learning (ML) que extrae automáticamente el texto, la escritura a mano, los elementos de diseño y los datos de la documentación escaneados.**

Amazon Textract es el servicio encargado de proveer funcionalidades de OCR.

>[!NOTE] ¿Qué es OCR?
>El **OCR (Optical Character Recognition)**, consiste en técnicas para identificar todos aquellos caracteres que se encuentran en una imagen. El OCR es ampliamente utilizado en **exámenes tipo test,** donde se identifica la respuesta que el usuario ha marcado. Pero si vamos más allá, podemos utilizar estos métodos para **digitalizar** cualquier tipo de **archivo que incluya texto**, ya sean imágenes o pdfs.


---
## Que se puede hacer con Textract

- Reconocimiento óptico de caracteres
	Detecta automáticamente texto y números en un documento.

- Extracción de formularios
	Permite detectar parejas clave-valor de un formulario. Dicho de otra forma, permite identificar el valor que contiene cada campo del formulario.

![[Pasted image 20260331173729.png]]

- Extracción de tablas
	Textract identifica el contenido que se estructura en tablas dentro de un documento, para que luego pueda ser subido a una base de datos relacional de forma sencilla.

- Reconocimiento de escritura
	Además de detectar texto escrito a máquina, Textract puede leer perfectamente aquellos caracteres escritos a mano.

- Bounding boxes
	Todos los datos extraídos de una imagen, proporcionan las coordenadas de su respectivo bounding box.

- Umbrales de confianza ajustables
	Al igual que con el bounding box, Textract también proporciona una puntuación de confianza, de manera que para tipos de datos en los que se tiene que estar realmente seguro de su identificación, pueda indicarse qué datos deben ser revisados por personas físicas.

