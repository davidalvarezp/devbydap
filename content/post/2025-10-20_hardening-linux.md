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

El **hardening** (o endurecimiento del sistema) es el proceso de reducir la superficie de ataque de un servidor, minimizando las vulnerabilidades y mejorando su resistencia frente a amenazas.  
En esta guía aprenderás, paso a paso, cómo aplicar buenas prácticas de seguridad en tu servidor **Linux**, desde la gestión de usuarios hasta la protección de servicios y registros del sistema.

---

## Mantén tu sistema actualizado

Un sistema desactualizado es uno de los principales vectores de ataque. Las actualizaciones corrigen vulnerabilidades conocidas, por lo que mantener tu distribución al día debe ser una prioridad.

```bash
sudo apt update && sudo apt upgrade -y
```

Además, puedes habilitar actualizaciones automáticas para paquetes críticos:

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

Esto garantizará que tu sistema reciba parches de seguridad incluso si olvidas actualizarlos manualmente.

---

## Gestión segura de usuarios y permisos

Controlar quién puede acceder al sistema es esencial. Algunas recomendaciones:

- **Deshabilita o elimina cuentas innecesarias:**  
  Cada cuenta es un posible punto de entrada. Usa `sudo deluser` o `sudo usermod -L usuario` para desactivarlas.
  
- **Evita el uso del usuario root:**  
  Trabaja con una cuenta estándar y usa `sudo` para tareas administrativas.  
  ```bash
  sudo adduser admin
  sudo usermod -aG sudo admin
  ```

- **Usa contraseñas fuertes o autenticación multifactor:**  
  Apóyate en herramientas como `pam_cracklib` o `libpam-pwquality` para reforzar políticas de contraseñas.

- **Revisa permisos de archivos críticos:**  
  ```bash
  sudo chmod 600 /etc/shadow
  sudo chmod 644 /etc/passwd
  ```

---

## Configura un SSH seguro

SSH es la puerta de entrada más usada a los servidores Linux, por lo que merece especial atención.

Edita el archivo de configuración:
```bash
sudo nano /etc/ssh/sshd_config
```

Y aplica las siguientes medidas:

- **Cambia el puerto por defecto** (por ejemplo, al 2222):  
  ```
  Port 2222
  ```
- **Desactiva el login directo de root:**  
  ```
  PermitRootLogin no
  ```
- **Usa autenticación con clave pública:**  
  ```
  PasswordAuthentication no
  ```
- **Habilita solo los protocolos seguros:**  
  ```
  Protocol 2
  ```

Finalmente, reinicia el servicio:
```bash
sudo systemctl restart ssh
```

---

## Firewall y servicios

Un firewall bien configurado es la primera línea de defensa frente a accesos no deseados.  
En Ubuntu y derivados, **UFW (Uncomplicated Firewall)** simplifica esta tarea:

```bash
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw status
```

Además:
- **Desactiva servicios innecesarios:**
  ```bash
  sudo systemctl disable nombre_servicio
  sudo systemctl stop nombre_servicio
  ```
- **Lista los servicios activos:**
  ```bash
  sudo ss -tuln
  sudo systemctl list-unit-files --type=service
  ```

Cuantos menos servicios en ejecución, menor será la superficie de ataque.

---

## Monitoreo y registros

Un servidor seguro no solo se protege, también **se vigila**.  
Configura herramientas que te alerten ante comportamientos sospechosos.

- **Fail2ban:** bloquea IPs que realizan intentos de acceso fallidos repetidos.  
  ```bash
  sudo apt install fail2ban
  sudo systemctl enable fail2ban
  ```

- **Auditd:** registra eventos importantes del sistema.  
  ```bash
  sudo apt install auditd
  sudo systemctl enable auditd
  ```
  Puedes revisar los logs con:
  ```bash
  sudo aureport -a
  ```

- **Revisión periódica de logs:**
  Los archivos más relevantes se encuentran en `/var/log/`:
  ```
  /var/log/auth.log
  /var/log/syslog
  /var/log/fail2ban.log
  ```

Analizar estos registros te permitirá detectar patrones de ataque o configuraciones inseguras.

---

## Medidas adicionales de hardening

Si quieres ir un paso más allá:

- Instala **AppArmor** o **SELinux** para control de acceso obligatorio (MAC).  
- Configura **logs remotos** o alertas por correo.  
- Implementa **copias de seguridad cifradas** y regulares.  
- Usa **integridad de archivos** con herramientas como `AIDE` o `Tripwire`.

---

## Conclusión

El **hardening en Linux** no es una acción puntual, sino un proceso continuo.  
Aplicar las prácticas básicas que hemos visto —mantener el sistema actualizado, controlar usuarios, asegurar SSH, configurar un firewall y monitorizar los registros— puede marcar la diferencia entre un servidor seguro y uno vulnerable.

Dedicar tiempo a reforzar la seguridad desde el principio te ahorrará muchos problemas en el futuro.  

> 💡 **Recuerda:** la mejor defensa es la prevención.
