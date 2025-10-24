<img align="center" alt="banner" src="imgs/banner.png">

# devbydap ([dev.davidalvarezp.com](https://dev.davidalvarezp.com))

> A modern, lightweight and fully open-source technical blog focused on **Cybersecurity**, **System Administration**, and **Web Development**, built entirely in **Hugo** using the [Dev](https://github.com/davidalvarezp/dev-theme) theme, based on [Stack](https://github.com/CaiJimmy/hugo-theme-stack).

![Preview](imgs/preview.png)

---

## 🚀 Overview

**devbydap** is a knowledge-sharing platform created by professionals passionate about technology, security, and development.

The project aims to become a **Spanish-language reference blog** for cybersecurity, system administration, and web development — offering well-written, practical, and transparent articles for the entire community.

---

## 🧠 Key Features

- Built with **[Hugo](https://gohugo.io/)** (fast static site generator)
- Powered by the **Dev Theme** by davidalvarezp & CaiJimmy
- Fully **open-source** and modular
- **Responsive** and optimized for mobile devices
- **Dark/Light mode** and minimalist design
- **SEO-friendly** structure
- Support for **syntax highlighting** and code snippets
- Markdown-based content

---

## 🏗️ Project Structure

```
.
├── archetypes/           # Hugo content archetypes
├── content/
│   ├── pages/            # Blog pages (Markdown)
│   └── posts/            # Blog posts (Markdown)
├── layouts/              # Custom layouts and partials
├── static/               # Static assets (images, CSS, JS)
├── themes/               # Hugo theme
├── config.toml           # Hugo configuration
├── LICENSE               # License
└── README.md             # This file
```

---

## 🧩 Installation & Usage

### 1️⃣ Clone the repository

```bash
git clone https://github.com/davidalvarezp/dev-theme.git
cd dev-theme
```

### 2️⃣ Install the theme

```bash
git submodule update --init --recursive
```

### 3️⃣ Run the local development server

```bash
hugo server -D
```

The site will be available at:  
👉 [http://localhost:1313](http://localhost:1313)

---

## 🔧 Configuration

Edit your `config.toml` (or `config.yaml`) to adjust:

- `baseURL` → your deployment URL (e.g., https://dev.davidalvarezp.com)
- `title`, `languageCode`, `author`, etc.
- Analytics and Search Console meta tags (should add in `layouts/partials/head-custom.html`)

Example:

```toml
baseURL = "https://dev.davidalvarezp.com"
languageCode = "es-ES"
title = "devbydap"
theme = "dev-theme"
```

---

## 🧰 Development Notes

To customize meta tags or tracking codes:
- Create or edit `layouts/partials/head-custom.html`
- Insert Search Console or Google Analytics scripts
- Rebuild with `hugo --minify`

---

## 📦 Deployment

You can deploy the site on:
- [Netlify](https://www.netlify.com/)
- [Vercel](https://vercel.com/)
- [Cloudflare Pages](https://pages.cloudflare.com/)

Example (Netlify):

```bash
netlify deploy --prod
```

---

## ✍️ Contributing

We welcome contributions from the community!  
If you want to add a new article, fix a bug, or improve the site:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-post`)
3. Commit your changes
4. Push and open a Pull Request

---

## 🧑‍💻 Authors

- **davidalvarezp** – Founder  
  [https://davidalvarezp.com](https://davidalvarezp.com)

With contributions from developers and security enthusiasts.  

---

## 🛡️ License

The **Hugo theme used in this project (“Dev”)** is a derivative of the Stack theme by CaiJimmy  
and is licensed under the **GNU General Public License v3.0**.  
You are free to fork, modify, and redistribute the theme under the terms of the GPLv3.

However, **all written content, blog posts, and original media** published on  
[dev.davidalvarezp.com](https://dev.davidalvarezp.com) are **copyright © 2025 davidalvarezp**  
and **may not be reused, redistributed, or reproduced** without explicit permission from the author.

In summary:
- 🎨 Theme (“Dev”, derivative of "Stack") → GNU GPLv3  
- 📝 Content → All Rights Reserved (**davidalvarezp**)

---

## 🌐 Links

- 🌍 Website: [https://dev.davidalvarezp.com](https://dev.davidalvarezp.com)
- 💼 Portfolio: [https://davidalvarezp.com](https://davidalvarezp.com)
- 🐙 GitHub: [@davidalvarezp](https://github.com/davidalvarezp)
- 🐦 Twitter: [@davidalvarezp_](https://twitter.com/devbydap)

---

> _“Knowledge is meant to be shared — not stored.”_  
> — devbydap Team
