---
author: "davidalvarezp"
title: "Integración de CI/CD con GitHub Actions en proyectos Hugo"
slug: "ci-cd-github-actions"
date: 2025-10-24
description: "Aprende a configurar pipelines de CI/CD para tu sitio Hugo usando GitHub Actions y automatiza despliegues y pruebas."
tags: ["WebDev", "Hugo", "Automatización", "GitHub"]
categories: ["Dev"]
draft: false
keywords: ["CI/CD", "GitHub Actions", "Hugo", "automatización"]
---

# Integración de CI/CD con GitHub Actions en proyectos Hugo

El desarrollo moderno de sitios web estáticos, como los generados con **Hugo**, se beneficia enormemente de la automatización.  
Configurar un pipeline de **CI/CD (Integración y Despliegue Continuos)** permite que cada cambio que hagas en tu repositorio se construya y publique automáticamente, sin intervención manual.

En este artículo aprenderás a configurar **GitHub Actions** para construir y desplegar tu sitio Hugo en GitHub Pages o cualquier otro servicio compatible.

---

## ¿Por qué usar CI/CD con Hugo?

Cuando desarrollas un blog o documentación técnica, los pasos típicos son:

1. Editar contenido en Markdown.
2. Ejecutar `hugo` localmente para generar el sitio.
3. Subir los archivos generados al servidor o repositorio de hosting.

Con **GitHub Actions**, puedes automatizar completamente ese proceso.  
Cada vez que hagas un `push` o merges una PR, el sitio se construirá y publicará automáticamente.

Ventajas principales:

- Despliegue automático y sin errores manuales  
- Integración directa con GitHub Pages, Netlify o Cloudflare  
- Builds reproducibles en entornos controlados  
- Posibilidad de añadir validaciones, pruebas o linting antes del deploy

---

## Crear el workflow

GitHub Actions usa archivos YAML ubicados en el directorio `.github/workflows/`.  
Crearemos uno llamado `deploy-hugo.yml` con los pasos básicos para compilar y desplegar tu blog.

```yaml
name: Build and Deploy Hugo
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'

      - name: Build site
        run: hugo --minify

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
### Explicación paso a paso

- actions/checkout@v3: descarga el código del repositorio para que el workflow pueda trabajar sobre él.
- peaceiris/actions-hugo@v2: instala Hugo en la versión especificada.
- hugo --minify: genera el sitio estático en la carpeta public/.
- peaceiris/actions-gh-pages@v3: sube automáticamente el contenido generado a la rama gh-pages, usada por GitHub Pages.

---

## Configurar GitHub Pages

1. Ve a la configuración del repositorio (Settings → Pages).
2. En “Source”, selecciona Deploy from a branch.
3. Elige la rama gh-pages y la carpeta raíz /.
4. Guarda los cambios.

Tu sitio estará disponible en https://usuario.github.io/nombre-del-repo/.

> Consejo: Si usas un dominio personalizado, crea un archivo CNAME en la carpeta static/ de tu proyecto con el dominio (por ejemplo, blog.midominio.com).

---

## Personalizar el flujo de despliegue

GitHub Actions es extremadamente flexible. Puedes añadir pasos para mejorar tu pipeline, por ejemplo:

### Validar el código antes del build

```yaml
- name: Lint Markdown
  run: npx markdownlint "**/*.md"
```

### Ejecutar pruebas (si tu sitio las incluye)

```yaml
- name: Run tests
  run: npm test
```

### Notificar por Slack o Discord al completar el deploy
```yaml
- name: Notify deployment
  uses: slackapi/slack-github-action@v1.23.0
  with:
    payload: '{"text":"🚀 Despliegue de Hugo completado con éxito!"}'
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
```

---

## Mantenimiento del workflow

- Actualiza las acciones periódicamente (actions/checkout, actions-hugo, etc.) para mantener compatibilidad y seguridad.
- Usa secrets para tokens y credenciales en lugar de variables públicas.
- Habilita la opción de require approval si quieres validar los despliegues en ramas principales.

---

## Conclusión

Integrar CI/CD con GitHub Actions en tu proyecto Hugo no solo ahorra tiempo, sino que garantiza despliegues consistentes y seguros.
Cada commit se convierte en una versión pública de tu sitio, con un proceso completamente automatizado y controlado desde el repositorio.

> Ahora cada push construirá y desplegará automáticamente tu sitio. ¡Tu blog estará siempre al día y sin esfuerzo!
