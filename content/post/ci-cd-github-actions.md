---
author: "davidalvarezp"
title: "Integración de CI/CD con GitHub Actions en proyectos Hugo"
slug: "ci-cd-github-actions"
date: 2025-10-22
description: "Aprende a configurar pipelines de CI/CD para tu sitio Hugo usando GitHub Actions y automatiza despliegues y pruebas."
tags: ["WebDev", "Hugo", "Automatización", "GitHub"]
categories: ["Dev"]
draft: false
keywords: ["CI/CD", "GitHub Actions", "Hugo", "automatización"]
---

# Integración de CI/CD con GitHub Actions en proyectos Hugo

Automatiza el build y despliegue de tu blog Hugo usando GitHub Actions.

## Crear workflow
```yaml
name: Build and Deploy Hugo
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
      - name: Build
        run: hugo --minify
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
```

> Ahora cada push construirá y desplegará automáticamente tu sitio.
