---
layout: post
title: "Mi primer post"
date: 2024-06-01 10:00:00 +0200
categories: [blog]
tags: [inicio, chirpy]
---

¡Hola mundo!

Este es mi primer post usando el tema **Chirpy** para Jekyll. Aquí irán los tutoriales, proyectos y más ideas.

Puedes usar **Markdown** para dar formato al contenido.

```ruby
puts "Hola desde Jekyll"

---

## ✅ ¿Qué hace cada campo?

- `layout: post` → obligatorio para que se renderice correctamente
- `title:` → el título visible
- `date:` → fecha y hora (formato ISO)
- `categories:` → organiza las entradas (afecta URLs y menús)
- `tags:` → para búsquedas o navegación por temas

---

## 🚀 Después de añadir el post

### Si trabajas localmente:
```bash
bundle exec jekyll serve
```

## Si usas GitHub Pages:

git add _posts/2024-06-01-mi-primer-post.md
git commit -m "Nuevo post: Mi primer post"
git push origin master
