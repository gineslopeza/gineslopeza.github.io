---
title: "JavaScript: Desde cero"
description: "JavaScript es el lenguaje que da interactividad a las aplicaciones web y móviles, creando interfaces dinámicas."
date: 2025-09-28 17:57:22
categories: [DAM, Programación Multimedia y Dispositivos Móviles, JavaScript]
tags: [JavaScript, DOM, Eventos]
comments: true
---

## ¿Qué es JavaScript?

JavaScript es un lenguaje de programación interpretado, ligero y multiplataforma que se utiliza principalmente para dotar de interactividad a las páginas web.
Fue creado en 1995 por Brendan Eich y hoy en día es uno de los pilares del desarrollo web moderno junto con HTML y CSS.

## Características clave de JavaScript

- **Lenguaje del Navegador**: Se ejecuta directamente en la mayoría de navegadores modernos.
- **Multiparadigma**: Soporta programación orientada a objetos, funcional y basada en eventos.
- **Dinámico**: Permite modificar el contenido y la estructura de una página sin necesidad de recargarla.
- **Amplio Ecosistema**: Tiene un gran número de librerías y frameworks como React, Angular o Vue.

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

## Flujo de Trabajo con JavaScript

1. **Escribir el Script** en un archivo `.js`.
2. **Vincularlo al HTML** con la etiqueta `<script src="app.js"></script>`.
3. **Probar en el Navegador** usando la consola de desarrollador.
4. **Iterar y Mejorar** añadiendo eventos, animaciones y lógica para la aplicación.

## Promises

Una **Promesa** en JavaScript es un **objeto** que representa un valor que puede estar disponible **ahora, en el futuro o nunca**.

En otras palabras:  
Una promesa conecta dos tipos de código:

- **Producing code** → el código que genera el resultado (puede tardar).
- **Consuming code** → el código que necesita el resultado (tiene que esperar).

**Frase clave:** Te prometo que habrá un resultado, pero puede que tarde.

```js
let myPromise = new Promise(function (myResolve, myReject) {
  // "Producing Code" (puede tardar)

  myResolve(); // cuando tiene éxito
  myReject(); // cuando ocurre un error
});

// "Consuming Code" (espera la promesa)
myPromise.then(
  function (value) {
    /* código si éxito */
  },
  function (error) {
    /* código si error */
  }
);
```

- myResolve(value) → se llama cuando la operación termina bien.
- myReject(error) → se llama cuando la operación falla.

### Estados de una Promesa

Una promesa puede estar en 3 estados:

Estado Significado Resultado
pending En proceso, esperando undefined
fulfilled Se resolvió correctamente Un valor
rejected Hubo un error Un objeto error

⚠️ No podemos acceder directamente a .state o .result.

Debemos usar métodos como .then() o .catch().

El método **`.catch()`** se usa en una **promesa** para manejar errores.

- Cuando una promesa **se rechaza** (`reject`) o ocurre un fallo en la ejecución, `.catch()` captura ese error.
- Es el equivalente a un **"try...catch"** pero aplicado a promesas.

```js
miPromesa
  .then((resultado) => {
    // código si éxito
  })
  .catch((error) => {
    // código si ocurre un error
  });
```

```js
let promesa = new Promise((resolve, reject) => {
  let correcto = false;

  if (correcto) {
    resolve("Todo salió bien ✅");
  } else {
    reject("Ocurrió un error ❌");
  }

  promesa
    .then((valor) => console.log(valor))
    .catch((err) => console.error("Error capturado:", err));
});
```

## Async y Await

`async` y `await` hacen que trabajar con **promesas** sea más sencillo.

- **`async`** hace que una función devuelva siempre una promesa.
- **`await`** hace que la ejecución espere a que una promesa se resuelva.

### Async

- La palabra clave **`async`** se usa para declarar una función **asíncrona**.
- Una función asíncrona **devuelve siempre una promesa**, aunque dentro escribamos código que parece "normal".

