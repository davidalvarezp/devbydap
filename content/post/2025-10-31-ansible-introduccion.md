---
author: "davidalvarezp"
title: "Introducción a Ansible: Automatización de configuración"
slug: "ansible-introduccion"
description: "Aprende a automatizar la configuración y administración de servidores con Ansible, usando playbooks y roles para entornos reproducibles."
tags: ["Ansible", "Automatización", "DevOps"]
categories: ["SysAdmin"]
date: "2025-10-31"
keywords: ["ansible", "automatización", "playbooks", "roles", "configuración de servidores"]
draft: false
---

# Introducción a Ansible: Automatización de configuración

Ansible es una herramienta de automatización de configuración y administración de sistemas que permite aplicar cambios de manera repetible y sin intervención manual.
Con Ansible puedes gestionar servidores, instalar software, ejecutar tareas y mantener entornos consistentes.

En esta entrada veremos cómo instalar Ansible, crear playbooks básicos y ejecutar tareas automatizadas en tus servidores.

---
## ¿Qué es Ansible y cómo funciona?

Ansible utiliza un enfoque agente-less, es decir, no requiere instalar software adicional en los servidores administrados.
Se conecta vía SSH y ejecuta tareas definidas en playbooks, escritos en YAML.

Ventajas principales:
- No requiere agentes en los servidores
- Fácil de aprender y mantener
- Permite automatizar despliegues complejos
- Integración con CI/CD y otras herramientas DevOps

---
## Instalación de Ansible

En Ubuntu/Debian:

```bash
sudo apt update
sudo apt install ansible -y
ansible --version
```

Para comprobar la conectividad con un host remoto:

```bash
ansible all -i "192.168.1.10," -m ping
```

> Nota: La coma al final de la IP es necesaria para indicar un host individual.

---
## Primer playbook

Crea un archivo playbook.yml para instalar Nginx en un servidor remoto:

```yaml
- name: Instalar Nginx en servidores
    hosts: all
    become: yes
    tasks:
- name: Actualizar paquetes
    apt:
    update_cache: yes

- name: Instalar Nginx
    apt:
    name: nginx
    state: present
```

Ejecuta el playbook con:

```bash
ansible-playbook -i "192.168.1.10," playbook.yml
```

---
## Roles y modularidad

Los roles permiten organizar tareas, variables y archivos de manera reutilizable:

```bash
ansible-galaxy init nginx_role
```

Dentro de nginx_role, podrás definir:

- tasks/main.yml
- handlers/main.yml
- templates/
- vars/main.yml

Luego puedes incluir el role en tu playbook para aplicar la configuración en cualquier host.

---
## Buenas prácticas

- Versionar playbooks y roles en Git
- Usar inventarios separados por entornos
- Comprobar cambios con ansible-playbook --check antes de aplicarlos
- Documentar variables y roles para mantener claridad

---
## Conclusión

Con Ansible, la administración de servidores y la automatización de tareas repetitivas se vuelve sencilla y escalable.
Al dominar playbooks y roles podrás:

- Configurar múltiples servidores simultáneamente
- Mantener consistencia entre entornos
- Reducir errores humanos y tiempo de operación

> Ansible transforma la infraestructura en un entorno reproducible y confiable sin complicaciones.
