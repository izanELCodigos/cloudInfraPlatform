# Cloud & Infrastructure Monitoring Platform

Un laboratorio práctico de infraestructura contenerizada con **Docker Compose** que despliega un stack completo de **observabilidad, métricas, gestión de logs, servidor web y base de datos relacional**.

El objetivo de este proyecto es simular un entorno de producción donde los servicios no solo están aislados y desplegados mediante contenedores, sino también monitorizados en tiempo real.

---

## Arquitectura del Stack

El entorno está compuesto por los siguientes servicios interconectados dentro de una red privada (`app-network`):

### Observabilidad y Métricas
* **Prometheus (`:9090`)**: Recolección y almacenamiento de métricas en series temporales.
* **Grafana (`:3000`)**: Panel de control visual para métricas y logs.
* **Node Exporter (`:9100`)**: Extracción de métricas de hardware y sistema operativo del host.
* **Nginx Exporter**: Scrapeo de métricas del servidor web (`stub_status`).

### Gestión de Logs (Logging)
* **Loki (`:3010`)**: Sistema de agregación de logs optimizado para Grafana.
* **Promtail**: Agente encargado de recolectar los logs de los contenedores Docker y enviarlos a Loki.

### Servidor Web & Datos
 **Nginx (`:80`, `:443`)**: Servidor web que actúa como punto de entrada HTTP/HTTPS.
* **MySQL 8.0**: Base de datos relacional con credenciales gestionadas mediante variables de entorno (`.env`).
* **CloudBeaver (`:4010`)**: Cliente web ligero para administración de la base de datos MySQL.

---

## Estructura de Persistencia y Redes

* **Redes**: Todos los contenedores se comunican a través de una red dedicada de tipo `bridge` (`app-network`), evitando la exposición innecesaria de puertos internos.
* **Volúmenes Persistentes**:
  * `grafana_data`: Mantiene los dashboards y configuraciones de Grafana.
  * `mysql_data`: Mantiene la persistencia de las bases de datos de MySQL.
  * `cloudbeaver_data`: Almacena la configuración y espacio de trabajo de CloudBeaver.
  * Mapeos en modo lectura (`:ro`) para archivos de configuración (`prometheus.yml`, `nginx.conf`, `promtail-config.yaml`).

---

## Despliegue e Instalación

### Prerrequisitos
* Docker y Docker Compose instalados.
* Git.

### Pasos
1. **Clonar el repositorio:**
   ```bash
   git clone [https://github.com/IzanELCodigos/Tu-Repo.git](https://github.com/IzanELCodigos/Tu-Repo.git)
   cd Tu-Repo