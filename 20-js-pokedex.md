# 20 — Ejercicio integrador: Pokédex

[← Manipulación del DOM](19-js-dom.md) | [← Índice](README.md)

---

## ¿Qué vas a construir?

Una **Pokédex** interactiva que:
- Muestra una lista de los primeros Pokémon
- Permite buscar un Pokémon por nombre o número
- Muestra su imagen, tipo, altura y peso
- Todo consultando la [PokéAPI](https://pokeapi.co/) — una API pública y gratuita

Al terminar tendrás una aplicación real que usa todo lo que aprendiste: HTML, CSS, JavaScript, `fetch` y manipulación del DOM.

---

## Cómo está organizado este ejercicio

El ejercicio tiene **5 pasos progresivos**. Cada paso agrega una funcionalidad nueva. Puedes detenerte en cualquier paso y ya tendrás algo que funciona.

| Paso | Qué agregas |
|------|------------|
| 1 | Estructura HTML y estilos base |
| 2 | Cargar y mostrar un Pokémon con fetch |
| 3 | Buscar por nombre desde un campo |
| 4 | Mostrar una lista de Pokémon |
| 5 | Detalles al hacer clic en una tarjeta |

---

## Antes de empezar: la PokéAPI

La URL base es:

```
https://pokeapi.co/api/v2/pokemon/{nombre-o-numero}
```

Por ejemplo:
- `https://pokeapi.co/api/v2/pokemon/pikachu`
- `https://pokeapi.co/api/v2/pokemon/25`

Los datos que usaremos de cada Pokémon:

```js
pokemon.name              // "pikachu"
pokemon.id                // 25
pokemon.height            // 4  (en decímetros → multiplica × 10 para cm)
pokemon.weight            // 60 (en hectogramos → divide ÷ 10 para kg)
pokemon.sprites.front_default  // URL de la imagen oficial
pokemon.types[0].type.name     // "electric"
pokemon.stats[0].base_stat     // valor del primer stat (HP)
```

Puedes explorar la respuesta completa pegando la URL en el navegador.

---

## Paso 1: Estructura HTML y estilos

Crea un archivo `pokedex.html` y pega este código:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pokédex</title>
    <style>
      * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
      }

      body {
        font-family: sans-serif;
        background: #f0f0f0;
        padding: 2rem;
      }

      h1 {
        text-align: center;
        color: #cc0000;
        margin-bottom: 1.5rem;
        font-size: 2.5rem;
      }

      .buscador {
        display: flex;
        justify-content: center;
        gap: 8px;
        margin-bottom: 2rem;
      }

      .buscador input {
        padding: 10px 16px;
        font-size: 1rem;
        border: 2px solid #ccc;
        border-radius: 8px;
        width: 280px;
      }

      .buscador button {
        padding: 10px 20px;
        font-size: 1rem;
        background: #cc0000;
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
      }

      .buscador button:hover {
        background: #aa0000;
      }

      #grilla {
        display: flex;
        flex-wrap: wrap;
        gap: 16px;
        justify-content: center;
      }

      .tarjeta {
        background: white;
        border-radius: 12px;
        padding: 16px;
        width: 160px;
        text-align: center;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        cursor: pointer;
        transition: transform 0.15s;
      }

      .tarjeta:hover {
        transform: translateY(-4px);
      }

      .tarjeta img {
        width: 96px;
        height: 96px;
      }

      .tarjeta h3 {
        text-transform: capitalize;
        margin: 8px 0 4px;
        font-size: 0.95rem;
      }

      .tarjeta .numero {
        color: #999;
        font-size: 0.8rem;
      }

      .tipo {
        display: inline-block;
        padding: 2px 10px;
        border-radius: 12px;
        font-size: 0.75rem;
        color: white;
        margin: 2px;
        text-transform: capitalize;
      }

      /* Colores por tipo */
      .tipo-fire     { background: #F08030; }
      .tipo-water    { background: #6890F0; }
      .tipo-grass    { background: #78C850; }
      .tipo-electric { background: #F8D030; color: #333; }
      .tipo-psychic  { background: #F85888; }
      .tipo-ice      { background: #98D8D8; color: #333; }
      .tipo-dragon   { background: #7038F8; }
      .tipo-dark     { background: #705848; }
      .tipo-fairy    { background: #EE99AC; color: #333; }
      .tipo-normal   { background: #A8A878; }
      .tipo-fighting { background: #C03028; }
      .tipo-flying   { background: #A890F0; }
      .tipo-poison   { background: #A040A0; }
      .tipo-ground   { background: #E0C068; color: #333; }
      .tipo-rock     { background: #B8A038; }
      .tipo-bug      { background: #A8B820; color: #333; }
      .tipo-ghost    { background: #705898; }
      .tipo-steel    { background: #B8B8D0; color: #333; }

      #detalle {
        max-width: 400px;
        margin: 2rem auto;
        background: white;
        border-radius: 16px;
        padding: 2rem;
        box-shadow: 0 4px 16px rgba(0,0,0,0.15);
        display: none;   /* oculto por defecto */
        text-align: center;
      }

      #detalle img {
        width: 160px;
        height: 160px;
      }

      #detalle h2 {
        text-transform: capitalize;
        color: #cc0000;
        font-size: 1.8rem;
        margin: 8px 0;
      }

      #detalle table {
        width: 100%;
        margin-top: 1rem;
        border-collapse: collapse;
      }

      #detalle td {
        padding: 6px 12px;
        border-bottom: 1px solid #eee;
        text-align: left;
      }

      #detalle td:first-child {
        font-weight: bold;
        color: #555;
        width: 40%;
      }

      #mensaje-error {
        text-align: center;
        color: #cc0000;
        margin-top: 1rem;
        display: none;
      }
    </style>
  </head>
  <body>

    <h1>Pokédex</h1>

    <div class="buscador">
      <input type="text" id="campoBusqueda" placeholder="Nombre o número..." />
      <button id="botonBuscar">Buscar</button>
    </div>

    <div id="mensaje-error">Pokémon no encontrado. Verifica el nombre o número.</div>

    <div id="detalle">
      <!-- se llenará con JavaScript -->
    </div>

    <div id="grilla">
      <!-- las tarjetas se cargarán aquí -->
    </div>

    <script>
      // Aquí escribirás el JavaScript en los pasos siguientes
    </script>

  </body>
</html>
```

Abre el archivo en el navegador. Deberías ver el título rojo y el buscador. La página está vacía porque todavía no cargamos datos.

---

## Paso 2: Cargar un Pokémon con fetch

Dentro del `<script>`, escribe las siguientes funciones.

La primera convierte los datos crudos de la API en un objeto más simple:

```js
function parsearPokemon(datos) {
  return {
    id: datos.id,
    nombre: datos.name,
    imagen: datos.sprites.front_default,
    tipos: datos.types.map(t => t.type.name),
    altura: datos.height * 10,       // de dm a cm
    peso: (datos.weight / 10).toFixed(1), // de hg a kg
  };
}
```

La segunda hace la petición a la API:

```js
async function obtenerPokemon(nombreONumero) {
  const url = `https://pokeapi.co/api/v2/pokemon/${nombreONumero}`;
  const respuesta = await fetch(url);

  if (!respuesta.ok) {
    throw new Error("Pokémon no encontrado");
  }

  const datos = await respuesta.json();
  return parsearPokemon(datos);
}
```

Prueba que funciona. Agrega esto temporalmente al final del script y abre la consola:

```js
obtenerPokemon("pikachu").then(p => console.log(p));
```

Deberías ver el objeto con los datos de Pikachu. Cuando lo confirmes, borra esa línea de prueba.

---

## Paso 3: Buscar desde el campo de texto

Ahora conecta el buscador con la API. Agrega estas funciones:

```js
function mostrarError(visible) {
  const mensaje = document.getElementById("mensaje-error");
  mensaje.style.display = visible ? "block" : "none";
}

function mostrarDetalle(pokemon) {
  const div = document.getElementById("detalle");

  // Construir las etiquetas de tipo
  const etiquetasTipo = pokemon.tipos
    .map(tipo => `<span class="tipo tipo-${tipo}">${tipo}</span>`)
    .join(" ");

  div.innerHTML = `
    <img src="${pokemon.imagen}" alt="${pokemon.nombre}" />
    <h2>#${pokemon.id} — ${pokemon.nombre}</h2>
    <div>${etiquetasTipo}</div>
    <table>
      <tr><td>Altura</td><td>${pokemon.altura} cm</td></tr>
      <tr><td>Peso</td><td>${pokemon.peso} kg</td></tr>
    </table>
  `;

  div.style.display = "block";
}

async function buscar() {
  const campo = document.getElementById("campoBusqueda");
  const termino = campo.value.trim().toLowerCase();

  if (!termino) return;

  mostrarError(false);

  try {
    const pokemon = await obtenerPokemon(termino);
    mostrarDetalle(pokemon);
  } catch {
    mostrarError(true);
    document.getElementById("detalle").style.display = "none";
  }
}

// Conectar el botón y la tecla Enter
document.getElementById("botonBuscar").addEventListener("click", buscar);
document.getElementById("campoBusqueda").addEventListener("keydown", (e) => {
  if (e.key === "Enter") buscar();
});
```

Prueba buscando "pikachu", "charmander" o "150". Deberías ver la tarjeta de detalle aparecer debajo del buscador.

---

## Paso 4: Cargar la lista inicial de Pokémon

Para mostrar la grilla de los primeros 20 Pokémon necesitas consultar un endpoint diferente que devuelve una lista:

```
https://pokeapi.co/api/v2/pokemon?limit=20
```

Responde con una lista de objetos `{ name, url }`. Luego debes consultar cada uno individualmente.

Agrega estas funciones:

```js
function crearTarjeta(pokemon) {
  const tarjeta = document.createElement("div");
  tarjeta.classList.add("tarjeta");

  const etiquetasTipo = pokemon.tipos
    .map(tipo => `<span class="tipo tipo-${tipo}">${tipo}</span>`)
    .join(" ");

  tarjeta.innerHTML = `
    <img src="${pokemon.imagen}" alt="${pokemon.nombre}" />
    <h3>${pokemon.nombre}</h3>
    <div class="numero">#${pokemon.id}</div>
    <div>${etiquetasTipo}</div>
  `;

  return tarjeta;
}

async function cargarGrilla() {
  const grilla = document.getElementById("grilla");
  grilla.innerHTML = "Cargando Pokémon...";

  try {
    const respuesta = await fetch("https://pokeapi.co/api/v2/pokemon?limit=20");
    const datos = await respuesta.json();

    grilla.innerHTML = ""; // limpiar el mensaje de carga

    for (let entrada of datos.results) {
      const pokemon = await obtenerPokemon(entrada.name);
      const tarjeta = crearTarjeta(pokemon);
      grilla.appendChild(tarjeta);
    }

  } catch (error) {
    grilla.innerHTML = "Error al cargar la lista.";
    console.error(error);
  }
}

cargarGrilla();
```

Al recargar la página verás cómo las tarjetas van apareciendo una a una conforme llegan los datos.

---

## Paso 5: Ver el detalle al hacer clic en una tarjeta

Solo tienes que agregar un evento `click` a cada tarjeta cuando la creas. Modifica la función `crearTarjeta` — agrega estas dos líneas al final, antes del `return`:

```js
  // Agregar dentro de crearTarjeta, antes del return:
  tarjeta.addEventListener("click", () => {
    mostrarDetalle(pokemon);
    window.scrollTo({ top: 0, behavior: "smooth" });
  });
```

Ahora al hacer clic en cualquier tarjeta, el detalle aparece arriba y la página hace scroll automáticamente.

---

## El código JavaScript completo

Una vez que hayas completado los 5 pasos, tu `<script>` debería verse así:

```js
function parsearPokemon(datos) {
  return {
    id: datos.id,
    nombre: datos.name,
    imagen: datos.sprites.front_default,
    tipos: datos.types.map(t => t.type.name),
    altura: datos.height * 10,
    peso: (datos.weight / 10).toFixed(1),
  };
}

async function obtenerPokemon(nombreONumero) {
  const url = `https://pokeapi.co/api/v2/pokemon/${nombreONumero}`;
  const respuesta = await fetch(url);
  if (!respuesta.ok) throw new Error("Pokémon no encontrado");
  const datos = await respuesta.json();
  return parsearPokemon(datos);
}

function mostrarError(visible) {
  const mensaje = document.getElementById("mensaje-error");
  mensaje.style.display = visible ? "block" : "none";
}

function mostrarDetalle(pokemon) {
  const div = document.getElementById("detalle");
  const etiquetasTipo = pokemon.tipos
    .map(tipo => `<span class="tipo tipo-${tipo}">${tipo}</span>`)
    .join(" ");

  div.innerHTML = `
    <img src="${pokemon.imagen}" alt="${pokemon.nombre}" />
    <h2>#${pokemon.id} — ${pokemon.nombre}</h2>
    <div>${etiquetasTipo}</div>
    <table>
      <tr><td>Altura</td><td>${pokemon.altura} cm</td></tr>
      <tr><td>Peso</td><td>${pokemon.peso} kg</td></tr>
    </table>
  `;
  div.style.display = "block";
}

async function buscar() {
  const campo = document.getElementById("campoBusqueda");
  const termino = campo.value.trim().toLowerCase();
  if (!termino) return;

  mostrarError(false);
  try {
    const pokemon = await obtenerPokemon(termino);
    mostrarDetalle(pokemon);
  } catch {
    mostrarError(true);
    document.getElementById("detalle").style.display = "none";
  }
}

function crearTarjeta(pokemon) {
  const tarjeta = document.createElement("div");
  tarjeta.classList.add("tarjeta");

  const etiquetasTipo = pokemon.tipos
    .map(tipo => `<span class="tipo tipo-${tipo}">${tipo}</span>`)
    .join(" ");

  tarjeta.innerHTML = `
    <img src="${pokemon.imagen}" alt="${pokemon.nombre}" />
    <h3>${pokemon.nombre}</h3>
    <div class="numero">#${pokemon.id}</div>
    <div>${etiquetasTipo}</div>
  `;

  tarjeta.addEventListener("click", () => {
    mostrarDetalle(pokemon);
    window.scrollTo({ top: 0, behavior: "smooth" });
  });

  return tarjeta;
}

async function cargarGrilla() {
  const grilla = document.getElementById("grilla");
  grilla.innerHTML = "Cargando Pokémon...";

  try {
    const respuesta = await fetch("https://pokeapi.co/api/v2/pokemon?limit=20");
    const datos = await respuesta.json();
    grilla.innerHTML = "";

    for (let entrada of datos.results) {
      const pokemon = await obtenerPokemon(entrada.name);
      const tarjeta = crearTarjeta(pokemon);
      grilla.appendChild(tarjeta);
    }
  } catch (error) {
    grilla.innerHTML = "Error al cargar la lista.";
    console.error(error);
  }
}

document.getElementById("botonBuscar").addEventListener("click", buscar);
document.getElementById("campoBusqueda").addEventListener("keydown", (e) => {
  if (e.key === "Enter") buscar();
});

cargarGrilla();
```

---

## Ideas para seguir mejorando

Si quieres ir más allá, aquí tienes algunos desafíos opcionales:

- **Más Pokémon:** cambia `limit=20` a `limit=150` para ver la primera generación completa
- **Más datos:** agrega la sección de estadísticas base (`pokemon.stats`)
- **Filtrar por tipo:** agrega botones para mostrar solo Pokémon de tipo fuego, agua, etc.
- **Carga paralela:** en lugar de cargar los Pokémon uno por uno, usa `Promise.all()` para cargar todos al mismo tiempo y que sea más rápido
- **Pokémon aleatorio:** agrega un botón que cargue un Pokémon al azar entre el 1 y el 898

---

## Lo que usaste en este ejercicio

| Concepto | Dónde aparece |
|----------|--------------|
| `fetch` + `async/await` | `obtenerPokemon()`, `cargarGrilla()` |
| `try/catch` | Manejo de errores en la búsqueda |
| `document.createElement` | `crearTarjeta()` |
| `appendChild` | Insertar tarjetas en la grilla |
| `innerHTML` | Rellenar la tarjeta de detalle |
| `classList` | Clases de color por tipo |
| `addEventListener` | Botón buscar, tecla Enter, clic en tarjeta |
| `Array.map()` | Crear etiquetas de tipo |
| Arrow functions | En todo el código |
| Template literals | Construir HTML dinámico |

---

[← Manipulación del DOM](19-js-dom.md) | [← Índice](README.md)
