---
author: "davidalvarezp"
title: "Introducción a SvelteKit: crea tu primer proyecto"
slug: "sveltekit-introduccion"
date: 2025-10-20
description: "Aprende a crear tu primer proyecto con SvelteKit y descubre cómo construir aplicaciones web modernas de forma rápida y eficiente."
tags: ["WebDev", "Frontend", "JavaScript"]
categories: ["Dev"]
draft: false
keywords: ["SvelteKit", "web development", "frontend", "tutorial"]
---

# Introducción a SvelteKit: crea tu primer proyecto

SvelteKit es un framework moderno para construir aplicaciones web rápidas y optimizadas.

## Instala Node.js
```bash
node -v
npm -v
```

## Crea un nuevo proyecto
```bash
npm create svelte@latest my-app
cd my-app
npm install
npm run dev
```

## Estructura del proyecto
- `/src/routes` → define páginas
- `/src/lib` → componentes reutilizables
- `/static` → assets

## Primer componente
```svelte
<script>
  let nombre = 'David';
</script>

<h1>Hola {nombre}, bienvenido a SvelteKit!</h1>
```

> ¡Listo! Ahora tienes tu primer proyecto corriendo localmente.
