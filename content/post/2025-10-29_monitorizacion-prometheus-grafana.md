---
author: "davidalvarezp"
title: "Monitoriza tus servidores con Prometheus y Grafana"
slug: "monitorizacion-prometheus-grafana"
date: 2025-10-29
description: "Aprende a configurar Prometheus y Grafana para monitorizar métricas de tus servidores y visualizar dashboards en tiempo real."
tags: ["Seguridad", "Monitorización"]
categories: ["SysAdmin"]
draft: false
keywords: ["monitorización", "Prometheus", "Grafana", "servidores"]
---

# Monitoriza tus servidores con Prometheus y Grafana

En entornos modernos, la observabilidad es fundamental para garantizar la disponibilidad y el rendimiento de los sistemas. Prometheus y Grafana forman una de las combinaciones más potentes para recolectar, almacenar y visualizar métricas de servidores y servicios.

Prometheus se encarga de recopilar y almacenar métricas mediante un modelo pull (consultando endpoints /metrics), mientras que Grafana actúa como interfaz visual, permitiendo construir paneles interactivos y alertas basadas en esas métricas.

## Instalar Prometheus

Para comenzar, instala Prometheus desde los repositorios oficiales:
```bash
sudo apt update
sudo apt install prometheus
```

El servicio Prometheus se instala y se ejecuta automáticamente como un demonio del sistema (prometheus.service). Puedes verificar su estado con:
```bash
sudo systemctl status prometheus
```

Por defecto, Prometheus expone su interfaz web en el puerto 9090, accesible desde http://<ip_servidor>:9090. Desde ahí puedes ejecutar consultas PromQL (Prometheus Query Language) para inspeccionar métricas.

La configuración principal se encuentra en /etc/prometheus/prometheus.yml, donde puedes definir los targets (hosts o servicios) desde los cuales se recopilarán métricas:
```yaml
scrape_configs:

job_name: "servidores"
static_configs:

targets: ["localhost:9100"]
```

Para obtener métricas de sistemas Linux (CPU, RAM, red, disco, etc.), instala el exporter correspondiente:
```bash
sudo apt install prometheus-node-exporter
```
Este componente expone métricas del sistema en :9100/metrics, que luego Prometheus recolectará automáticamente.

## Instalar Grafana

Grafana es la capa de visualización de la pila de monitorización. Permite crear dashboards personalizables y configurar alertas.

Instala Grafana con los siguientes comandos:
```bash
sudo apt install grafana
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

El servicio se ejecuta por defecto en el puerto 3000 (http://<ip_servidor>:3000) y las credenciales iniciales son:
- Usuario: admin
- Contraseña: admin

Se recomienda cambiar la contraseña en el primer inicio de sesión.

Una vez dentro, el siguiente paso es conectar Prometheus como fuente de datos (Data Source):
- En el panel lateral, ve a Connections → Data sources → Add data source.
- Selecciona Prometheus.
- En el campo URL, introduce:
```
http://localhost:9090

```
- Guarda la configuración haciendo clic en Save & Test.

## Configurar dashboards

Una vez establecida la conexión, puedes crear dashboards personalizados para visualizar métricas clave.

Algunos ejemplos de paneles recomendados:
- CPU Usage: métrica node_cpu_seconds_total filtrada por modo idle o user.
- Memoria RAM: node_memory_MemAvailable_bytes y node_memory_MemTotal_bytes.
- Tráfico de red: node_network_receive_bytes_total y node_network_transmit_bytes_total.
- Espacio en disco: node_filesystem_avail_bytes y node_filesystem_size_bytes.

Puedes importar dashboards preconstruidos desde grafana.com/grafana/dashboards
 Un ejemplo muy usado es el Node Exporter Full (ID: 1860), que ofrece visualizaciones completas para hosts Linux.

Para importar un dashboard:
- En Grafana, ve a Dashboards → Import.
- Introduce el ID (1860) y selecciona la fuente de datos Prometheus.
- Haz clic en Load y luego Import.

## Buenas prácticas de monitorización

- Mantén Prometheus y Grafana actualizados a la última versión estable.
- Limita el acceso web mediante autenticación o VPN.
- Configura retención de métricas según tus necesidades (--storage.tsdb.retention.time=15d).
- Crea alertas en Grafana para CPU alta, uso de memoria o pérdida de conectividad.
- Centraliza la monitorización de múltiples servidores en una misma instancia de Prometheus mediante federation.

## Conclusión

Con Prometheus y Grafana, puedes obtener una visión completa del estado de tus servidores y anticiparte a problemas de rendimiento o disponibilidad. Esta combinación permite implementar una cultura de observabilidad, clave en entornos DevOps y de producción moderna.

> Con esto podrás monitorizar tus servidores y anticiparte a problemas de rendimiento.
