# 14 — JavaScript: la consola y el navegador

[← Flexbox](13-flexbox.md) | [Siguiente: Datos y estructuras →](15-js-datos-estructuras.md)

---

## ¿Qué es JavaScript?

HTML describe el contenido de una página. CSS describe cómo se ve. **JavaScript** le da comportamiento: reacciona a clics, mueve elementos, consulta datos de internet, valida formularios.

Piénsalo así:
- HTML es el esqueleto (estructura)
- CSS es la ropa (apariencia)
- JavaScript es los músculos y el cerebro (comportamiento y lógica)

---

## ¿Dónde se escribe JavaScript?

Igual que CSS, tienes dos opciones principales:

### Opción 1: dentro de la página con `<script>`

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi página</title>
  </head>
  <body>
    <h1>Hola mundo</h1>

    <script>
      console.log("¡JavaScript funcionando!");
    </script>
  </body>
</html>
```

> Pon el `<script>` **al final del `<body>`**, justo antes de `</body>`. Así el navegador carga el HTML antes de ejecutar el código.

### Opción 2: en un archivo separado `.js`

```html
<!-- En el HTML -->
<script src="script.js"></script>
```

```js
// En script.js
console.log("Hola desde archivo externo");
```

---

## La consola del navegador

La **consola** es la herramienta más importante para aprender JavaScript. Es como una ventana al interior de tu página.

**Cómo abrirla:**
- Chrome / Edge: presiona `F12` o `Ctrl+Shift+I` (Windows) / `Cmd+Option+I` (Mac)
- Ve a la pestaña **Console**

---

## `console.log()` — imprimir mensajes

`console.log()` imprime cualquier cosa en la consola. Es tu herramienta principal para ver qué está pasando en tu código.

```js
console.log("Hola mundo");
console.log(42);
console.log(true);
console.log("Mi nombre es", "Ana", "y tengo", 25, "años");
```

Puedes pasar varios valores separados por coma y los imprime todos en una línea.

```js
let nombre = "Carlos";
let edad = 30;
console.log("Nombre:", nombre, "— Edad:", edad);
// → Nombre: Carlos — Edad: 30
```

> Las líneas que empiezan con `//` son **comentarios**: el navegador las ignora. Úsalos para explicar tu código.

---

## `alert()` — mostrar una ventana emergente

`alert()` muestra un cuadro de diálogo en pantalla. El usuario debe cerrarlo para continuar.

```js
alert("¡Bienvenido a mi página!");
```

Es útil para avisos simples, pero en aplicaciones reales se prefiere mostrar mensajes dentro de la propia página (más adelante aprenderás cómo).

---

## `prompt()` — pedirle información al usuario

`prompt()` abre un cuadro de diálogo con un campo de texto. **Devuelve** lo que el usuario escribe como texto.

```js
let nombre = prompt("¿Cómo te llamas?");
console.log("Hola,", nombre);
```

Si el usuario cancela, `prompt()` devuelve `null`.

---

## `confirm()` — hacer una pregunta de sí/no

`confirm()` muestra un cuadro con botones "Aceptar" y "Cancelar". Devuelve `true` si el usuario acepta, `false` si cancela.

```js
let respuesta = confirm("¿Quieres continuar?");
console.log(respuesta); // true o false
```

---

## Punto y coma

En JavaScript, las instrucciones terminan con `;`. No siempre es obligatorio, pero es buena práctica incluirlo para evitar errores difíciles de detectar.

```js
console.log("Primera instrucción");
console.log("Segunda instrucción");
```

---

## Ejemplo completo

Crea un archivo `index.html` con esto y ábrelo en el navegador:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi primer JS</title>
  </head>
  <body>
    <h1>Abre la consola (F12)</h1>

    <script>
      console.log("=== Bienvenido ===");

      let nombre = prompt("¿Cuál es tu nombre?");

      if (nombre) {
        alert("¡Hola, " + nombre + "! Bienvenido al curso.");
        console.log("El usuario se llama:", nombre);
      } else {
        console.log("El usuario no ingresó su nombre.");
      }
    </script>
  </body>
</html>
```

Abre la consola antes de recargar la página para ver los mensajes aparecer en tiempo real.

---

## Resumen

| Herramienta | ¿Para qué sirve? |
|-------------|-----------------|
| `console.log()` | Imprimir mensajes en la consola (solo tú los ves) |
| `alert()` | Mostrar un aviso al usuario |
| `prompt()` | Pedirle texto al usuario |
| `confirm()` | Hacerle una pregunta de sí/no al usuario |

---

[← Flexbox](13-flexbox.md) | [Siguiente: Datos y estructuras →](15-js-datos-estructuras.md)
