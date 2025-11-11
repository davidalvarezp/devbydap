---
author: "davidalvarezp"
title: "Cómo detectar y mitigar ataques de fuerza bruta en SSH"
slug: "mitigar-fuerza-bruta-ssh"
date: 2025-10-28
description: "Aprende a proteger tus servidores SSH de ataques de fuerza bruta y a configurar medidas de seguridad para evitar accesos no autorizados."
tags: ["Seguridad"]
categories: ["CyberSec", "SysAdmin"]
draft: false
keywords: ["SSH", "fuerza bruta", "seguridad servidores"]
---

# Cómo detectar y mitigar ataques de fuerza bruta en SSH

Los ataques de fuerza bruta son intentos automatizados y repetitivos para adivinar contraseñas de usuarios a través del servicio SSH (Secure Shell). Este tipo de ataque aprovecha configuraciones débiles o credenciales predecibles, y puede comprometer por completo un servidor si no se aplican medidas de protección adecuadas.

## Revisar intentos de acceso

El primer paso para mitigar un ataque de fuerza bruta es detectar los intentos fallidos de autenticación. El log del sistema registra estos eventos en /var/log/auth.log (en distribuciones basadas en Debian) o /var/log/secure (en Red Hat y derivados).

Para listar los intentos fallidos puedes usar:
```bash
grep "Failed password" /var/log/auth.log
```

Este comando muestra líneas con información sobre la IP origen, el usuario objetivo y la hora del intento. También puedes contar el número de ataques por dirección IP:
```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
```

Este análisis permite identificar patrones de ataque y decidir si es necesario bloquear direcciones IP manualmente mediante iptables, ufw, o herramientas de detección automática.

## Configurar fail2ban

Fail2ban es una herramienta que analiza los logs del sistema y bloquea automáticamente las direcciones IP que muestran un comportamiento sospechoso (por ejemplo, múltiples intentos de login fallidos en poco tiempo).

Para instalar y habilitar fail2ban:
```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

Una vez instalado, puedes crear una configuración personalizada en /etc/fail2ban/jail.local:
```bash
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
findtime = 600
```

En este ejemplo:
- maxretry define el número máximo de intentos fallidos antes del bloqueo.
- bantime indica el tiempo (en segundos) que la IP permanecerá bloqueada.
- findtime establece el periodo de análisis para esos intentos.

Para verificar que fail2ban está funcionando correctamente:
```bash
sudo fail2ban-client status sshd
```

Este comando muestra cuántas IPs han sido bloqueadas y cuáles siguen activas.

## Ajustar configuración de SSH

Una configuración segura del demonio SSH (sshd) es esencial para reducir la superficie de ataque. Edita el archivo /etc/ssh/sshd_config y aplica los siguientes ajustes:

- Cambiar el puerto por defecto:
```bash
Port 2222
```
Esto reduce los intentos automatizados dirigidos al puerto 22.

- Deshabilitar el acceso directo como root:
```bash
PermitRootLogin no
```
Evita que un atacante intente adivinar la contraseña del usuario root directamente.

- Usar autenticación por claves públicas en lugar de contraseñas:
```bash
PasswordAuthentication no
PubkeyAuthentication yes
```
Las claves SSH utilizan criptografía asimétrica (RSA, Ed25519 o ECDSA) y son prácticamente imposibles de forzar por métodos de fuerza bruta.

- Limitar usuarios permitidos:
```bash
AllowUsers admin devops
```
Solo los usuarios listados podrán autenticarse vía SSH.

- Activar logs detallados:
```bash
LogLevel VERBOSE
```
Esto facilita auditorías y análisis de incidentes.

Una vez realizados los cambios, recarga el servicio:
```bash
sudo systemctl reload ssh
```

## Monitoreo continuo y alertas

Además de fail2ban, es recomendable implementar monitoreo continuo mediante herramientas como:
- OSSEC o Wazuh: detección de intrusiones y correlación de eventos.
- Prometheus + Grafana: visualización de métricas de intentos SSH.
- Syslog remoto o SIEM (Security Information and Event Management) para correlacionar eventos entre múltiples servidores.

## Conclusión

La protección de servicios SSH es un pilar esencial de la seguridad en servidores Linux. Detectar intentos de fuerza bruta, aplicar reglas de bloqueo automático con fail2ban y endurecer la configuración de SSH son pasos críticos para minimizar riesgos.

.> Estas medidas reducen significativamente el riesgo de ataques automatizados y mejoran la resiliencia general de tu infraestructura.
