# E2 UF1885 - Detección, análisis y resolución de incidencias (ERP-CRM)

**Alumno:** Dominguez, Milagros  
**Fecha:** 1965-11-28  
**Entorno:** Ubuntu Server + Docker  
**Contenedores:** odoo-dev-E1UF1884 (CRM) | postgrpostgres-dev-E1UF1884 (BD)

---

## 1. Análisis inicial del sistema y parámetros de rendimiento
### 1.1 Servicios de acceso al CRM
- Descripción:
  - Acceso al ERP/CRM (aplicaciones web): contenedor odoo-dev-E1UF1884
  - El servicio de base de datos: contenedor postgres-dev-E1UF1884
  - Servicio de publicación  de puerto / acceso web: Docker publica 8069/tcp
  - Red y DNS del sistema: interfaz la IP  192.168.1.137
  - Acceso administrativo remoto: SSH en 22/tcp para tareas de soporte.
- Evidencias: evidencias/01_analisis/

### 1.2 Parámetros (CPU / RAM / Disco / Red) y relación con CRM+BD
  -CPU ~ 64.7 idle, load average: 2.33, 1.05, 0.56
- Conclusiones: No hay saturación de CPU.

- RAM   10Gi total;      1.1Gi usado;       9.0Gi libre
- Conclusiones: Hay suficiente memoria, no hay presión ahora mismo con la RAM. 

- Disco: /dev/sda2   tamaño:98G   usado: 11G   disponible: 83G   % uso: (12%) 
- Conclusiones: No hay problema de capacidad por ahora


---

## 2. Monitorización de procesos y detección de sobrecarga
### 2.1 Proceso problemático detectado
- Proceso/servicio:
  - Contenedor de postgres-dev-UF1884 (servicio postgreSQL para ERP/CRM)
  - Proceso interno forzado por el sistema: yes > /dev/null & (generador carga CPU)
- Datos y justificación:
  - CPU %:(postgres-dev-UF1884): 11548.91%, indica saturación
  - Consumo de memoria bajo ( 109.3MiB / 10.81GiB)
  - Saqturación se produce a nivel del CPU
- Impacto en el CRM:
  - Lentitud extrema en operaciones que dependen de la base de datos.
  - Usuarios perciben bloqueos y esperas prolongadas.

---

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
- Los usuarios no pueden acceder al CRM
- La URL del servicio no responde.
### 3.2 Diagnóstico
- Verificar el estado de los contenedores (docker ps).
- El contedor odoo-dev-E1UF1884 no se encuentra en ejecución.
### 3.3 Acción aplicada
- Se procede a restablecer el servicio de contenedor, arrancando nuevamente.
 ```    sudo docker start odoo-dev-E1UF1884
 ```
### 3.4 Verificación
- Verificar el estado del contenedor
-  **sudo docker ps**
### 3.5 Rollback
 - En esta situación consiste en arrancar el contenedor como se indica en la acción  

---

## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada:
  Simulación saturación de memoria RAM mediante ejecución de un proceso que consume gran cantidad de memoria,
  provocando una reducción importante de la memoria libre 
- Datos capturados:
  free -h->antes y después de la simulación
  vmstat 1 5 antes y después de la simulación   
- Análisis:
  Análisis de la simulación disponia de 8,9Gi de memoria libre. Tras la simulación, la memoria libre es de 1,1Gi el sistema no ha llegado a nivel crítico, pero si a un escenario
  de riesgo 
- Verificación requisitos HW/SW:
  El sistema cuenta con 10 Gib RAM y no tiene swap configurada.
  Para entornos ERP/CRM con carga recurrente esta configuración puede ser insuficiente en picos de consumo de memoria.
       Aumentar memoria RAM disponible, o
       configurar swap comop medida preventiva.
- Registro:
  La simulación se realizó de forma controlada y reversible sin pérdida de datos.

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN): «Docker proporciona comandos integrados para monitorear el uso de recursos de los contenedores, incluidos CPU, memoria y E/S de red, lo que ayuda a identificar cuellos de botella de rendimiento.»
- Interpretación (ES): Docker proporciona comandos integrados que permiten monitorizar el uso de recursos de los contenedores, como CPU y memoria, lo que facilita la identificación de cuellos de botella que pueden afectar al rendimiento del sistema ERP-CRM.
- Fragmento 2 (EN): «El uso elevado de memoria puede afectar significativamente el rendimiento de la aplicación, lo que podría provocar tiempos de respuesta más lentos o inestabilidad del servicio.»
- Interpretación (ES):
- Fragmento 3 (EN): «El uso elevado de memoria puede afectar significativamente el rendimiento de la aplicación, lo que podría provocar tiempos de respuesta más lentos o inestabilidad del servicio.»
- Interpretación (ES):
