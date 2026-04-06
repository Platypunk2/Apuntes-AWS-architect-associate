![[Pasted image 20260405202130.png]]

# Lógica central
AWS sigue un principio muy simple: **todo está denegado por defecto**. El acceso sólo se concede cuando hay un `Allow` explícito, y siempre puede ser anulado por un `Deny` explícito. El orden de evaluación es:
1. **Deny explícito** -> termina la evaluación, acceso denegado
2. **SCP (si usas AWS Organizations)** -> actúa como techo; si la acción no está dentro de lo que el SCP permite, se deniega.
3. **Reource-based policies** -> si hay un `Allow`, puede conceder acceso directamente (incluso sin indentity policy)
4. **Identity-based policies** -> si hay un `Allow` aquí y no hay deny en ningún lado, se concede acceso.

---

# Ejemplo

``` json
{
  "Version": "2012-10-17",
  "Id": "EC2TerminationPolicy",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "ec2:Region": "us-west-1"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": "ec2:TerminateInstances",
      "Resource": "*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "10.200.200.0/24"
        }
      }
    }
  ]
}
```

En resumen los `Statement` son:
```json
Statement 1: Deny ec2:* donde región ≠ us-west-1
Statement 2: Allow ec2:TerminateInstances desde IP 10.200.200.0/24
```

**Escenario A:** Usuario en IP `10.200.200.100` intenta terminar una instancia en `us-east-1`

1. Se evalúa el Statement 1: la región es `us-east-1`, que NO es igual a `us-west-1` → la condición `StringNotEquals` es verdadera → **Deny aplica**
2. La evaluación termina. **Resultado: DENEGADO**, sin importar que el Statement 2 tenga un Allow

**Escenario B:** Usuario en IP `10.200.200.100` intenta terminar una instancia en `us-west-1`

1. Statement 1: la región ES `us-west-1` → `StringNotEquals` es **falsa** → el Deny NO aplica
2. Statement 2: la IP está en `10.200.200.0/24` → Allow aplica
3. **Resultado: PERMITIDO**

**Escenario C:** Usuario en IP `192.168.1.1` intenta terminar una instancia en `us-west-1`

1. Statement 1: no aplica (región correcta)
2. Statement 2: la IP no está en el rango → Allow no aplica
3. No hay ningún Allow que cubra esta acción → **Resultado: DENEGADO implícitamente**

---

# Ejemplo 2

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::mi-bucket/*"
    },
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::mi-bucket/*",
      "Condition": {
        "StringNotEquals": {
          "s3:prefix": ["backups/"]
        }
      }
    }
  ]
}
```

En resumen, puedes hacer todo en el bucket, pero no puedes borrar objetos a menos que estén en la carpeta `backups/`

- Intentas borrar `mi-bucket/logs/app.log` → Statement 1 da Allow, pero Statement 2 evalúa que el prefijo no es `backups/` → **Deny gana**
- Intentas borrar `mi-bucket/backups/2024.zip` → Statement 2 ve que el prefijo SÍ es `backups/` → condición falsa → Deny no aplica → Statement 1's Allow **queda vigente** → **PERMITIDO**
