# 18 — Fetch y promesas

[← Funciones](17-js-funciones.md) | [Siguiente: Manipulación del DOM →](19-js-dom.md)

---

## El problema: el tiempo en programación

Imagina que le pides a un amigo que vaya al supermercado. Tú no te quedas quieto esperando — sigues haciendo otras cosas mientras él regresa. Cuando llega, te avisa y entonces guardas las compras.

Así funciona JavaScript con las peticiones de red: cuando pides datos a un servidor, el programa **no se detiene** a esperar — sigue ejecutando otras instrucciones. Cuando llegan los datos, se ejecuta el código que los procesa.

Esto se llama **programación asíncrona**.

---

## ¿Qué es una promesa?

Una **promesa** (Promise) representa una operación que todavía no terminó, pero que eventualmente terminará con un resultado (o con un error).

Tiene tres estados:

```
⏳ Pendiente (pending)   → todavía esperando
✅ Resuelta (fulfilled)  → terminó con éxito
❌ Rechazada (rejected)  → ocurrió un error
```

---

## `fetch()` — pedir datos a internet

`fetch()` es la función que usa el navegador para hacer peticiones HTTP. Devuelve una promesa.

```js
fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
  .then(respuesta => respuesta.json())
  .then(datos => {
    console.log(datos.name);   // "pikachu"
    console.log(datos.height); // 4
  })
  .catch(error => {
    console.log("Ocurrió un error:", error);
  });
```

El encadenamiento de `.then()`:
1. `fetch()` hace la petición y devuelve una promesa con la **respuesta cruda**
2. `.then(respuesta => respuesta.json())` convierte esa respuesta a un objeto JavaScript
3. `.then(datos => ...)` recibe el objeto ya convertido y lo usa
4. `.catch(error => ...)` captura cualquier error en toda la cadena

---

## `async / await` — la forma moderna (y más legible)

`async/await` es una forma de escribir código asíncrono que parece código normal y se lee de arriba hacia abajo.

```js
async function buscarPokemon(nombre) {
  const respuesta = await fetch(`https://pokeapi.co/api/v2/pokemon/${nombre}`);
  const datos = await respuesta.json();
  console.log(datos.name, datos.height);
}

buscarPokemon("charmander");
```

- `async` antes de `function` indica que la función es asíncrona
- `await` pausa la ejecución de esa función hasta que la promesa se resuelva
- El resto del programa **no** se detiene — solo esa función espera

### Con manejo de errores

```js
async function buscarPokemon(nombre) {
  try {
    const respuesta = await fetch(`https://pokeapi.co/api/v2/pokemon/${nombre}`);

    if (!respuesta.ok) {
      throw new Error(`Error ${respuesta.status}: Pokémon no encontrado`);
    }

    const datos = await respuesta.json();
    return datos;

  } catch (error) {
    console.error("Algo salió mal:", error.message);
    return null;
  }
}
```

`try/catch` es el equivalente de `if/else` para errores:
- El código dentro de `try` se ejecuta normalmente
- Si algo lanza un error, la ejecución salta a `catch`

---

## ¿Qué es JSON?

Cuando un servidor responde a un `fetch()`, generalmente envía datos en formato **JSON** (JavaScript Object Notation). Es texto estructurado que parece exactamente un objeto de JavaScript.

```json
{
  "name": "pikachu",
  "height": 4,
  "weight": 60,
  "types": [
    { "type": { "name": "electric" } }
  ]
}
```

`respuesta.json()` convierte ese texto en un objeto JavaScript real con el que puedes trabajar normalmente.

---

## Ejemplo completo: consultar una API

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Primer Fetch</title>
  </head>
  <body>
    <h1>Consulta de Pokémon</h1>
    <p id="resultado">Cargando...</p>

    <script>
      async function cargarPokemon() {
        try {
          const respuesta = await fetch("https://pokeapi.co/api/v2/pokemon/bulbasaur");
          const pokemon = await respuesta.json();

          const texto = `
            Nombre: ${pokemon.name}
            Altura: ${pokemon.height * 10} cm
            Peso: ${pokemon.weight / 10} kg
          `;

          document.getElementById("resultado").textContent = texto;

        } catch (error) {
          document.getElementById("resultado").textContent = "Error al cargar";
          console.error(error);
        }
      }

      cargarPokemon();
    </script>
  </body>
</html>
```

---

## Conceptos clave resumidos

| Concepto | ¿Qué hace? |
|----------|-----------|
| `fetch(url)` | Hace una petición HTTP a una URL |
| `.then(fn)` | Ejecuta `fn` cuando la promesa se resuelve |
| `.catch(fn)` | Ejecuta `fn` si hay un error |
| `async function` | Declara una función que puede usar `await` |
| `await` | Espera que una promesa se resuelva |
| `respuesta.json()` | Convierte la respuesta en un objeto JS |
| `try / catch` | Ejecuta código y captura errores |
| `respuesta.ok` | `true` si el servidor respondió con éxito (código 200–299) |

---

## ¿Cómo sé qué datos devuelve una API?

Pega la URL directamente en el navegador. Por ejemplo:

```
https://pokeapi.co/api/v2/pokemon/pikachu
```

El navegador muestra el JSON completo. También puedes usar la pestaña **Network** del inspector (`F12`) para ver peticiones en tiempo real.

---

[← Funciones](17-js-funciones.md) | [Siguiente: Manipulación del DOM →](19-js-dom.md)
