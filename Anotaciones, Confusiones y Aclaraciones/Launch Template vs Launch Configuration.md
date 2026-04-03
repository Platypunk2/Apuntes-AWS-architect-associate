**Ambos sirven para definir cómo se deben instanciar las máquinas virtuales (EC2) dentro de un grupo de Auto Scaling.**

---
## Tabla comparativa

|**Característica**|**Launch Template (Recomendado)**|**Launch Configuration (Legacy)**|
|---|---|---|
|**Versionamiento**|Permite múltiples versiones (v1, v2, v3).|No permite versiones; debes crear uno nuevo si algo cambia.|
|**Flexibilidad**|Puedes elegir subconjuntos de parámetros al lanzar.|Es inmutable; los parámetros son fijos una vez creado.|
|**Instancias Spot**|Permite combinar Instancias On-Demand y Spot.|Solo permite un tipo de compra por grupo.|
|**Arquitectura**|Soporta arquitecturas modernas (T3, graviton, etc.).|Limitado en tipos de instancia más recientes.|
|**Uso fuera de ASG**|Puede usarse para lanzar instancias individuales.|Solo funciona con Auto Scaling Groups (ASG).|

---

# ¿Por qué usar Launch Template?
**Launch Configuration es la tecnología antigua (legacy), mientras que Launch Template es la recomendación actual de AWS debido a su flexibilidad**

AWS ha dejado claro que el **Launch Template** es el estándar de oro por varias razones estratégicas:

1. **Gestión de Versiones:** Si necesitas actualizar el ID de la AMI o el tipo de instancia, simplemente creas una nueva versión del template. Puedes marcar  una versión como "Default" o revertir a una anterior fácilmente si algo falla.
2. **Parámetros heredados:** Puedes crear una plantilla base y que otras plantillas hereden configuraciones, lo que reduce errores manuales.
3. **Mejores prácticas de seguridad:** Permite aplicar políticas de IAM más granulares y soporta de forma nativa características nuevas como el uso de sistemas de archivos EFS o configuraciones avanzadas de red.
4. **Ahorro de costos:** Es la única forma de aprovechar las flotas mixtas en Auto Scaling, permitiéndote mezclar instancias de diferentes familias o utilizar capacidad sobrante (Spot) de forma inteligente.

Sólo puedes utilizar una plantilla de lanzamiento para aprovisionar capacidad en varios tipos de instancias utilizando tanto instancias bajo demanda como Instancias Spot para conseguir la escala, el rendimiento y el coste deseados.
Una plantilla de lanzamiento es similar a una configuración de lanzamiento, en el sentido de que especifica la información de configuración de la instancia, como el ID de la Imagen de Máquina de Amazon (AMI), el tipo de instancia, un par de claves, grupos de seguridad y otros parámetros que utilizas para lanzar instancias EC2. Además, definir una plantilla de lanzamiento en lugar de una configuración de lanzamiento te permite tener varias versiones de una plantilla.
Con las plantillas de lanzamiento, puedes aprovisionar capacidad en varios tipos de instancias utilizando tanto instancias bajo demanda como Instancias Spot para conseguir la escala, el rendimiento y el coste deseados. Por tanto, ésta es la opción correcta.