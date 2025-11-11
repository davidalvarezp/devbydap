---
author: "davidalvarezp"
title: "Firewall y detección de intrusiones con Suricata y Fail2ban"
slug: "firewall-suricata-fail2ban"
description: "Aprende a configurar un firewall avanzado y sistemas de detección de intrusiones con Suricata y Fail2ban en servidores Linux."
tags: ["Linux", "Seguridad", "Firewall", "IDS"]
categories: ["SysAdmin"]
date: "2025-11-03"
keywords: ["linux", "suricata", "fail2ban", "firewall", "detección de intrusiones"]
draft: false
---

# Firewall y detección de intrusiones con Suricata y Fail2ban

La seguridad de servidores Linux se mejora combinando **firewalls robustos** con **detección de intrusiones**. Suricata permite análisis profundo de tráfico de red, mientras Fail2ban protege contra ataques de fuerza bruta y otros intentos de intrusión.

## Configuración básica de firewall

Para proteger un servidor, primero configuraremos el firewall utilizando UFW y reglas avanzadas de iptables.

### UFW avanzado
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 80,443/tcp
sudo ufw enable
sudo ufw status verbose
```

### iptables
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
sudo iptables -P INPUT DROP
```

## Instalación de Suricata

```bash
sudo apt update
sudo apt install suricata -y
sudo systemctl enable suricata
sudo systemctl start suricata
```

Ejecutar en modo IDS en la interfaz de red eth0:
```bash
sudo suricata -c /etc/suricata/suricata.yaml -i eth0
```

## Configuración de Fail2ban

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

Configurar jail.local para proteger SSH:
```text
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
```

## Monitoreo y alertas

- Ver logs de Suricata: `/var/log/suricata/fast.log`
- Estado de Fail2ban: `sudo fail2ban-client status sshd`

## Buenas prácticas

- Mantener reglas y firmas actualizadas en Suricata
- Revisar periódicamente los logs y alertas
- Limitar permisos de usuarios críticos
- Combinar con hardening de servicios para máxima protección

## Conclusión

Combinando **firewall avanzado, IDS y Fail2ban**, se logra una defensa sólida frente a intrusiones y ataques de fuerza bruta, aumentando significativamente la seguridad de servidores Linux.