```js
async function saludo() {
  return "Hola!";
}

saludo().then((msg) => console.log(msg));
// Salida: Hola!
```

Esto es equivalente a:

```js
function myFunction() {
  return Promise.resolve("Hello");
}
```

Cómo usar la promesa

```js
myFunction().then(
  function (value) {
    /* código si tiene éxito */
  },
  function (error) {
    /* código si hay un error */
  }
);
```

### Await

La palabra clave await se usa dentro de una función async.

Sirve para esperar a que una promesa se resuelva antes de continuar.

Mientras tanto, JavaScript no bloquea el resto del programa, pero dentro de esa función sí "pausa" hasta tener el resultado.

```js
async function myDisplay() {
  let myPromise = new Promise(function (resolve, reject) {
    resolve("Hola Mundo");
  });
  document.getElementById("demo").innerHTML = await myPromise;
}
myDisplay();
```

Los parámetros **(resolve, reject)** están predefinidos en JavaScript.

Normalmente no necesitamos **reject**, solo **resolve**.

## 1. ¿Qué es una API?

Las Interfaces de Programacion de Aplicaciones (APIs, Application Programming Interface, por sus siglas en inglés) son construcciones disponibles en los lenguajes de programación que permiten a los desarrolladores crear funcionalidades complejas de una manera simple. Estas abstraen el código más complejo para proveer una sintaxis más fácil de usar en su lugar.

En resumen son un conjunto de **reglas, funciones y protocolos** que permiten que dos programas diferentes se comuniquen entre sí.

En informática, una API define un **conjunto de reglas** para solicitar datos o servicios sin necesidad de conocer cómo está programado el sistema por dentro.

Una API es como un **puente** que conecta dos sistemas para que puedan intercambiar información o servicios de forma ordenada.

### 1.1 ¿Por qué existen las APIs?

- Para **reutilizar servicios** ya creados (ejemplo: usar Google Maps en una web sin programar un mapa desde cero).
- Para que distintos sistemas puedan **interactuar entre sí** sin necesidad de conocer su funcionamiento interno.
- Para **estandarizar** la forma en que se piden y se entregan datos.

### 1.3 Funcionamiento de una API web

En la web, las APIs funcionan mediante **peticiones HTTP**.
Los métodos más comunes son:

- **GET** → solicitar datos (ej. leer información).
- **POST** → enviar datos (ej. crear algo nuevo).
- **PUT** → actualizar datos existentes.
- **DELETE** → eliminar datos.

La respuesta más habitual es en **formato JSON**, un estándar que organiza la información de forma clara y legible por JavaScript.

En el ámbito de Internet, las APIs permiten:

- Pedir datos a un servidor remoto.
- Enviar información a una base de datos.
- Integrar servicios externos (ejemplo: iniciar sesión con Google, mostrar tweets en una página, consultar el tiempo, etc.).

## Tipos de API y su funcionamiento

### 1.2 Tipos de API

Las APIs pueden clasificarse según su **uso** y **forma de acceso**:

- **APIs públicas (Open APIs)**
  Accesibles para cualquier desarrollador. Ejemplo: la API de Pokémon o de The Cat API.

- **APIs privadas**
  Se usan dentro de una empresa u organización para conectar servicios internos.

- **APIs de socios (Partner APIs)**
  Limitadas a colaboradores específicos con permisos de acceso.

- **APIs locales (bibliotecas o frameworks)**
  No usan Internet. Ejemplo: la API de JavaScript para manipular el DOM (`document.querySelector`).

---

### 1.2.1 ¿Qué es una API REST?

**REST (Representational State Transfer)** es el estilo más usado en APIs web modernas.
Sus características principales son:

- Se basa en **peticiones HTTP** (GET, POST, PUT, DELETE).
- Utiliza **URLs** para identificar recursos (ejemplo: `/usuarios/5` → el usuario con id=5).
- Normalmente responde en **JSON**.
- Es **stateless** (cada petición es independiente, no guarda estado en el servidor).

**Ejemplo RESTful:**

