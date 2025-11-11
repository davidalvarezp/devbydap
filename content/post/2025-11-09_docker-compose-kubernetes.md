---
author: "davidalvarezp"
title: "Despliegue de contenedores con Docker Compose y Kubernetes"
slug: "docker-compose-kubernetes"
description: "Aprende a orquestar contenedores usando Docker Compose y migrarlos a Kubernetes para producción escalable."
tags: ["Docker", "Kubernetes", "DevOps", "Orquestación"]
categories: ["Dev"]
draft: false
keywords: ["docker", "compose", "kubernetes", "containers", "orquestación"]
date: "2025-11-09"
---

# Despliegue de contenedores con Docker Compose y Kubernetes

Docker Compose facilita el desarrollo y prueba de aplicaciones multi-contenedor, mientras Kubernetes permite **escalar y gestionar producción** de forma automatizada.

## Docker Compose

### Instalación

```bash
sudo apt install docker-compose -y
docker-compose --version
```

### Archivo `docker-compose.yml`

```yaml
version: '3.9'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: example
```

### Comandos útiles

```bash
docker-compose up -d
docker-compose logs
docker-compose down
```

## Migración a Kubernetes

### Crear Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx:latest
        ports:
        - containerPort: 80
```

### Crear Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

### Buenas prácticas

* Versionar manifiestos en Git
* Configurar namespaces por entorno
* Utilizar ConfigMaps y Secrets para configuración y credenciales
* Hacer health checks y readiness probes

## Conclusión

Docker Compose es excelente para desarrollo, y Kubernetes para **producción escalable**, combinando ambos permite flujo completo CI/CD.
