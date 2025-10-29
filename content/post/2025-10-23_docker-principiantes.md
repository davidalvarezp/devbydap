---
author: "davidalvarezp"
title: "Docker para principiantes: contenedores desde cero"
slug: "docker-principiantes"
date: 2025-10-23
description: "Aprende a usar Docker desde cero para crear, ejecutar y gestionar contenedores, mejorando la eficiencia de tus entornos de desarrollo y servidores."
tags: ["Docker", "Containers", "DevOps"]
categories: ["SysAdmin"]
draft: false
keywords: ["docker", "contenedores", "DevOps", "tutorial Docker"]
---

# Docker para principiantes: contenedores desde cero

Docker permite empaquetar aplicaciones y dependencias en contenedores ligeros.

## Instalar Docker
```bash
sudo apt install docker.io
sudo systemctl enable docker
sudo systemctl start docker
```

## Ejecutar un contenedor
```bash
docker run -it --name mi-contenedor ubuntu bash
```

## Crear una imagen propia
```bash
docker build -t mi-imagen .
```

## Gestionar contenedores
```bash
docker ps
docker stop mi-contenedor
docker rm mi-contenedor
```

> Con estos pasos básicos, puedes empezar a usar Docker para simplificar despliegues y entornos de desarrollo.
