# 16 — Programación básica: variables, condiciones y ciclos

[← Datos y estructuras](15-js-datos-estructuras.md) | [Siguiente: Funciones →](17-js-funciones.md)

---

## Variables

Una **variable** es una caja con nombre donde guardas información. Puedes consultarla y cambiarla después.

```js
let edad = 20;
console.log(edad); // 20

edad = 21;         // cambiar el valor
console.log(edad); // 21
```

### `let`, `const` y `var`

JavaScript tiene tres palabras para declarar variables. En la práctica usa solo `let` y `const`:

| Palabra | ¿Se puede cambiar? | Uso recomendado |
|---------|-------------------|----------------|
| `const` | No | Valores que no cambiarán |
| `let` | Sí | Valores que sí pueden cambiar |
| `var` | Sí | Antiguo, evítalo |

```js
const PI = 3.14159;       // nunca cambiará
let contador = 0;         // cambiará durante el programa
contador = contador + 1;  // ahora es 1
```

> **Regla práctica:** empieza siempre con `const`. Solo cambia a `let` si necesitas reasignar el valor.

---

## Condicionales: `if / else`

Un **condicional** le permite al programa tomar decisiones: "si esto es verdad, haz una cosa; si no, haz otra".

```js
let hora = 14;

if (hora < 12) {
  console.log("Buenos días");
} else if (hora < 19) {
  console.log("Buenas tardes");
} else {
  console.log("Buenas noches");
}
// → "Buenas tardes"
```

La estructura es:

```
if (condición) {
  // código que se ejecuta si la condición es VERDADERA
} else if (otra condición) {
  // código si la segunda condición es verdadera
} else {
  // código si ninguna condición fue verdadera
}
```

### Operadores lógicos

Puedes combinar condiciones:

```js
let edad = 22;
let tieneLicencia = true;

if (edad >= 18 && tieneLicencia) {
  console.log("Puede conducir");
}

if (edad < 13 || edad > 65) {
  console.log("Tarifa especial");
}
```

| Operador | Significado | Ejemplo |
|----------|-------------|---------|
| `&&` | Y (ambos deben ser true) | `a && b` |
| `\|\|` | O (al menos uno debe ser true) | `a \|\| b` |
| `!` | NO (invierte el valor) | `!true` → `false` |

---

## El ciclo `for`

Un ciclo **repite** un bloque de código un número determinado de veces. El `for` es el más común.

```js
for (let i = 0; i < 5; i++) {
  console.log("Vuelta número", i);
}
// → Vuelta número 0
// → Vuelta número 1
// → Vuelta número 2
// → Vuelta número 3
// → Vuelta número 4
```

El `for` tiene tres partes separadas por `;`:

```
for (inicio; condición; paso)
```

- **Inicio:** `let i = 0` — empieza en 0
- **Condición:** `i < 5` — continúa mientras sea verdad
- **Paso:** `i++` — suma 1 a `i` cada vuelta (`i++` es lo mismo que `i = i + 1`)

### Recorrer un array con `for`

```js
let paises = ["México", "Colombia", "Argentina", "Chile"];

for (let i = 0; i < paises.length; i++) {
  console.log(i, paises[i]);
}
// → 0 México
// → 1 Colombia
// → 2 Argentina
// → 3 Chile
```

### `for...of` — la forma más moderna

Para recorrer arrays, `for...of` es más limpio cuando no necesitas el índice:

```js
let colores = ["rojo", "verde", "azul"];

for (let color of colores) {
  console.log(color);
}
// → rojo
// → verde
// → azul
```

---

## El ciclo `while`

El `while` repite un bloque **mientras** una condición siga siendo verdadera. Es útil cuando no sabes cuántas veces necesitas repetir.

```js
let intentos = 0;

while (intentos < 3) {
  console.log("Intento número", intentos + 1);
  intentos++;
}
// → Intento número 1
// → Intento número 2
// → Intento número 3
```

> **Cuidado:** si la condición siempre es verdadera, el ciclo nunca termina y el navegador se congela. Asegúrate de que la condición eventualmente se vuelva `false`.

---

## `break` y `continue`

Dentro de cualquier ciclo puedes:
- **`break`** — salir del ciclo inmediatamente
- **`continue`** — saltar a la siguiente vuelta sin ejecutar el resto

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) break;          // se detiene cuando i es 5
  console.log(i);
}
// → 0 1 2 3 4

for (let i = 0; i < 6; i++) {
  if (i % 2 === 0) continue;  // salta los pares
  console.log(i);
}
// → 1 3 5
```

---

## Ejemplo integrador

```js
const calificaciones = [7, 9, 4, 10, 6, 3, 8];
let aprobados = 0;
let reprobados = 0;

for (let cal of calificaciones) {
  if (cal >= 6) {
    aprobados++;
    console.log(`Calificación ${cal} → APROBADO`);
  } else {
    reprobados++;
    console.log(`Calificación ${cal} → REPROBADO`);
  }
}

console.log("---");
console.log("Aprobados:", aprobados);
console.log("Reprobados:", reprobados);
```

---

## Resumen

| Concepto | Sintaxis | ¿Para qué? |
|----------|---------|-----------|
| Variable (cambiable) | `let x = valor` | Guardar datos que cambian |
| Variable (fija) | `const x = valor` | Guardar datos que no cambian |
| Condición | `if () { } else { }` | Tomar decisiones |
| Ciclo contado | `for (let i=0; i<n; i++)` | Repetir un número fijo de veces |
| Ciclo por lista | `for (let item of lista)` | Recorrer cada elemento de un array |
| Ciclo condicional | `while (condición)` | Repetir mientras algo sea verdad |

---

[← Datos y estructuras](15-js-datos-estructuras.md) | [Siguiente: Funciones →](17-js-funciones.md)
