---
author: "davidalvarezp"
title: "Monitorización avanzada con Prometheus y Grafana: métricas, alertas y dashboards profesionales"
slug: "monitorizacion-prometheus-grafana-avanzada"
description: "Guía completa de monitorización con Prometheus y Grafana: instalación, métricas personalizadas, alertas, dashboards y buenas prácticas para entornos de producción."
tags: ["Prometheus", "Grafana", "Monitoring", "DevOps", "Alerting"]
categories: ["sysadmin", "dev"]
date: 2025-11-15
keywords: ["Prometheus", "Grafana", "alerting", "metrics", "dashboards"]
draft: false
---

# Monitorización avanzada con Prometheus y Grafana: métricas, alertas y dashboards profesionales

En entornos modernos de producción, la **observabilidad** es crítica. Prometheus y Grafana son herramientas líderes para recolectar métricas, visualizar datos y generar alertas proactivas.

Este artículo cubre:
- Instalación y configuración avanzada de Prometheus
- Métricas personalizadas
- Integración con Grafana y creación de dashboards
- Alertas y reglas en tiempo real
- Buenas prácticas y optimización

---

## 1. Instalación de Prometheus

### Descarga oficial

```
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.51.0/prometheus-2.51.0.linux-amd64.tar.gz
tar xvfz prometheus-2.51.0.linux-amd64.tar.gz
cd prometheus-2.51.0.linux-amd64
```

### Estructura principal

- prometheus.yml → configuración
- prometheus → binario
- promtool → herramientas de verificación
- consoles/ y console_libraries/ → dashboards básicos

---

## 2. Configuración avanzada de Prometheus

### prometheus.yml ejemplo

```
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']

rule_files:
  - 'alert.rules.yml'
```

### Buenas prácticas

- Definir intervalos de scrape consistentes  
- Usar múltiples jobs para servicios críticos  
- Validar configuración con `promtool check config prometheus.yml`

---

## 3. Métricas personalizadas

### Exporter básico en Bash

```
#!/bin/bash
echo "custom_metric 1"
```

### Exporter en Python

```
from prometheus_client import start_http_server, Gauge
import random

MY_GAUGE = Gauge('my_metric', 'Descripción de mi métrica')
start_http_server(8000)
while True:
  MY_GAUGE.set(random.random())
```

### Integrar exporters en Prometheus

```
- job_name: 'custom'
  static_configs:
    - targets: ['localhost:8000']
```

---

## 4. Grafana: instalación y primeros pasos

### Descarga oficial

```
sudo apt install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
sudo apt update
sudo apt install grafana
sudo systemctl enable --now grafana-server
```

### Configuración básica

- Acceder a `http://localhost:3000`  
- Usuario/admin: admin/admin  
- Configurar datasources → Prometheus

---

## 5. Dashboards avanzados

### Métricas clave

- CPU, memoria, disco, red  
- Latencia de servicios  
- Errores HTTP y logs  
- Métricas personalizadas

### Paneles útiles

- Heatmaps de latencia  
- Tablas de top endpoints  
- Gráficos de alertas recientes

---

## 6. Alerting y reglas

### Alertmanager

```
sudo apt install prometheus-alertmanager
sudo systemctl enable --now alertmanager
```

### Configuración básica

```
global:
  resolve_timeout: 5m

route:
  group_by: ['alertname']
  receiver: 'email'

receivers:
  - name: 'email'
    email_configs:
      - to: 'ops@empresa.com'
```

### Prometheus alert rules

```
groups:
  - name: node.rules
    rules:
      - alert: NodeMemoryHigh
        expr: node_memory_Active_bytes / node_memory_MemTotal_bytes > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Memoria usada > 90%"
```

---

## 7. Scraping avanzado

### Usar relabel_configs

```
- source_labels: [__address__]
  regex: '(.*):.*'
  target_label: instance
  replacement: '${1}'
```

### Filtrado de métricas innecesarias

```
- metric_relabel_configs:
    - source_labels: [__name__]
      regex: 'go_.*'
      action: drop
```

---

## 8. Integración con Kubernetes

### Prometheus Operator

```
kubectl apply -f prometheus-operator.yaml
```

### ServiceMonitors

```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: myservice
spec:
  selector:
    matchLabels:
      app: myservice
  endpoints:
  - port: metrics
    interval: 15s
```

---

## 9. Alerting avanzado con Grafana

### Notificaciones

- Email  
- Slack  
- Webhook  
- Microsoft Teams

### Reglas de alerta complejas

- Condiciones combinadas  
- Detección de picos  
- Alertas silenciables por horarios

---

## 10. Seguridad en monitorización

- Habilitar HTTPS en Prometheus y Grafana  
- Autenticación básica o OAuth2 en Grafana  
- Firewalls para restringir acceso  
- Rotar secrets de exportadores

---

## 11. Escalabilidad

- Sharding de Prometheus  
- Replica Prometheus para HA  
- Uso de Thanos o Cortex para long-term storage  
- Retención configurable de métricas

---

## 12. Optimización de consultas

- Etiquetas consistentes para series  
- Evitar demasiadas series cardinales altas  
- Usar recording rules  
- Cache de dashboards en Grafana

---

## 13. Ejemplo completo de pipeline de monitorización

- Desplegar Prometheus y Alertmanager  
- Desplegar Grafana  
- Configurar exportadores (node_exporter, cadvisor)  
- Configurar dashboards  
- Configurar alertas y notificaciones

---

## 14. Buenas prácticas

- Versionar configuración en Git  
- Revisar métricas críticas periódicamente  
- Documentar dashboards y alertas  
- Hacer pruebas de alertas simuladas  
- Automatizar backup de bases de datos de Prometheus

---

## 15. Conclusión

La monitorización avanzada con Prometheus y Grafana permite:
- Detectar problemas antes de que impacten a usuarios  
- Visualizar métricas personalizadas  
- Automatizar alertas proactivas  
- Escalar a entornos grandes y dinámicos  

> “No se trata solo de medir, sino de actuar a tiempo con la información correcta.”

