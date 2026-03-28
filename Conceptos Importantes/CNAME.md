Un **CNAME** (Canonical Name o Nombre Canónico) es un tipo de registro en el sistema de nombres de dominio (DNS) que funciona como un **alias**. En lugar de apuntar un nombre directamente a una dirección IP, el CNAME apunta un nombre a **otro nombre**.
- **Registro A:** `miweb.com` -> `192.0.2.1` (Apunta a una IP).
- **Registro CNAME:** `base-datos-ventas.aws.com` -> `servidor-real-01.aws.com` (Apunta a otro nombre).

¿Por qué se usa en AWS RDS Multi-AZ?