GET /usuarios → obtener todos los usuarios

GET /usuarios/1 → obtener usuario con id 1

POST /usuarios → crear nuevo usuario

PUT /usuarios/1 → actualizar usuario con id 1

DELETE /usuarios/1 → borrar usuario con id 1

### 1.3. CRUD en APIs

El término **CRUD** describe las 4 operaciones básicas que cualquier API debe permitir sobre los datos:

- **C**reate → Crear (POST)
- **R**ead → Leer (GET)
- **U**pdate → Actualizar (PUT/PATCH)
- **D**elete → Eliminar (DELETE)

Ejemplo:
En una API de biblioteca, el recurso "libros" tendría estas operaciones:

- `POST /libros` → Añadir un libro.
- `GET /libros` → Ver todos los libros.
- `PUT /libros/2` → Modificar el libro con id 2.
- `DELETE /libros/2` → Eliminar el libro con id 2.

---

### 1.4. ¿Siempre son mediante URL?

No. Aunque las más comunes (REST, GraphQL, SOAP) suelen usar Internet y URLs, existen otros tipos:

- **REST APIs** → usan HTTP y URLs (lo más común).
- **SOAP** → protocolo basado en XML (más complejo, usado en banca y servicios antiguos).
- **GraphQL** → permite pedir exactamente los datos que necesitas con una sola consulta.
- **gRPC** → comunicación rápida entre servicios (muy usado en microservicios).
- **APIs locales** → como las APIs del sistema operativo (ej: API de Windows para abrir archivos).
- **APIs de librerías** → por ejemplo, la API de JavaScript para manipular el DOM o la API de Math.

---

### 1.5. ¿Cómo se programan las APIs?

En el lado del **servidor** se programa la lógica que responderá a las peticiones.
Ejemplo en Node.js con Express:

```js
// Ejemplo de API REST en Node.js
const express = require("express");
const app = express();
app.use(express.json());

let usuarios = [{ id: 1, nombre: "Ana" }];

// R (Read) - obtener usuarios
app.get("/usuarios", (req, res) => {
  res.json(usuarios);
});

// C (Create) - añadir usuario
app.post("/usuarios", (req, res) => {
  const nuevo = { id: usuarios.length + 1, nombre: req.body.nombre };
  usuarios.push(nuevo);
  res.json(nuevo);
});

// U (Update) - actualizar usuario
app.put("/usuarios/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const usuario = usuarios.find((u) => u.id === id);
  usuario.nombre = req.body.nombre;
  res.json(usuario);
});

// D (Delete) - eliminar usuario
app.delete("/usuarios/:id", (req, res) => {
  usuarios = usuarios.filter((u) => u.id != req.params.id);
  res.json({ mensaje: "Usuario eliminado" });
});

app.listen(3000, () => console.log("API en http://localhost:3000"));
```

### 1.6 ¿Cómo se usan en JavaScript (cliente)?

En JavaScript utilizamos la función `fetch()` para realizar peticiones a una API.

```js
// Obtener todos los usuarios (GET)
async function obtenerUsuarios() {
  const res = await fetch("http://localhost:3000/usuarios");
  const datos = await res.json();
  console.log(datos);
}

// Crear un nuevo usuario (POST)
async function crearUsuario() {
  const res = await fetch("http://localhost:3000/usuarios", {
    method: "POST",<!DOCTYPE html>
```

```js
async function getPokemon(nombre) {
  try {
    const respuesta = await fetch(
      `https://pokeapi.co/api/v2/pokemon/${nombre}`
    );
    if (!respuesta.ok) {
      throw new Error("Error en la petición: " + respuesta.status);
    }

    const datos = await respuesta.json();

    console.log("Nombre:", datos.name);
    console.log("Altura:", datos.height);
    console.log("Peso:", datos.weight);
    console.log(
      "Habilidades:",
      datos.abilities.map((a) => a.ability.name)
    );
  } catch (error) {
    console.error("Ocurrió un error:", error.message);
  }
}

