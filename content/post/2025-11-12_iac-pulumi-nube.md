---
author: "davidalvarezp"
title: "Infraestructura como código con Pulumi en la nube"
slug: "iac-pulumi-nube"
description: "Aprende a gestionar infraestructura en la nube usando Pulumi con código en TypeScript para despliegues reproducibles y seguros."
tags: ["Pulumi", "IaC", "AWS", "DevOps"]
categories: ["Dev"]
draft: false
keywords: ["pulumi", "iac", "infraestructura", "cloud", "devops"]
date: "2025-11-12"
---

# Infraestructura como código con Pulumi en la nube

Pulumi permite definir infraestructura en la nube usando **lenguajes de programación modernos** como TypeScript o Python, facilitando despliegues reproducibles y versionados.

## Instalación de Pulumi

```bash
curl -fsSL https://get.pulumi.com | sh
pulumi version
```

## Crear proyecto

```bash
pulumi new typescript -n mi-infraestructura
```

## Ejemplo de stack en AWS

```typescript
import * as pulumi from "@pulumi/pulumi";
import * as aws from "@pulumi/aws";

const bucket = new aws.s3.Bucket("mi-bucket", {
    versioning: { enabled: true }
});
export const bucketName = bucket.id;
```

## Buenas prácticas

* Versionar código en Git
* Separar entornos dev/prod con stacks diferentes
* Integrar con CI/CD para despliegues automáticos
* Revisar cambios antes de aplicar con `pulumi preview`

## Conclusión

Pulumi permite **gestionar infraestructura como código con seguridad y reproducibilidad**, integrándose con flujos DevOps modernos.
