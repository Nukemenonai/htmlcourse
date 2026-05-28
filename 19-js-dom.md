# 19 — Manipulación del DOM

[← Fetch y promesas](18-js-fetch-promesas.md) | [Siguiente: Ejercicio — Pokédex →](20-js-pokedex.md)

---

## Recuerda: el DOM es el árbol de tu página

Como viste en la lección de HTML, el navegador convierte tu documento en un árbol llamado **DOM** (Document Object Model). JavaScript puede leer y modificar ese árbol: agregar elementos, cambiar textos, responder a clics... todo en tiempo real sin recargar la página.

El objeto `document` es tu punto de entrada al DOM — representa toda la página.

---

## Seleccionar elementos

Antes de modificar algo, tienes que encontrarlo.

### `document.querySelector(selector)`

Devuelve el **primer** elemento que coincide con un selector CSS.

```js
const titulo = document.querySelector("h1");
const boton = document.querySelector("#enviar");       // por id
const caja = document.querySelector(".tarjeta");       // por clase
const input = document.querySelector("form input");    // selector combinado
```

### `document.querySelectorAll(selector)`

Devuelve **todos** los elementos que coinciden — una colección que puedes recorrer.

```js
const parrafos = document.querySelectorAll("p");

parrafos.forEach(parrafo => {
  console.log(parrafo.textContent);
});
```

### `document.getElementById(id)`

Busca un elemento por su atributo `id`. Es más rápido que `querySelector` pero solo sirve para ids.

```js
const resultado = document.getElementById("resultado");
```

### `document.getElementsByClassName(clase)`

Devuelve todos los elementos con esa clase. Es más antiguo — prefiere `querySelectorAll`.

---

## Leer y cambiar el contenido

### `.textContent` — texto plano

```js
const parrafo = document.querySelector("p");

console.log(parrafo.textContent); // lee el texto actual
parrafo.textContent = "Nuevo texto"; // cambia el texto
```

### `.innerHTML` — HTML dentro del elemento

```js
const caja = document.querySelector("#caja");

caja.innerHTML = "<strong>Texto en negrita</strong>";
```

> Usa `.textContent` cuando el contenido sea texto del usuario (evita vulnerabilidades). Usa `.innerHTML` solo cuando necesites insertar HTML real.

---

## Cambiar estilos y clases

### `.style`

Modifica el estilo en línea directamente:

```js
const titulo = document.querySelector("h1");
titulo.style.color = "blue";
titulo.style.fontSize = "2rem";
titulo.style.display = "none"; // ocultar
```

### `.classList`

Es mejor agregar o quitar **clases CSS** que manipular estilos directamente. Define los estilos en tu CSS y actívalos con JavaScript:

```js
const caja = document.querySelector(".caja");

caja.classList.add("activo");     // agrega la clase "activo"
caja.classList.remove("activo");  // la quita
caja.classList.toggle("activo");  // la agrega si no está, la quita si ya está
caja.classList.contains("activo"); // true o false
```

---

## Cambiar atributos

```js
const imagen = document.querySelector("img");

imagen.src = "nueva-imagen.jpg";         // cambiar atributo src
imagen.alt = "Descripción de la imagen";

const enlace = document.querySelector("a");
enlace.href = "https://ejemplo.com";
enlace.setAttribute("target", "_blank"); // abrir en nueva pestaña
```

---

## Escuchar eventos: `addEventListener`

Los **eventos** son acciones del usuario o del navegador: clics, teclas presionadas, movimiento del ratón, carga de la página, etc.

`addEventListener(evento, función)` ejecuta una función cada vez que ocurre el evento.

```js
const boton = document.querySelector("#miBoton");

boton.addEventListener("click", function() {
  console.log("¡Clic!");
});
```

Con arrow function (más común):

```js
boton.addEventListener("click", () => {
  console.log("¡Clic!");
});
```

### Eventos comunes

| Evento | Cuándo ocurre |
|--------|--------------|
| `click` | Al hacer clic |
| `dblclick` | Al hacer doble clic |
| `mouseover` | Al pasar el cursor encima |
| `keydown` | Al presionar una tecla |
| `keyup` | Al soltar una tecla |
| `input` | Al escribir en un campo |
| `change` | Al cambiar el valor de un campo |
| `submit` | Al enviar un formulario |
| `load` | Cuando la página termina de cargar |

### El objeto `event`

La función recibe automáticamente un objeto con información sobre el evento:

```js
const campo = document.querySelector("input");

campo.addEventListener("input", (evento) => {
  console.log("El usuario escribió:", evento.target.value);
});
```

`evento.target` es el elemento que disparó el evento.

---

## Crear y agregar elementos

### `document.createElement(etiqueta)`

Crea un nuevo elemento HTML (en memoria, aún no está en la página).

```js
const parrafo = document.createElement("p");
parrafo.textContent = "Soy un nuevo párrafo";
```

### `elemento.appendChild(hijo)`

Inserta el elemento al final de otro:

```js
const lista = document.querySelector("#miLista");
const elemento = document.createElement("li");
elemento.textContent = "Nuevo ítem";
lista.appendChild(elemento);
```

### `elemento.remove()`

Elimina un elemento de la página:

```js
const parrafo = document.querySelector("#parrafoViejo");
parrafo.remove();
```

---

## Ejemplo completo: lista dinámica

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Lista dinámica</title>
    <style>
      body { font-family: sans-serif; padding: 2rem; }
      input { padding: 8px; margin-right: 8px; }
      button { padding: 8px 16px; }
      li { margin: 4px 0; cursor: pointer; }
      li:hover { color: red; text-decoration: line-through; }
    </style>
  </head>
  <body>
    <h1>Mi lista de tareas</h1>
    <input type="text" id="nuevaTarea" placeholder="Escribe una tarea..." />
    <button id="agregar">Agregar</button>
    <ul id="lista"></ul>

    <script>
      const inputTarea = document.querySelector("#nuevaTarea");
      const botonAgregar = document.querySelector("#agregar");
      const lista = document.querySelector("#lista");

      botonAgregar.addEventListener("click", () => {
        const texto = inputTarea.value.trim();

        if (texto === "") return; // no agregar si está vacío

        const item = document.createElement("li");
        item.textContent = texto;

        // clic en el ítem lo elimina
        item.addEventListener("click", () => item.remove());

        lista.appendChild(item);
        inputTarea.value = ""; // limpiar el campo
        inputTarea.focus();    // devolver el foco al campo
      });

      // también agregar con Enter
      inputTarea.addEventListener("keydown", (e) => {
        if (e.key === "Enter") botonAgregar.click();
      });
    </script>
  </body>
</html>
```

---

## Resumen

| Acción | Código |
|--------|--------|
| Seleccionar uno | `document.querySelector("selector")` |
| Seleccionar varios | `document.querySelectorAll("selector")` |
| Leer texto | `elemento.textContent` |
| Cambiar texto | `elemento.textContent = "nuevo"` |
| Insertar HTML | `elemento.innerHTML = "<b>texto</b>"` |
| Cambiar estilo | `elemento.style.color = "red"` |
| Agregar clase | `elemento.classList.add("clase")` |
| Quitar clase | `elemento.classList.remove("clase")` |
| Alternar clase | `elemento.classList.toggle("clase")` |
| Escuchar evento | `elemento.addEventListener("click", fn)` |
| Crear elemento | `document.createElement("p")` |
| Insertar hijo | `padre.appendChild(hijo)` |
| Eliminar elemento | `elemento.remove()` |

---

[← Fetch y promesas](18-js-fetch-promesas.md) | [Siguiente: Ejercicio — Pokédex →](20-js-pokedex.md)
