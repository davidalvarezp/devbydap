---
author: "davidalvarezp"
title: "Hardening avanzado de SSH: defensa contra fuerza bruta, túneles seguros y configuración enterprise"
slug: "ssh-hardening-avanzado"
description: "Guía completa para asegurar SSH a nivel profesional: endurecimiento, cifrado moderno, mitigación de fuerza bruta, claves, MFA y monitoreo."
tags: ["SSH", "Seguridad", "Linux", "Servidores"]
categories: ["sysadmin", "cybersec"]
date: 2025-11-14
keywords: ["ssh hardening", "seguridad ssh", "fuerza bruta ssh", "linux security"]
draft: false
---

# Hardening avanzado de SSH: defensa contra fuerza bruta, túneles seguros y configuración enterprise

SSH es la puerta de entrada más utilizada para administrar servidores Linux y, por lo tanto, también uno de los vectores de ataque más frecuentes.

Un servicio SSH mal configurado puede permitir:
- Ataques de fuerza bruta
- Accesos no autorizados
- Movimientos laterales
- Escaladas de privilegios
- Robo de claves

En este artículo aprenderás a implementar un **SSH Zero Trust**, endurecido al máximo y adaptado a entornos empresariales o de alta seguridad.

---

## 1. Deshabilitar configuraciones inseguras por defecto

Edición del archivo:
```
sudo nano /etc/ssh/sshd_config
```

### Desactivar login directo de root

```
PermitRootLogin no
```

### Desactivar contraseñas

```
PasswordAuthentication no
KbdInteractiveAuthentication no
```

### Limitar protocolos

```
Protocol 2
```

### Deshabilitar autenticación insegura

```
HostbasedAuthentication no
RhostsRSAAuthentication no
RSAAuthentication no
```

---

## 2. Cambiar el puerto SSH de forma inteligente

```
Port 2222
```

No es una medida de seguridad absoluta, pero **reduce ruido**, fuerza bruta y escaneo.

### Abrir el puerto en el firewall
```
sudo ufw allow 2222/tcp
```

---

## 3. Claves SSH modernas y seguras

### Generar claves modernas recomendadas (ed25519)

```
ssh-keygen -t ed25519 -a 200 -C "admin@server"
```

### Alternativa segura (RSA 4096)

```
ssh-keygen -t rsa -b 4096 -o -a 200
```

### Deshabilitar claves antiguas en sshd

```
PubkeyAcceptedKeyTypes=ssh-ed25519,ssh-rsa
```

---

## 4. Activar autenticación multifactor (MFA)

Mucho más seguro que claves solas.

### Instalar Google Authenticator PAM

```
sudo apt install libpam-google-authenticator
```

### Ejecutar configuración por usuario
```
google-authenticator
```

### Editar PAM

```
sudo nano /etc/pam.d/sshd
```

Añadir:
```
auth required pam_google_authenticator.so nullok
```

### Habilitar MFA en sshd

```
ChallengeResponseAuthentication yes
```

---

## 5. Limitar accesos por usuario, grupo y IP

### Acceso solo a usuarios concretos

```
AllowUsers admin deploy
```

### Acceso por grupos

```
AllowGroups admins
```

### Acceso solo desde ciertas IP

```
Match Address 192.168.1.0/24
    PasswordAuthentication no
```

---

## 6. Timeouts agresivos para romper ataques

```
LoginGraceTime 20
ClientAliveInterval 30
ClientAliveCountMax 2
```

Esto reduce sesiones colgadas y bots intentando conexiones masivas.

---

## 7. Cifrado moderno (Kex, MACs, Ciphers)

### Reemplazar cifrados inseguros

```
KexAlgorithms curve25519-sha256
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com
MACs hmac-sha2-512,hmac-sha2-256
```

### Ver soportes del servidor

```
ssh -Q cipher
ssh -Q kex
ssh -Q mac
```

---

## 8. Mitigar fuerza bruta con Fail2Ban

### Instalar
```
sudo apt install fail2ban -y
```

### Configurar
```
sudo nano /etc/fail2ban/jail.local
```

```
[sshd]
enabled = true
maxretry = 3
bantime = 1h
findtime = 10m
```

### Reiniciar
```
sudo systemctl restart fail2ban
```

---

