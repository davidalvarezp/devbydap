---
author: "davidalvarezp"
title: "Infraestructura como código avanzada con AWS CDK"
slug: "iac-aws-cdk"
description: "Aprende a crear y gestionar infraestructura en AWS usando AWS CDK con buenas prácticas y ejemplos de despliegues completos."
tags: ["AWS", "CDK", "IaC", "DevOps"]
categories: ["Dev"]
date: "2025-11-07"
keywords: ["aws", "cdk", "infraestructura como código", "iac"]
draft: false
---

# Monitorización de contenedores con cAdvisor y Prometheus

cAdvisor proporciona métricas en tiempo real de contenedores Docker. Combinado con Prometheus, permite análisis histórico y alertas basadas en uso de recursos.

## Instalación de cAdvisor

```bash
docker run   --volume=/:/rootfs:ro   --volume=/var/run:/var/run:rw   --volume=/sys:/sys:ro   --volume=/var/lib/docker/:/var/lib/docker:ro   --publish=8080:8080   --detach=true   --name=cadvisor   google/cadvisor:latest
```

## Integración con Prometheus

Agregar un job en `prometheus.yml`:
```yaml
scrape_configs:
  - job_name: 'cadvisor'
    static_configs:
      - targets: ['host.docker.internal:8080']
```

## Buenas prácticas

- Configurar dashboards Grafana para métricas de CPU, memoria y red
- Definir alertas para uso elevado de recursos
- Monitorear containers críticos y estado de replicación

## Conclusión

cAdvisor + Prometheus permite **monitorización detallada de contenedores**, asegurando estabilidad y rendimiento de la infraestructura Docker.
