---
author: "davidalvarezp"
title: "Monitorización con Loki y Alertmanager"
slug: "monitorizacion-loki-alertmanager"
description: "Aprende a centralizar logs con Loki y configurar alertas con Alertmanager para monitoreo proactivo de sistemas y contenedores."
tags: ["Prometheus", "Loki", "Alertmanager", "Logs"]
categories: ["SysAdmin"]
draft: false
keywords: ["loki", "alertmanager", "monitorización", "logs", "prometheus"]
date: "2025-11-11"
---

# Monitorización con Loki y Alertmanager

Loki centraliza logs de aplicaciones y contenedores. Combinado con Alertmanager y Prometheus, permite **detección de incidentes y alertas proactivas**.

## Instalación de Loki y Promtail

```bash
docker run -d --name loki -p 3100:3100 grafana/loki:2.9.0
docker run -d --name promtail -v /var/log:/var/log grafana/promtail:2.9.0 -config.file=/etc/promtail/config.yaml
```

## Configuración de Alertmanager

```yaml
global:
  resolve_timeout: 5m
route:
  group_by: ['alertname']
  receiver: 'email'
receivers:
- name: 'email'
  email_configs:
  - to: 'ops@empresa.com'
    from: 'alertas@empresa.com'
    smarthost: 'smtp.empresa.com:587'
    auth_username: 'alertas'
    auth_password: 'password'
```

## Buenas prácticas

* Crear dashboards Grafana para logs y métricas
* Configurar alertas críticas y no críticas
* Retener logs suficientes para análisis forense
* Revisar patrones de alertas y ajustar reglas

## Conclusión

Loki + Alertmanager permite **monitorización centralizada de logs y alertas**, mejorando tiempos de respuesta ante incidentes.