## 9. Wazuh / OSSEC para análisis en tiempo real

Para detección avanzada:
- Cambios en archivos
- Intentos de acceso
- Fuerza bruta distribuida
- SSH hijacking

### Instalación rápida Wazuh

```
curl -sO https://packages.wazuh.com/4.8/wazuh-agent.deb
sudo dpkg -i wazuh-agent.deb
```

---

## 10. Port knocking avanzado (port-knock)

Abre el puerto SSH solo tras enviar una secuencia de “golpes”.

### Configuración con knockd

```
sudo apt install knockd
```

```
[options]
start_command = ufw allow 2222
stop_command = ufw deny 2222
```

---

## 11. SSH sobre WireGuard (Zero Trust real)

### Crear túnel seguro

```
wg genkey | tee wg.key | wg pubkey > wg.pub
```

### SSH limitado exclusivamente al túnel

```
ListenAddress 10.10.10.1:22
```

---

## 12. Registros avanzados con auditd

### Instalar auditd
```
sudo apt install auditd
```

### Auditar acceso a claves
```
auditctl -w /home/*/.ssh/ -p war -k ssh_keys
```

### Auditar configuraciones
```
auditctl -w /etc/ssh/sshd_config -p wa -k ssh_config
```

---

## 13. Monitorizar intentos de fuerza bruta en tiempo real

### Comando útil
```
sudo tail -f /var/log/auth.log
```

### Detección con awk
```
awk '/Failed password/ {print $1,$2,$3,$11}' /var/log/auth.log
```

---

## 14. Reglas avanzadas de iptables

### Limitar conexiones simultáneas
```
iptables -A INPUT -p tcp --syn --dport 2222 -m connlimit --connlimit-above 3 -j DROP
```

### Limitar velocidad
```
iptables -A INPUT -p tcp --dport 2222 -m state --state NEW -m recent --update --seconds 60 --hitcount 10 -j DROP
```

---

## 15. Verificación automática de integridad SSH

### Script de autocomprobación

```
if ! sha256sum -c /etc/ssh/sshd_config.sha256; then
  echo "⚠ CONFIG SSH ALTERADA"
fi
```

---

## 16. Proteger claves SSH del usuario

### Permisos correctos
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Evitar ssh-agent en memoria persistente

---

## 17. SSH con certificados (CA interna)

Método de autenticación enterprise.

### Crear CA
```
ssh-keygen -f ssh_ca -t ed25519
```

### Firmar claves
```
ssh-keygen -s ssh_ca -I usuario -n usuario id_ed25519.pub
```

### Configurar servidor

```
TrustedUserCAKeys /etc/ssh/ca.pub
```

---

## 18. Evitar ataques MITM

### Revisar fingerprint siempre
```
ssh-keyscan -H server.com >> ~/.ssh/known_hosts
```

### Usar DNSSEC + SSHFP

```
ssh-keygen -r dominio.com
```

---

## 19. Buenas prácticas adicionales

- Deshabilitar SSHv1  
- Usar logs remotos  
- Usar banners legales  
- Limitar SFTP  
- Rotar claves automáticamente  
- Bloquear países completos con geoip  
- Autenticación por hardware (YubiKey)  

---

## 20. Configuración final completa recomendada (sshd_config)

```
Port 2222
Protocol 2
PermitRootLogin no
PasswordAuthentication no
KbdInteractiveAuthentication no
PubkeyAuthentication yes
ChallengeResponseAuthentication yes
Usedns no
LoginGraceTime 20
ClientAliveInterval 30
ClientAliveCountMax 2
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com
KexAlgorithms curve25519-sha256
MACs hmac-sha2-512,hmac-sha2-256
AllowUsers admin
TrustedUserCAKeys /etc/ssh/ca.pub
```

---

## Conclusión

Un SSH seguro no se basa en una sola medida, sino en un **conjunto de capas**:
- Cifrado moderno  
- Autenticación fuerte  
- Restricciones de acceso  
- Firewalls  
- Monitoreo  
- Reglas antibruteforce  
- Integridad del sistema  

Implementar todo este hardening eleva tu servidor al nivel de seguridad requerido en infraestructuras críticas, empresas y entornos cloud modernos.

> “La seguridad no es un estado, es un proceso continuo.”
