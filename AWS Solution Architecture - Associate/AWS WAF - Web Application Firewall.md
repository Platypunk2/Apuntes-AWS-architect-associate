**AWS WAF es un firewall de aplicaciones web que ayuda a proteger las aplicaciones web de los ataques al permitirle configurar reglas que permiten, bloquean o monitorean (cuentan) solicitudes web en función de las condiciones que defina.**

## Opciones de implementación
- En Amazon CloudFront ([[Amazon CloudFront]]) como parte de CDN.
- En Application Load Balancer frente a servidores web y origen que se ejecutan en EC2.
- Amazon API Gateway para API REST.
- AWS AppSync para API de GraphQL

# Concepto clave
AWS WAF le brinda control sobre cómo el tráfico llega a sus aplicaciones al permitirle crear reglas de seguridad que controlan el tráfico de bots y bloquean patrones de ataque comunes, como inyección SQL o secuencias de comandos entre sitios.

Paga solo por lo que uses, precios basados en cuántas reglas se implementan y cuántas solicitudes recibe la aplicación.

![[Pasted image 20260311110133.png]]

