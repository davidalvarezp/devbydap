---
author: "davidalvarezp"
title: "Introducción a Terraform: Infraestructura como Código"
slug: "terraform-introduccion"
description: "Aprende a automatizar y gestionar infraestructura en la nube con Terraform mediante la práctica de Infraestructura como Código (IaC)."
tags: ["Terraform", "IaC", "DevOps", "Cloud"]
categories: ["Dev", "SysAdmin"]
date: "2025-10-30"
keywords: ["terraform", "infraestructura como código", "IaC", "cloud", "automatización"]
draft: false
---
 
# Introducción a Terraform: Infraestructura como Código

Terraform es una herramienta de Infraestructura como Código (IaC) que permite definir, provisionar y gestionar infraestructura en la nube de forma declarativa. Con Terraform puedes crear recursos en AWS, Azure, Google Cloud y otros proveedores de manera consistente y reproducible.

En este artículo veremos cómo instalar Terraform, crear un proyecto básico y desplegar recursos en la nube.

---
## ¿Qué es Infraestructura como Código?

La Infraestructura como Código permite gestionar infraestructura de manera similar al software, con ventajas como:

- Versionamiento y control de cambios
- Reproducibilidad de entornos
- Automatización y reducción de errores manuales
- Integración con pipelines CI/CD

Terraform utiliza un lenguaje declarativo llamado HCL (HashiCorp Configuration Language) para describir los recursos que necesitamos.

---
## Instalación de Terraform

En sistemas Linux puedes instalar Terraform siguiendo estos pasos:

```bash
sudo apt update
sudo apt install wget unzip -y
wget https://releases.hashicorp.com/terraform/1.6.0/terraform_1.6.0_linux_amd64.zip
unzip terraform_1.6.0_linux_amd64.zip
sudo mv terraform /usr/local/bin/
terraform version .
```
> Consejo: Terraform se actualiza frecuentemente, revisa la última versión oficial en la web de HashiCorp


---
## Primer proyecto con Terraform

1. Crea un directorio para tu proyecto:

```bash
mkdir terraform-demo
cd terraform-demo
```

2. Crea un archivo main.tf con el siguiente contenido para desplegar un recurso simple, por ejemplo, un bucket en AWS S3:

```hcl
provider "aws" {
 region = "us-east-1"
}

resource "aws_s3_bucket" "mi_bucket" {
 bucket = "terraform-demo-bucket-12345"
 acl = "private"
}
```

3. Inicializa el proyecto:

```bash
terraform init
```

4. Previsualiza los cambios que se aplicarán:

```bash
terraform plan
```

5. Aplica la configuración:

```bash
terraform apply
```

- Terraform creará el bucket en tu cuenta de AWS siguiendo exactamente lo definido en main.tf.

---
## Gestión y mantenimiento de infraestructura

- Actualizar recursos: Modifica tu main.tf y vuelve a ejecutar terraform apply.
- Eliminar infraestructura:

```bash
terraform destroy
```

- Estado de la infraestructura: Terraform mantiene un archivo terraform.tfstate para rastrear los recursos. Nunca lo modifiques manualmente.

---
## Buenas prácticas

- Versionar el código en Git
- Usar workspaces para separar entornos (dev, staging, prod)
- Mantener variables sensibles en archivos .tfvars y no en el repositorio
- Revisar cambios con terraform plan antes de aplicar

---
## Conclusión

Terraform simplifica la gestión de infraestructura y permite integrar prácticas de DevOps de manera más eficiente y segura.
Con un poco de práctica, podrás:

- Automatizar despliegues en múltiples proveedores
- Mantener entornos consistentes y reproducibles
- Reducir errores manuales y optimizar tu flujo de trabajo

> Con Terraform, tu infraestructura se convierte en código que evoluciona contigo.
