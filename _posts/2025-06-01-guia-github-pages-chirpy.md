---
layout: post
title: "Cómo crear una GitHub Pages con el tema Chirpy: paso a paso, errores comunes y soluciones"
date: 2024-06-01 12:00:00 +0200
categories: [guías]
tags: [github-pages, jekyll, chirpy, errores]
---

Crear un sitio web profesional con **GitHub Pages** y el tema **Chirpy para Jekyll** puede parecer simple al principio, pero es común encontrarse con errores que no están bien documentados. Aquí te dejo una guía completa y práctica para tenerlo todo funcionando.

---

## ✅ Requisitos previos

- Cuenta de GitHub
- Tener Git y Ruby instalados si trabajas localmente (opcional)
- Familiaridad con Markdown y commits básicos

---

## 🛠️ Paso 1: Hacer fork del tema

1. Ve a [https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)
2. Haz clic en **Fork**
3. Renombra tu repositorio a `usuario.github.io` (si quieres una página personal)

---

## 📦 Paso 2: Clonar y preparar localmente (opcional)

```bash
git clone git@github.com:tu_usuario/tu_repo.git
cd tu_repo
bash tools/init.sh
```

> Esto limpiará archivos de ejemplo y activará GitHub Actions.

---

## ⚙️ Paso 3: Editar `_config.yml`

Ejemplo básico:

```yaml
lang: es-ES
locale: es-ES
timezone: Europe/Madrid

title: Mi sitio
description: Sitio técnico personal
avatar: /assets/img/avatar.png
favicon:
  icon: /assets/img/favicon.ico
include:
  - assets/img
  - assets/img/favicons
  - assets/img/avatar.png
```

---

## 🧪 Paso 4: Añadir contenido

Crea posts en `_posts/` con este formato:

```markdown
---
layout: post
title: "Título del post"
date: 2024-06-01 12:00:00 +0200
categories: [blog]
tags: [tema1, tema2]
---

Contenido del post aquí.
```

---

## 🎨 Paso 5: Personalizar el avatar y favicon

- Coloca tu imagen de perfil en `assets/img/avatar.png`
- Coloca favicons en `assets/img/favicon.ico` o `assets/img/favicons/`
- Usa [favicon.io](https://favicon.io) para generar archivos `.ico`

---

## 🔄 Paso 6: Hacer commit y push

```bash
git add .
git commit -m "Inicialización del sitio"
git push origin master
```

Esto activará GitHub Actions que generará la rama `gh-pages`.

---

## 🌍 Paso 7: Activar GitHub Pages

1. Ve a `Settings → Pages`
2. Fuente: `gh-pages` y carpeta `/ (root)`
3. Espera unos segundos y accede a:

```
https://usuario.github.io
```

---

## ❗ Errores comunes y soluciones

### 1. `--- layout: home ---` aparece en la página

💥 **Causa:** GitHub Pages intenta mostrar el código fuente directamente  
🛠️ **Solución:** Asegúrate de que GitHub Actions está activado y has hecho `init.sh + commit`

---

### 2. `bash tools/init.sh` da error `$'': command not found`

💥 **Causa:** Los scripts `.sh` tienen finales de línea `CRLF` (Windows)  
🛠️ **Solución:** Ejecuta en Git Bash:

```bash
find tools -type f -name "*.sh" -exec sed -i 's/\r$//' {} +
```

---

### 3. Error `ENOENT: .git/COMMIT_EDITMSG\r`

💥 **Causa:** Husky/Commitlint no soporta rutas con `\r` (Windows)  
🛠️ **Solución temporal:** usar `--no-verify` al hacer commit:

```bash
git commit -m "Mensaje" --no-verify
```

---

### 4. El favicon no se actualiza

💥 **Causa:** El navegador usa `/favicon.ico` por defecto  
🛠️ **Solución:** copia tu imagen como:

```bash
cp assets/img/favicons/favicon.png assets/img/favicon.ico
```

Y agrégala a `include:` en `_config.yml`

---

### 5. HTML-Proofer falla por archivos que no existen

💥 **Causa:** Imágenes como `/assets/img/avatar.png` no están incluidas en la build  
🛠️ **Solución:** Asegúrate de que `_config.yml` tenga:

```yaml
include:
  - assets/img
  - assets/img/avatar.png
  - assets/img/favicon.ico
```

---

## ✅ Resultado

Al final, tendrás un sitio Jekyll potente, moderno, y completamente gestionado con GitHub, ¡sin necesidad de hosting externo!

---

¿Tienes preguntas o errores no mencionados aquí? Escríbeme por GitHub o Twitter y con gusto los agrego a esta guía.
