**Datos e información para monitorear sus aplicaciones, responder a los cambios de rendimiento en todo el sistema, optimizar la utilización de recursos y obtener una visión unificada del estado operativo.**

## Monitoreo de infraestructura
Supervisa métricas y registros clave, visualiza las aplicaciones e infraestructura, crea alarmas y correlaciona métricas y registros.

## Escalabilidad
Toma medidas automáticamente para habilitar Amazon EC2 Auto Scaling o detener una instancia, por ejemplo, para que puedas automatizar la capacidad y la planificación de recursos.

![[Pasted image 20260312181046.png]]

---
**CloudWatch es una plataforma completa de observabilidad para AWS**
## Métricas (CloudWatch Metrics)

El servicio más fundamental. Recopila y visualiza métricas numéricas en tiempo real de todos los servicios AWS (CPU, memoria, latencia, errores, etc.). Puedes crear tus propias **métricas personalizadas** desde tus aplicaciones.

## Alarmas (CloudWatch Alarms)

Monitorea métricas y **dispara acciones automáticas** cuando superan un umbral, por ejemplo enviar una notificación SNS, escalar instancias EC2 con Auto Scaling, o ejecutar una acción de recuperación.

## Dashboards

Paneles de visualización **personalizables** donde puedes combinar gráficas de métricas, logs y alarmas en una sola vista. Útil para tener visibilidad operacional en tiempo real.

## Logs (CloudWatch Logs)

Lo que ya conoces: recopilación, almacenamiento y análisis de registros.

## Logs Insights

Motor de **consultas interactivas** sobre tus logs con un lenguaje propio para analizar grandes volúmenes de datos rápidamente.

## CloudWatch Events / EventBridge

Detecta **cambios de estado** en recursos AWS y enruta eventos hacia destinos como Lambda, SQS, SNS, etc. (Actualmente evolucionó a Amazon EventBridge).

## CloudWatch Synthetics

Permite crear **canaries** (scripts automatizados) que simulan usuarios navegando tu aplicación para detectar problemas antes que los usuarios reales.

## CloudWatch RUM (Real User Monitoring)

Monitorea la **experiencia real de los usuarios** en tu aplicación web: tiempos de carga, errores JavaScript, rendimiento del navegador.

## CloudWatch Evidently

Sirve para hacer **feature flags** y experimentos A/B en producción, midiendo el impacto de nuevas funcionalidades.

## CloudWatch Internet Monitor

Monitorea la **salud de la conectividad a internet** entre tus usuarios y tus aplicaciones AWS, detectando problemas de red globales.

## CloudWatch Container Insights

Monitoreo especializado para **ECS, EKS y Kubernetes**, recopilando métricas de contenedores, pods y clusters.

## CloudWatch Lambda Insights

Monitoreo avanzado específico para **funciones Lambda**: duración, memoria, cold starts, etc.

## CloudWatch Application Insights

Detecta automáticamente **anomalías y problemas** en aplicaciones .NET y SQL Server que corren en AWS.

---

## Resumen visual

```
CloudWatch
├── Métricas        → ¿Qué números están midiendo mis recursos?
├── Alarmas         → ¿Cuándo algo sale del rango normal?
├── Dashboards      → ¿Cómo visualizo todo junto?
├── Logs            → ¿Qué está escribiendo mi aplicación?
├── Logs Insights   → ¿Cómo consulto mis logs masivamente?
├── Synthetics      → ¿Mi app funciona desde afuera?
├── RUM             → ¿Qué experiencia tienen mis usuarios reales?
├── Evidently       → ¿Cómo pruebo nuevas features?
├── Internet Monitor→ ¿Hay problemas de red hacia mis usuarios?
└── X-Ray / Traces  → ¿Cómo fluyen las solicitudes por mi sistema?
```

En esencia, CloudWatch cubre los **tres pilares de la observabilidad**: métricas, logs y trazas, siendo la solución centralizada de monitoreo de AWS.