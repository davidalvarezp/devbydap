---
author: "davidalvarezp"
title: "Automatiza tus tareas con Bash y Cron"
slug: "automatizar-tareas-bash-cron"
date: 2025-10-21
description: "Aprende a automatizar tareas en Linux usando scripts Bash y cron, optimizando la gestión de servidores y procesos repetitivos."
tags: ["Linux", "Automatización", "Bash"]
categories: ["SysAdmin"]
draft: false
keywords: ["bash", "cron", "automatización", "linux scripts"]
---

# Automatiza tus tareas con Bash y Cron

La automatización es clave para administrar servidores de forma eficiente.

## Crear un script Bash
```bash
#!/bin/bash
echo "Backup de la base de datos iniciado"
# comando de backup aquí
```

## Hacerlo ejecutable
```bash
chmod +x backup.sh
```

## Programar con Cron
```bash
crontab -e
```
Agregar línea:
```
0 2 * * * /ruta/a/backup.sh
```

- Ejecuta el script todos los días a las 2:00 AM

> Con Bash + Cron puedes automatizar casi cualquier tarea repetitiva en tu servidor.