getPokemon("charmander");
```

## ¿Qué es la paginación?

La **paginación** consiste en dividir un conjunto grande de resultados en **páginas** más pequeñas.  
Ventajas:

- Reduce el tiempo de carga y el consumo de datos.
- Mejora la experiencia de usuario (UI más ágil).
- Facilita recorrer resultados de forma ordenada.

En muchas APIs, la paginación se controla con **parámetros de consulta** (query params) como `?page=2`, `?limit=20`, etc.

La API que usaremos
**Rick and Morty API (personajes)**  
Endpoint base: `https://rickandmortyapi.com/api/character`

Respuesta (resumen):

```json
{
  "info": {
    "count": 826,
    "pages": 42,
    "next": "https://rickandmortyapi.com/api/character?page=2",
    "prev": null
  },
  "results": [
    /* 20 personajes por página */
  ]
}
```

Claves:

info.pages → total de páginas.

info.next / info.prev → enlaces listos para ir a la siguiente/anterior página.

results → los elementos de la página actual (20 por defecto).

### Estrategias de paginación comunes

Por número de página: ?page=N (lo usaremos aquí).

Por desplazamiento/limit: ?offset=40&limit=20.

Por cursor: el servidor devuelve un cursor/next para pedir la siguiente “ventana”.

En esta API, la estrategia es por número de página y, además, te da los enlaces next/prev, lo que simplifica el código.

## Actividad: Paginación con `fetch` y renderizado de “cards” (Rick and Morty API)

### 1. Descripción

Implementa, exclusivamente con **JavaScript**, una pequeña aplicación web que:

1. Obtiene personajes desde la **Rick and Morty API** mediante `fetch`.
2. Muestra los resultados en forma de **cards simples** (imagen, nombre, estado).
3. Permite navegar por las páginas con botones **Anterior** / **Siguiente**.
4. Gestiona estados básicos: deshabilitar botones cuando corresponda y mostrar errores.

> El **HTML** y el **CSS** te los proporciona el profesor. Debes trabajar únicamente el archivo **`app.js`** (o el `<script>` dentro del HTML, según se te indique).

---

### 2. Objetivos de aprendizaje

- Comprender la **paginación** en una API pública.
- Usar **`fetch`**, **promesas** y **`async/await`** para consumir datos.
- Manipular el **DOM** para renderizar listas de elementos.
- Implementar controles de interfaz (navegación y deshabilitado de botones).
- Manejar errores de red o de respuesta de forma adecuada.

---

### 3. Requisitos y restricciones

- **No** se permite usar librerías o frameworks (React, jQuery, etc.).
- **No** modifiques el HTML/CSS entregado (salvo que el profesor lo autorice).
- Código **propio y original** (no generadores automáticos).
- La aplicación debe funcionar en un navegador moderno sin configuración adicional.

**Ids esperados en el HTML (consulta el archivo entregado):**

- Contenedor de cards: `#grid`
- Botones: `#prev` y `#next`
- Etiqueta de página: `#pageLabel`

---

### 4. API a utilizar

