**Dos características de AWS para aumentar la seguridad en su VPC: grupos de seguridad y ACL de red.**

**Grupos de seguridad:** los grupos de seguridad actúa como un firewall para las instancias de Amazon EC2 asociadas, controlando tanto el tráfico entrante como saliente a nivel de instancia. Cuando inicias una instancia, puedes asociarla con uno o más grupos de seguridad que hayas creado. Si no especificas un grupo de seguridad cuando inicia una instancia, la instancia se asocia automáticamente con el grupo de seguridad predeterminado para la VPC.

**Listas de control de acceso a la red (ACL):** Las ACL de red actúan como un firewall para las subredes asociadas, controlando tanto el tráfico entrante como saliente a nivel de subred.


> [!NOTE] Temas clave del examen
> - Las ACL de red son sin estado.
> - Los grupos de seguridad tienen estado.

**Grupos de Seguridad: Con Estado (Stateful)**
Cuando decimos que un Grupo de Seguridad tiene estado, significa que si permites el tráfico de entrada, el tráfico de salida de respuesta se permite **automáticamente**, sin importar las reglas de salida.
- **El "Portero Inteligente:"** Imagina un portero que anota quién entra. Si te dejó pasar para entrar al edificio, te deja salir automáticamente porque ya te validó al entrar.
- **Funcionamiento:** Si abres el puerto 80 (HTTP) de entrada, la instancia puede responder al cliente por cualquier puerto efímero de salida sin que tengas que configurar nada extra.

**NACL (Network ACL): Sin Estado (Stateless)**
Las ACL de red no guardan memoria de las conexiones. Tratan cada paquete de datos como un evento totalmente nuevo y aislado.
- **El "Portero con Amnesia":** Este portero no recuerda a nadie. Si entraste, bien, pero cuando intentes salir, te pedirá tus credenciales de nuevo. Si no hay una regla específica que diga "Permitir Salida", te quedarás encerrado.
- **Funcionamiento:** Si permites tráfico de entrada en el puerto 443 (HTTPS), **debes** crear manualmente una regla de salida para permitir la respuesta. De lo contrario, el paquete de respuesta será descartado al intentar salir de la subred.

## Mejores Prácticas

- Utiliza ACL de red para controlar el acceso a sus subredes y utiliza grupos de seguridad para controlar el tráfico a instancias EC2 en sus subredes.
- Cuando agregas subredes a su VPC, elige varias zonas de disponibilidad (AZ) para asegurarte que los recursos alojados en esas subredes estén altamente disponibles. Una AZ es uno o más centros de datos con alimentación redundante, redes y conectividad en una región de AWS. Los AZ le permiten hacer que las aplicaciones de producción sean altamente disponibles, tolerantes a fallas y escalables.

![[Pasted image 20260226164231.png]]

# Grupos de seguridad de AWS
**Actúa como un firewall virtual, controlando el tráfico permitido para llegar y salir de los recursos asociados**

## Componentes del grupo de seguridad
- Nombre
- Descripción
- Protocolo
- Rango de puertos
- Dirección IP
- Rango IP
- Nombre del grupo de seguridad.

## Otros conceptos clave
- Sólo se pueden especificar reglas de permitir, pero no reglas de denegación
- Cuando creas por primera vez un grupo de seguridad, no tiene reglas de entrada. Por lo tanto, no se permite el tráfico entrante hasta que agregues reglas de entrada al grupo de seguridad.
- Las VPC predeterminadas y las VPC que crees vienen con un grupo de seguridad predeterminado. No se puede eliminar un grupo de seguridad predeterminado.
![[Pasted image 20260226173857.png]]

# Listas de controles de acceso a la red (NACL) de AWS
**Capa opcional de seguridad para VPC que actúa como firewall que controla el tráfico dentro y fuera de las subredes**

## Propósito

Puedes configurar ACL de red con reglas similares a tus grupos de seguridad para agregar una capa adicional de seguridad a tu VPC.

## Componentes clave

Una ACL de red tiene reglas de entrada y salida separadas, y cada regla puede permitir o denegar el tráfico.

Una ACL de red contiene una lista numerada de reglas. AWS evalúa las reglas. AWS evalúa las reglas en orden, comenzando por la regla numerada más baja, para determinar si el tráfico está permitido dentro o fuera de cualquier subred asociada con la ACL de la red.

![[Pasted image 20260226175953.png]]

# Grupos de Seguridad frente a NACL
**Guía resumida para diferenciar las capacidades.**

![[Pasted image 20260226180248.png]]

# Diagrama de grupos de seguridad y NACL
**Enfoque de seguridad en capas para una defensa adicional**

![[Pasted image 20260226180454.png]]
