---
author: "davidalvarezp"
title: "Monitoriza tus servidores con Prometheus y Grafana"
slug: "monitorizacion-prometheus-grafana"
date: 2025-10-24
description: "Aprende a configurar Prometheus y Grafana para monitorizar métricas de tus servidores y visualizar dashboards en tiempo real."
tags: ["Seguridad", "Monitorización"]
categories: ["SysAdmin"]
draft: false
keywords: ["monitorización", "Prometheus", "Grafana", "servidores"]
---

# Monitoriza tus servidores con Prometheus y Grafana

Prometheus y Grafana permiten visualizar métricas clave de tus servidores.

## Instalar Prometheus
```bash
sudo apt install prometheus
```

## Instalar Grafana
```bash
sudo apt install grafana
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```

## Configurar dashboards
- Conectar Prometheus como datasource en Grafana
- Crear dashboards para CPU, memoria, tráfico de red

> Con esto podrás monitorizar tus servidores y anticiparte a problemas de rendimiento.
