Anycast es un método de enrutamiento donde múltiples servidores en distintas ubicaciones geográficas comparten la misma dirección IP. El tráfico de red se dirige automáticamente al servidor más cercano (topológicamente) al usuario, lo que reduce la latencia, mejora la velocidad y aumenta la disponibilidad ante ataques DDoS

![[Pasted image 20260226182143.png]]

El proceso de selección para elegir un centro de datos concreto suele estar optimizado para reducir la latencia al seleccionar el centro de datos que esté más cerca del solicitante. 

## ¿Por qué utilizar una red Anycast?

Si se hacen muchas solicitudes simultáneamente al mismo **servidor de origen**, el servidor puede verse desbordado por el tráfico y ser incapaz de responder eficazmente a las a las solicitudes entrantes adicionales. Con una red Anycast, en lugar de que un servidor de origen se lleve la peor parte del tráfico, la carga puede repartirse entre otros centros de datos disponibles, cada uno de los cuales contará con servidores capaces de procesar y responder a la solicitud entrante. Este método de **enrutamiento** puede impedir que un servidor de origen amplíe su capacidad y previene interrupciones del servicio a los clientes que solicitan contenidos al servidor de origen.

## El concepto: La "Tienda de Conveniencia"

Imagina una cadena de cafeterías. Todas tienen el mismo nombre y venden el mismo menú. Si buscas en tu GPS "Café Express", el mapa no te envía a la sede central, sino a la que esté **más cerca de tu ubicación actual**.

En redes, Anycast hace lo mismo:

- Varios servidores en distintas partes del mundo anuncian la **misma dirección IP**.
- Los routers de Internet eligen el camino más corto (basado en el protocolo BGP).
- El usuario se conecta al servidor que esté "más cerca" en términos de saltos de red.

## ¿Se replican los servicios automáticamente?

**No.** El protocolo Anycast no sabe qué hay dentro del servidor. Él solo dice: _"Si buscas esta IP, yo soy un camino para llegar"_.

La responsabilidad de que el contenido sea el mismo recae en el administrador del sistema. Si quieres que todos los servidores tengan la misma web o el mismo servicio:

1. **Tú debes copiar los datos:** Tienes que usar herramientas externas (como `rsync`, replicación de bases de datos o contenedores) para que todos los nodos tengan la misma información.

2. **Configuración idéntica:** Debes instalar el mismo software en cada servidor para que, sin importar a cuál llegue el usuario, la respuesta sea la misma.

## ¿Es un reparto de servicios (Load Balancing)?

Es un tipo de balanceo, pero a nivel **geográfico y de red**, no de capacidad:

- **Anycast:** Reparte el tráfico según la **distancia**. Si un servidor en Brasil y otro en España tienen la misma IP, los usuarios de Sudamérica irán a Brasil y los de Europa a España.
- **Unicast + Load Balancer:** Recibe todo el tráfico en un solo punto y luego lo reparte internamente según qué servidor está menos ocupado.


> [!NOTE] Dato clave
> Si un servidor Anycast se cae, los routers simplemente dejan de ver ese camino y envían al usuario al siguiente servidor más cercano. Esto lo hace excelente para servicios de **DNS** y **CDNs** (como Cloudflare o Google).


