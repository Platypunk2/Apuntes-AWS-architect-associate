# Direccionamiento IPv4

La VPC ([[Amazon VPC]]) abarca dos rangos de direcciones IP:

- **10.0.0.0/16** → permite hasta 65,536 direcciones (10.0.0.0 – 10.0.255.255)
- **10.1.0.0/16** → un segundo bloque CIDR asociado
![[Pasted image 20260312091550.png]]

### Direcciones Reservadas por AWS

En **cada subred**, AWS reserva automáticamente 5 direcciones. Por ejemplo, en la subred `10.0.1.0/24`:

|Dirección|Uso|
|---|---|
|10.0.1.0|Dirección de red|
|10.0.1.1|Enrutador VPC (gateway)|
|10.0.1.2|Resolver DNS (Route 53)|
|10.0.1.3|Reservada para uso futuro|
|10.0.1.255|Difusión (broadcast)|

Esto significa que de 256 IPs disponibles en un /24, **solo 251 son utilizables**.

### Zonas de Disponibilidad (AZs)

Hay **dos zonas** para alta disponibilidad, cada una con:

**Subred Pública** (acceso a internet)

- AZ1: `10.0.1.0/24` → una instancia con IP pública `54.203.236.116` e IPs privadas `10.0.1.38` y `10.0.1.112`
- AZ2: `10.0.2.0/24` → instancia con **EIP (Elastic IP)** fija `52.34.234.27` e IPs privadas `10.0.2.200` y `10.0.2.47`

**Subred Privada** (sin acceso directo a internet)

- AZ1: `10.0.128.0/24`
- AZ2: `10.1.129.0/24`

# Direccionamiento IPv6

### Direcciones reservadas en IPv6

Similar a IPv4, AWS reserva algunas en cada subred:

|Dirección|Uso|
|---|---|
|`2001:db8:ec2:2:01::0`|Dirección de red|
|`2001:db8:ec2:2:01::1`|Enrutador VPC|
|`2001:db8:ec2:2:01::2`|Reservada|
|`2001:db8:ec2:2:01::3`|Reservada|
|`2001:db8:ec2:2:01::ffff:ffff:ffff:ffff`|Broadcast|

También aparecen dos especiales:

- `fd00:ec2::/32` → Reservado internamente por AWS
- `fe80::xff:fex:x/64` → Dirección de enlace local del enrutador VPC

![[Pasted image 20260312153538.png]]

### Las direcciones IPv6 en la imagen

**La VPC ahora tiene 3 bloques:**

```
10.0.0.0/16      ← IPv4 igual que antes
10.1.0.0/16      ← IPv4 igual que antes
2001:db8:ec2::/56 ← nuevo bloque IPv6
```

**Cada subred tiene su propio bloque /64:**

```
Subred pública AZ1:  2001:db8:ec2:01::/64
Subred pública AZ2:  2001:db8:ec2:02::/64
Subred privada AZ1:  2001:db8:ec2:80::/64
```


# Comparación IPv4 vs IPv6

|Característica|IPv4|IPv6|
|---|---|---|
|**Tamaño de dirección**|32 bits `10.0.1.38`|128 bits `2001:db8:ec2:1::1`|
|**Cantidad de IPs**|~4 mil millones|340 sextillones|
|**Bloque VPC**|`/16` (65k IPs)|`/56` (muchísimas más)|
|**Bloque subred**|`/24` (256 IPs)|`/64` (18 quintillones)|
|**IPs reservadas**|5 por subred|5 por subred (igual)|
|**IP pública**|Necesita EIP o IP dinámica separada|**Cada instancia ya tiene su propia IP pública IPv6**|
|**NAT Gateway**|Necesario para que privadas salgan a internet|**No necesario**, IPv6 es nativamente público|
|**Coexistencia**|—|Pueden coexistir (**Dual Stack**)|
## El punto más importante

En IPv4 las IPs privadas (`10.x.x.x`) **nunca son públicas**, por eso necesitas NAT o EIP para salir a internet.

En IPv6 **no existe ese concepto**, todas las direcciones son globalmente únicas y públicamente enrutables. La seguridad la manejas con Security Groups y no con "ocultarte detrás de un NAT".