Endpoint base de personajes: [https://rickandmortyapi.com/api/character?page=N](https://rickandmortyapi.com/api/character?page=N)

Respuesta relevante:

- `info.pages`: número total de páginas.
- `results`: array con los personajes de esa página.
- Campos útiles por personaje: `name`, `status`, `image`.

---

### 5. Tareas paso a paso

#### Paso 1 — Preparación del estado

- Declara variables para el estado mínimo:
  - `currentPage` (empieza en `1`).
  - `totalPages` (inicialízala a `1`).

#### Paso 2 — Función de obtención (`fetchPage`)

- Crea una función **asíncrona** `fetchPage(page)` que:
  1. Haga `fetch` a `https://rickandmortyapi.com/api/character?page=${page}`.
  2. Compruebe `respuesta.ok`. Si es **false**, lanza un `Error` con el `status`.
  3. Parse el JSON.
  4. Actualice `currentPage` y `totalPages` con los datos de `info`.
  5. Llame a `renderCharacters(datos.results)` para pintar las cards.
  6. Llame a `updateControls()` para actualizar botones y etiqueta de página.

> **Nota:** Maneja errores con `try/catch`. Si hay error, muestra un mensaje en `#grid` en color rojo (por ejemplo, “Error cargando datos”).

#### Paso 3 — Renderizado de cards (`renderCharacters`)

- Implementa `renderCharacters(chars)`:
  - Si `chars` es un array, mapea cada elemento a una **card** muy simple que incluya:
    - `<img src="..." alt="...">`
    - `<h3>Nombre</h3>`
    - `<p>Estado</p>`
  - Inserta el HTML resultante en `#grid` con `innerHTML`.
  - Si no hay resultados, muestra un mensaje: “No hay resultados”.

#### Paso 4 — Actualización de controles (`updateControls`)

- Implementa `updateControls()` para:
  - Actualizar el texto de `#pageLabel` con: `Página X de Y`.
  - Deshabilitar `#prev` si `currentPage === 1`.
  - Deshabilitar `#next` si `currentPage === totalPages`.

#### Paso 5 — Eventos de los botones

- Añade `addEventListener("click", …)` a:
  - `#prev`: si `currentPage > 1`, llama a `fetchPage(currentPage - 1)`.
  - `#next`: si `currentPage < totalPages`, llama a `fetchPage(currentPage + 1)`.

#### Paso 6 — Carga inicial

- Al cargar la página, invoca `fetchPage(1)` para mostrar la primera página.

#### (Opcional recomendado) Indicador de carga

- Mientras esperas la respuesta, muestra en algún elemento (p. ej. arriba del grid) el texto “Cargando…”.
- Deshabilita temporalmente los botones mientras dura la petición.

---

### 6. Criterios de evaluación (rúbrica)

| Criterio                        | Detalle                                                                  | Ponderación |
| ------------------------------- | ------------------------------------------------------------------------ | ----------- |
| **Funcionalidad de paginación** | Carga página 1, navega correctamente, límites bien gestionados           | 40%         |
| **Consumo de API**              | Uso correcto de `fetch`, manejo de `res.ok`, parseo de JSON              | 20%         |
| **Renderizado DOM**             | Cards bien formadas (imagen, nombre, estado), actualización del grid     | 15%         |
| **Manejo de errores/UX**        | Mensajes de error, deshabilitado de botones, (opcional: “Cargando…”)     | 15%         |
| **Calidad del código**          | Claridad, nombres significativos, funciones separadas, sin código muerto | 10%         |

---

### 7. Pruebas de verificación (checklist)

- [ ] Al abrir, se carga **Página 1** y se muestran ~20 personajes.
- [ ] Botón **Anterior** está deshabilitado en Página 1.
- [ ] Al pulsar **Siguiente**, aumenta la página y se renderizan **nuevos** personajes.
- [ ] Al llegar a la última página, **Siguiente** queda deshabilitado.
- [ ] Si la petición falla (simula desconexión), aparece un **mensaje de error** visible en el grid.
- [ ] No se han modificado HTML/CSS originales (solo JS).

---

### 8. Pistas técnicas (si las necesitas)

- Usa **template literals** para construir el HTML de las cards:
  ```js
  grid.innerHTML = chars
    .map(
      (c) => `
    <div class="card">
      <img src="${c.image}" alt="${c.name}">
      <h3>${c.name}</h3>
      <p>${c.status}</p>
    </div>
  `
    )
    .join("");
  ```

Recuerda siempre comprobar respuesta.ok antes de respuesta.json().

Envuelve las peticiones en try/catch para capturar errores de red.

Evita múltiples clics rápidos deshabilitando botones mientras se carga.

### Entrega

Entrega tu archivo app.js (o el HTML con el bloque de código JavaScript al final, según indique el profesor).

Incluye comentarios breves explicando cada función.

Si quieres, te paso también un **`app.js` plantilla vacío** con las funciones y comentarios para que ellos solo tengan que completarlo.
