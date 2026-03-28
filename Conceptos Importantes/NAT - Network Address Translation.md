Un NAT (Network Address Translation o Traducción de Direcciones de Red) es una tecnología utilizada por los routers para mapear múltiples dispositivos en una red privada (LAN) a una única dirección IP pública para acceder a Internet.
![[Pasted image 20260225104603.png]]

### Ejemplo de NAT en una casa

Supongamos que en tu casa tienes:

- Tu **laptop**
- Tu **celular**
- Tu **Smart TV**

Todos están conectados al mismo **router WiFi**.

#### 1️⃣ Direcciones IP privadas dentro de la casa (LAN)

Dentro de la red local, cada dispositivo tiene una **IP privada**:

- Laptop → `192.168.1.10`
- Celular → `192.168.1.11`
- Smart TV → `192.168.1.12`

Estas IP **solo funcionan dentro de tu red local**.

#### 2️⃣ Dirección IP pública

Tu proveedor de internet te da **una sola IP pública**, por ejemplo:

- Router → `200.55.120.30`

Esta es la **única IP que Internet ve**.

#### 3️⃣ Cuando un dispositivo accede a Internet

Supongamos que tu **laptop (192.168.1.10)** entra a Google.

El proceso sería:

1. Laptop envía una petición a Google:
    
    Origen: 192.168.1.10  
    Destino: google.com
    
2. El **router aplica NAT** y cambia la dirección de origen:
    
    Origen: 200.55.120.30  
    Destino: google.com
    
3. Google responde a:
    
    200.55.120.30
    
4. El router revisa su **tabla NAT** y sabe que esa respuesta corresponde a:
    
    192.168.1.10
    
5. Entonces envía la respuesta a tu laptop.

#### 4️⃣ Si otro dispositivo también usa Internet

Por ejemplo tu celular (`192.168.1.11`) entra a YouTube.

El router **también usa la misma IP pública**, pero distingue las conexiones usando **puertos**.

Ejemplo de tabla NAT del router:

|IP privada|Puerto|IP pública|Puerto externo|
|---|---|---|---|
|192.168.1.10|5001|200.55.120.30|30001|
|192.168.1.11|5002|200.55.120.30|30002|

Así **muchos dispositivos comparten una sola IP pública**.

---

💡 **Idea clave:**  
NAT permite que **muchos dispositivos de una red privada usen una sola dirección IP pública para acceder a Internet**, lo que ahorra direcciones IPv4.