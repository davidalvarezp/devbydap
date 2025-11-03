---
author: "davidalvarezp"
title: "Cómo detectar y mitigar ataques de fuerza bruta en SSH"
slug: "mitigar-fuerza-bruta-ssh"
date: 2025-10-24
description: "Aprende a proteger tus servidores SSH de ataques de fuerza bruta y a configurar medidas de seguridad para evitar accesos no autorizados."
tags: ["Seguridad"]
categories: ["CyberSec", "SysAdmin"]
draft: true
keywords: ["SSH", "fuerza bruta", "seguridad servidores"]
---

# Cómo detectar y mitigar ataques de fuerza bruta en SSH

Los ataques de fuerza bruta son intentos repetidos de adivinar contraseñas de usuarios en SSH.

## Revisar intentos de acceso
```bash
grep "Failed password" /var/log/auth.log
```

## Configurar fail2ban
```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

## Ajustar SSH
- Cambiar puerto por defecto
- Deshabilitar root login
- Usar claves en lugar de contraseñas

> Estas medidas reducen significativamente el riesgo de ataques automatizados.
