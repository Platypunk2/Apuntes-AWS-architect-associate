Un Host Bastión, o un servidor de salto (jump box), es un servidor reforzado y altamente seguro situado en el perímetro de una red (generalmente en una subred pública o DMZ). Actúa como punto de entrada único y seguro para que los administradores accedan a redes privadas, controlando el tráfico y limitando la superficie de ataque o recursos críticos.

![[Pasted image 20260309161416.png]]

<iframe title="¿Qué es un Bastion Host? - Guía de Acceso Seguro (Jump Server &amp; SSH)" src="https://www.youtube.com/embed/OR2OGI7Amcw?feature=oembed" height="113" width="200" allowfullscreen="" allow="fullscreen" style="aspect-ratio: 1.76991 / 1; width: 100%; height: 100%;"></iframe>

Internet -> Bastion -> Private Network 

## Reglas de oro para un bastión
- Whitelist IP
	Permite solo tu IP de oficina/casa.
- Claves SSH (sin passwords)
	Usa .pem o Ed25519 keys. Prohibido passwords
- Auditoria de Logs
	Monitorea quién entra y qué hace.

## Bastion Host vs VPN

Imagina que un **Bastion Host** es un "recepcionista" que custodia una puerta específica, mientras que una **VPN** es un "túnel privado" que te permite entrar al edificio completo y moverte por los pasillos.

La elección depende de si solo necesitas realizar tareas de mantenimiento en servidores específicos o si necesitas que tu computadora se comporte como si estuviera físicamente en la oficina.

### Comparativa rápida

|**Característica**|**Bastion Host (Jump Box)**|**VPN (Red Privada Virtual)**|
|---|---|---|
|**Objetivo**|Acceso administrativo (SSH/RDP) a servidores.|Conectividad total a la red para cualquier app.|
|**Alcance**|**Granular**: Accedes a un servidor a la vez.|**Amplio**: Te unes a toda la subred/red.|
|**Software**|Generalmente ninguno (usa terminal o navegador).|Requiere un cliente (AnyConnect, OpenVPN, etc.).|
|**Complejidad**|Simple para pocos usuarios.|Mayor carga de gestión y escalabilidad.|
|**Visibilidad**|Expuesto a internet (pero muy protegido).|Suele estar oculto detrás de un firewall.|
