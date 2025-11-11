---
author: "davidalvarezp"
title: "Seguridad avanzada en Linux con AppArmor y SELinux"
slug: "seguridad-linux-apparmor-selinux"
description: "Aprende a proteger servidores Linux usando AppArmor y SELinux, configurando políticas de seguridad y control de acceso avanzadas."
tags: ["Linux", "Seguridad", "AppArmor", "SELinux"]
categories: ["SysAdmin"]
draft: false
keywords: ["linux", "apparmor", "selinux", "hardening", "seguridad"]
date: "2025-11-08"
---

# Seguridad avanzada en Linux con AppArmor y SELinux

Linux ofrece mecanismos avanzados de control de acceso como **AppArmor** y **SELinux**, que permiten restringir la ejecución de procesos y el acceso a archivos sensibles. En este artículo exploraremos su configuración y buenas prácticas.

## AppArmor

AppArmor aplica perfiles de seguridad a procesos individuales, limitando qué recursos pueden usar.

### Instalación y activación

```bash
sudo apt install apparmor apparmor-utils -y
sudo systemctl enable apparmor
sudo systemctl start apparmor
sudo aa-status
```

### Configuración de perfiles

* Crear un perfil personalizado:

```bash
sudo aa-genprof /usr/bin/mi-aplicacion
sudo aa-enforce /etc/apparmor.d/mi-aplicacion
```

* Monitorear violaciones con `dmesg` o `/var/log/syslog`

## SELinux

SELinux proporciona **Mandatory Access Control (MAC)** para un control granular sobre procesos y recursos.

### Instalación y estado

```bash
sudo apt install selinux-basics selinux-policy-default -y
sudo selinux-activate
sestatus
```

### Modos de SELinux

* Enforcing: aplica políticas estrictas
* Permissive: registra violaciones pero no bloquea
* Disabled: desactiva SELinux

### Políticas y contextos

* Visualizar contextos: `ls -Z /etc/passwd`
* Cambiar contexto: `chcon -t httpd_sys_content_t /var/www/html`

## Buenas prácticas

* Mantener perfiles actualizados y revisados periódicamente
* Auditar logs para detectar violaciones
* Combinar con firewall y hardening adicional
* Evitar deshabilitar SELinux a menos que sea estrictamente necesario

## Conclusión

Combinando AppArmor y SELinux, se logra un **entorno de ejecución controlado**, reduciendo riesgos de vulnerabilidades y exploits.
