---
title: "JavaScript: Desde cero"
description: "JavaScript es el lenguaje que da interactividad a las aplicaciones web y móviles, creando interfaces dinámicas."
date: 2025-09-28 17:57:22
categories:
  [FP, DAM, Programación Multimedia y Dispositivos Móviles, JavaScript]
tags: [JavaScript, DOM, Eventos]
comments: true
---

# ¿Qué es JavaScript?

JavaScript es un lenguaje de programación interpretado, ligero y multiplataforma que se utiliza principalmente para dotar de interactividad a las páginas web.  
Fue creado en 1995 por Brendan Eich y hoy en día es uno de los pilares del desarrollo web moderno junto con HTML y CSS.

---

## Características clave de JavaScript

- **Lenguaje del Navegador**: Se ejecuta directamente en la mayoría de navegadores modernos.
- **Multiparadigma**: Soporta programación orientada a objetos, funcional y basada en eventos.
- **Dinámico**: Permite modificar el contenido y la estructura de una página sin necesidad de recargarla.
- **Amplio Ecosistema**: Tiene un gran número de librerías y frameworks como React, Angular o Vue.

---

## ¿Cómo funciona JavaScript?

1. **Incorpora JavaScript en HTML**:

   ```html
   <script>
     alert("Hola, mundo!");
   </script>
   ```

2. **Variables y Tipos**: Define variables con `let`, `const` o `var`.

   ```javascript
   let nombre = "Ana";
   const edad = 20;
   ```

3. **Funciones**: Bloques de código reutilizables.

   ```javascript
   function saludar(nombre) {
     return "Hola " + nombre;
   }
   ```

4. **Manipulación del DOM**: Permite acceder y modificar elementos de la página.
   ```javascript
   document.getElementById("titulo").innerText = "Texto cambiado";
   ```

---

## Flujo de Trabajo con JavaScript

1. **Escribir el Script** en un archivo `.js`.
2. **Vincularlo al HTML** con la etiqueta `<script src="app.js"></script>`.
3. **Probar en el Navegador** usando la consola de desarrollador.
4. **Iterar y Mejorar** añadiendo eventos, animaciones y lógica para la aplicación.
