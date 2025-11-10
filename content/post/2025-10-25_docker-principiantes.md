---
author: "davidalvarezp"
title: "Docker para principiantes: contenedores desde cero"
slug: "docker-principiantes"
date: 2025-10-25
description: "Aprende a usar Docker desde cero para crear, ejecutar y gestionar contenedores, mejorando la eficiencia de tus entornos de desarrollo y servidores."
tags: ["Docker", "Containers", "DevOps"]
categories: ["SysAdmin"]
draft: false
keywords: ["docker", "contenedores", "DevOps", "tutorial Docker"]
---

# Docker para principiantes: contenedores desde cero

Docker ha revolucionado la forma en que desarrollamos, desplegamos y ejecutamos aplicaciones. En lugar de lidiar con entornos inconsistentes o dependencias rotas, Docker permite **empaquetar todo lo necesario** (código, librerías y configuraciones) dentro de **contenedores ligeros y portables**.

En este artículo veremos cómo instalar Docker, ejecutar tu primer contenedor, crear una imagen personalizada y gestionar contenedores en tu sistema.

---

## ¿Qué es un contenedor?

Un **contenedor** es una instancia ejecutable de una imagen. Las imágenes son plantillas inmutables que definen el entorno y el software que se ejecutará dentro del contenedor.  
A diferencia de las máquinas virtuales, los contenedores comparten el **kernel del sistema operativo** del host, lo que los hace mucho más ligeros y rápidos.

📦 **Ventajas principales:**
- Aislamiento de procesos y dependencias  
- Portabilidad entre entornos (local, staging, producción)  
- Despliegues consistentes y reproducibles  
- Menor consumo de recursos frente a las VMs tradicionales  

---

## Instalación de Docker

En distribuciones basadas en Debian o Ubuntu, puedes instalar Docker directamente desde los repositorios oficiales:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

Verifica que la instalación haya sido exitosa con:

```bash

docker --version
```

Y prueba que el servicio esté en ejecución:

```bash
sudo systemctl status docker
```

> Consejo: Si prefieres evitar usar sudo cada vez, agrega tu usuario al grupo docker:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

## Ejecutar tu primer contenedor

El siguiente comando descarga la imagen oficial de Ubuntu y ejecuta un contenedor interactivo con una shell bash:

```bash
docker run -it --name mi-contenedor ubuntu bash
```

- -it: Permite interactuar con el contenedor (modo terminal).
- --name: Asigna un nombre personalizado al contenedor.
- ubuntu: Es la imagen base.
- bash: El comando que se ejecutará dentro del contenedor.

Dentro del contenedor, notarás un prompt similar a este:

```bash
root@<container_id>:/#
```

Estás dentro de un entorno aislado, con su propio sistema de archivos. Puedes instalar paquetes, ejecutar comandos, o incluso montar volúmenes externos.

Para salir sin detener el contenedor:

```bash
exit
```

---

## Crear tu propia imagen

Supongamos que quieres crear una imagen personalizada basada en Ubuntu que tenga curl y git instalados.
Primero, crea un archivo llamado Dockerfile en un directorio vacío con el siguiente contenido:

```dockerfile
# Imagen base
FROM ubuntu:latest

# Instalar dependencias
RUN apt update && apt install -y curl git

# Comando por defecto
CMD ["bash"]
```

Luego, construye la imagen con:

```bash
docker build -t mi-imagen .
```

- -t mi-imagen: Asigna un nombre a la imagen.
- .: Indica el contexto de construcción (directorio actual).

Para comprobar que se creó correctamente:

```bash
docker images
```

Y puedes ejecutarla con:

```bash
docker run -it mi-imagen
```

---

## Gestión básica de contenedores

Una vez que empieces a usar Docker de forma habitual, necesitarás gestionar tus contenedores activos e inactivos.

Listar contenedores en ejecución:

```bash
docker ps
```

Listar todos los contenedores (incluidos los detenidos):

```bash
docker ps -a
```

Detener un contenedor:

```bash
docker stop mi-contenedor
```

Eliminar un contenedor detenido:

```bash
docker rm mi-contenedor
```

Eliminar imágenes que ya no necesites:

```bash
docker rmi mi-imagen
```

Y para limpiar recursos huérfanos o temporales:

```bash
docker system prune
```

---

## Docker Hub: el repositorio de imágenes
Docker Hub es el repositorio público oficial de Docker, donde puedes descargar imágenes ya preparadas o subir tus propias imágenes.
Por ejemplo, puedes ejecutar una aplicación Node.js sin necesidad de instalar Node en tu host:

```bash
docker run -it --rm node:20 bash
```

---

## Conclusión
Docker simplifica el ciclo de vida del desarrollo al empaquetar entornos completos en contenedores reproducibles y portables.

Con unos pocos comandos, puedes:

- Crear y ejecutar contenedores en segundos
- Construir imágenes personalizadas
- Mantener entornos limpios y consistentes

Si sigues estos pasos básicos, tendrás las bases sólidas para adentrarte en temas más avanzados como Docker Compose, volúmenes persistentes, y redes personalizadas, que veremos en futuras entregas.

> Con Docker, la frase “en mi máquina sí funciona” pasa a ser cosa del pasado.
