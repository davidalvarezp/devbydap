---
author: "davidalvarezp"
title: "Introducción a SvelteKit: crea tu primer proyecto"
slug: "sveltekit-introduccion"
date: 2025-10-21
description: "Aprende a crear tu primer proyecto con SvelteKit y descubre cómo construir aplicaciones web modernas de forma rápida y eficiente."
tags: ["WebDev", "Frontend", "JavaScript"]
categories: ["Dev"]
draft: false
keywords: ["SvelteKit", "web development", "frontend", "tutorial"]
---
 
# Introducción a SvelteKit: crea tu primer proyecto

**SvelteKit** es un framework moderno para construir aplicaciones web rápidas, ligeras y optimizadas.  
Basado en **Svelte**, aprovecha la compilación en tiempo de construcción (en lugar de en tiempo de ejecución) para generar aplicaciones altamente eficientes.

En este artículo aprenderás a crear tu primer proyecto con SvelteKit paso a paso, entendiendo su estructura y filosofía.

---

## Instala Node.js

Antes de empezar, asegúrate de tener instalado **Node.js** y **npm** (Node Package Manager), ya que son necesarios para crear y ejecutar proyectos con SvelteKit.

Comprueba tus versiones con:

```bash
node -v
npm -v
```

Si no los tienes, puedes descargar Node.js desde [nodejs.org](https://nodejs.org).  
Te recomiendo instalar la versión LTS (Long Term Support) para mayor estabilidad.

---

## Crea un nuevo proyecto con SvelteKit

SvelteKit incluye un asistente oficial que te permite crear un nuevo proyecto con una configuración básica en pocos segundos.

Ejecuta en tu terminal:

```bash
npm create svelte@latest my-app
cd my-app
npm install
npm run dev
```

Esto hará lo siguiente:

1. Creará un nuevo proyecto llamado **my-app**.  
2. Instalará las dependencias necesarias.  
3. Iniciará un servidor de desarrollo en `http://localhost:5173` (o el puerto disponible).

Abre esa dirección en tu navegador y verás la página de inicio de SvelteKit.

---

## Estructura del proyecto

Una vez creado el proyecto, encontrarás una estructura similar a esta:

```
my-app/
├── src/
│   ├── routes/
│   ├── lib/
│   └── app.html
├── static/
├── package.json
└── svelte.config.js
```

### `/src/routes`
Aquí defines las **rutas y páginas** de tu aplicación.  
Cada archivo `.svelte` dentro de esta carpeta corresponde a una ruta.

Por ejemplo, `src/routes/about/+page.svelte` creará la página `/about`.

### `/src/lib`
Contiene **componentes reutilizables**, como botones, menús o layouts.

### `/static`
Guarda **recursos estáticos** como imágenes, fuentes o íconos.  
Todo lo que pongas aquí se servirá directamente desde la raíz del sitio.

---

## Crea tu primer componente

Ahora que ya tienes el proyecto funcionando, vamos a crear un componente simple.

Edita el archivo `src/routes/+page.svelte` y reemplázalo con el siguiente contenido:

```svelte
<script>
  let nombre = 'David';
</script>

<h1>Hola {nombre}, ¡bienvenido a SvelteKit!</h1>
<p>Tu primera app ya está corriendo localmente 🚀</p>
```

Guarda el archivo y verás el cambio reflejado en tiempo real gracias al **Hot Module Reloading (HMR)** integrado.

---

## ¿Por qué elegir SvelteKit?

Algunas ventajas que hacen que SvelteKit destaque frente a otros frameworks como React o Next.js:

- **Renderizado híbrido** (SSR + CSR + SSG) sin configuración extra.
- **Rendimiento superior** gracias a la compilación de componentes.
- **Menor tamaño de bundle**, lo que se traduce en tiempos de carga más rápidos.
- **Excelente DX (Developer Experience)**: sintaxis limpia, feedback instantáneo y soporte moderno.
- **Integración fácil** con adaptadores para Vercel, Netlify, Cloudflare y más.

---

## Conclusión

Has creado tu primer proyecto con **SvelteKit**, entendido su estructura y creado un componente básico.  
Este framework es ideal para desarrolladores que buscan **velocidad, simplicidad y rendimiento** en sus aplicaciones web.

En próximos artículos profundizaremos en temas como **rutas dinámicas**, **stores**, **formularios** y **despliegue en producción**.

> **Consejo:** explora la documentación oficial en [kit.svelte.dev](https://kit.svelte.dev) para descubrir todo su potencial.
