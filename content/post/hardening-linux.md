---
author: "davidalvarezp"
title: "Guía práctica de hardening en Linux"
slug: "hardening-linux"
description: "Aprende a asegurar tu servidor Linux con buenas prácticas de hardening paso a paso, protegiendo servicios, usuarios y configuraciones."
tags: ["Linux", "Seguridad", "Servicios", "Servidores"]
categories: ["sysadmin", "cybersec"]
date: 2025-10-20
keywords: ["hardening", "Linux security", "seguridad servidores"]
draft: false
---


# Guía práctica de hardening en Linux

El **hardening** consiste en reducir la superficie de ataque de un sistema. En este artículo, veremos cómo asegurar un servidor Linux de manera práctica.

## Actualiza tu sistema
```bash
sudo apt update && sudo apt upgrade -y
```

## Gestiona usuarios y permisos
- Deshabilita cuentas innecesarias
- Usa sudo en lugar de root
- Configura contraseñas fuertes

## Configura SSH seguro
- Cambia puerto por defecto
- Desactiva login de root
- Usa autenticación con clave

## Firewall y servicios
```bash
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```
- Desactiva servicios que no uses

## Monitoreo y logs
- Instala herramientas como `fail2ban` y `auditd`
- Revisa logs periódicamente

> Con estas prácticas básicas, tu servidor estará mucho más protegido ante ataques comunes.
