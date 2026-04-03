**No hay un limite de instancias específico por Availability Zone, sino un límite de VCPUs por región.**

El límite de instancias On-Demand se basa en la cantidad de vCPUs permitidas por región. Debes solicitar un aumento de límite a AWS y reintentar las solicitudes fallidas una vez aprobado.

Cada tipo de instancia EC2 tiene un número de vCPUs asignado, y al alcanzar el límite regional, las solicitudes fallarán.

Para lanzar mas instancias, debes solicitar un aumento de límite a AWS a través del Service Quotas en la consola de administración.