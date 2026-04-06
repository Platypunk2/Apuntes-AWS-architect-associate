1. Según la política de terminación por defecto, se da la primera prioridad a cualquier estrategia de asignación de instancias Bajo Demanda frente a Instancias Spot.
2. La siguiente prioridad es considerar cualquier instancia con la plantilla de lanzamiento más antigua, a menos que exista una instancia que utilice una configuración de lanzamiento.
3. A continuación, debes considerar cualquier instancia que tenga la configuración de lanzamiento más antigua.

# Ejemplo

> Amazon EC2 Auto Scaling necesita terminar una instancia de la zona de disponibilidad (AZ) us-east-1a ya que tiene el mayor número de instancias entre las AZs que se utilizan actualmente. Hay 4 instancias en la AZ us-east-1a así: La Instancia A tiene la plantilla de lanzamiento más antigua, la Instancia B tiene la configuración de lanzamiento más antigua, la Instancia C tiene la configuración de lanzamiento más reciente y la Instancia D es la más próxima a la siguiente hora de facturación. ¿Cuál de las siguientes instancias se terminaría según la política de terminación por defecto?

**R:**
Instancia B 
Según la política de terminación por defecto, se da la primera prioridad a cualquier estrategia de asignación de instancias Bajo Demanda frente a Instancias Spot. Como no se ha proporcionado tal información para el caso de uso dado, este criterio puede ignorarse. La siguiente prioridad es considerar cualquier instancia con la plantilla de lanzamiento más antigua, a menos que exista una instancia que utilice una configuración de lanzamiento. Así que esto descarta la Instancia A. A continuación, debes considerar cualquier instancia que tenga la configuración de lanzamiento más antigua. Esto implica que la Instancia B será seleccionada para la terminación y que la Instancia C también será descartada, ya que tiene la configuración de lanzamiento más reciente. La Instancia D, que es la más próxima a la siguiente hora de facturación, no se selecciona porque este criterio es el último en el orden de prioridad.

