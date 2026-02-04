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
- Datos y justificación:
- Impacto en el CRM:

---

## 3. Resolución de una incidencia técnica simulada
### 3.1 Síntomas
### 3.2 Diagnóstico
### 3.3 Acción aplicada
### 3.4 Verificación
### 3.5 Rollback

---

## 4. Simulación de saturación del sistema (CPU o Memoria)
- Técnica utilizada:
- Datos capturados:
- Análisis:
- Verificación requisitos HW/SW:
- Registro:

---

## 5. Documentación y registro técnico
### 5.1 Incidencias detectadas / Acciones / Resultados
### 5.2 Interpretación de documentación en inglés (monitorización / rendimiento / administración CRM)
- Fragmento 1 (EN):
- Interpretación (ES):
- Fragmento 2 (EN):
- Interpretación (ES):
- Fragmento 3 (EN):
- Interpretación (ES):
