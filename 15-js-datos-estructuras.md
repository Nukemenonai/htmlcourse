# 15 — Datos elementales y estructuras de datos

[← Consola y navegador](14-js-consola-navegador.md) | [Siguiente: Programación básica →](16-js-programacion-basica.md)

---

## Tipos de datos básicos

JavaScript maneja distintos tipos de información. Los más importantes son:

| Tipo | Nombre en inglés | Ejemplos |
|------|-----------------|---------|
| Texto | `string` | `"Hola"`, `'mundo'`, `` `¡JS!` `` |
| Número | `number` | `42`, `3.14`, `-7` |
| Booleano | `boolean` | `true`, `false` |
| Nada | `null` | `null` |
| No definido | `undefined` | `undefined` |

---

## Strings (cadenas de texto)

Un **string** es cualquier texto entre comillas. Puedes usar comillas simples `'`, dobles `"`, o backticks `` ` ``.

```js
let saludo = "Hola, mundo";
let nombre = 'Ana';
let mensaje = `Bienvenido, ${nombre}`;  // ← los backticks permiten insertar variables
```

Los backticks (`` ` ``) son especialmente útiles porque permiten **interpolación**: insertar el valor de una variable dentro del texto con `${}`.

```js
let ciudad = "Bogotá";
let temperatura = 18;
console.log(`Hoy en ${ciudad} hace ${temperatura}°C.`);
// → Hoy en Bogotá hace 18°C.
```

### Propiedades y métodos útiles de strings

```js
let texto = "javascript es genial";

console.log(texto.length);          // 20 — cuántos caracteres tiene
console.log(texto.toUpperCase());   // "JAVASCRIPT ES GENIAL"
console.log(texto.includes("genial")); // true
console.log(texto.replace("genial", "poderoso")); // "javascript es poderoso"
console.log(texto[0]);              // "j" — primer carácter (empieza en 0)
```

---

## Numbers (números)

JavaScript no distingue entre enteros y decimales — todos son `number`.

```js
let entero = 42;
let decimal = 3.14;
let negativo = -100;

console.log(10 + 3);   // 13
console.log(10 - 3);   // 7
console.log(10 * 3);   // 30
console.log(10 / 3);   // 3.333...
console.log(10 % 3);   // 1  ← módulo: el resto de la división
console.log(2 ** 8);   // 256 ← potencia: 2 elevado a 8
```

> El operador `%` (módulo) es muy útil: te dice si un número es par o impar. Si `n % 2 === 0`, el número es par.

---

## Booleans (verdadero / falso)

Un **boolean** solo puede ser `true` o `false`. Es el resultado de comparaciones y condiciones.

```js
let esMayor = 18 > 10;   // true
let esMenor = 5 > 100;   // false

console.log(5 === 5);    // true  — igual en valor y tipo
console.log(5 !== 3);    // true  — diferente
console.log(10 >= 10);   // true  — mayor o igual
console.log(3 < 1);      // false — menor que
```

> Usa siempre `===` (triple igual) para comparar — compara valor **y** tipo. El doble `==` hace conversiones que pueden dar resultados inesperados.

---

## null y undefined

- `null` significa "sin valor, intencionalmente vacío". Lo asignas tú.
- `undefined` significa "esto existe pero todavía no tiene valor". JavaScript lo asigna automáticamente.

```js
let dato = null;       // vacío a propósito
let otroDato;          // undefined: declaré la variable pero no le di valor
console.log(dato);     // null
console.log(otroDato); // undefined
```

---

## Arrays (listas)

Un **array** es una lista ordenada de valores. Se escribe con corchetes `[]`.

Piénsalo como una fila de cajones numerados, donde el primer cajón es el número **0**.

```js
let frutas = ["manzana", "banana", "naranja"];

console.log(frutas[0]); // "manzana" — primer elemento
console.log(frutas[1]); // "banana"
console.log(frutas[2]); // "naranja"
console.log(frutas.length); // 3 — cuántos elementos hay
```

### Modificar un array

```js
let colores = ["rojo", "verde", "azul"];

colores.push("amarillo");        // agrega al final
colores.pop();                   // elimina el último
colores.unshift("negro");        // agrega al inicio
colores.shift();                 // elimina el primero

console.log(colores.includes("verde")); // true
console.log(colores.indexOf("azul"));   // 1 — posición donde está
```

### Recorrer un array

```js
let animales = ["perro", "gato", "pájaro"];

animales.forEach(function(animal) {
  console.log(animal);
});
// → perro
// → gato
// → pájaro
```

---

## Objetos

Un **objeto** agrupa información relacionada bajo un mismo nombre. En lugar de posiciones numéricas (como los arrays), usa **llaves o claves** (keys) con nombres descriptivos.

Piénsalo como una ficha de datos: la ficha de una persona tiene nombre, edad, ciudad...

```js
let persona = {
  nombre: "Luis",
  edad: 25,
  ciudad: "Ciudad de México"
};

console.log(persona.nombre);  // "Luis"
console.log(persona.edad);    // 25
console.log(persona["ciudad"]); // "Ciudad de México" — otra forma de acceder
```

### Modificar y agregar propiedades

```js
persona.edad = 26;           // modificar
persona.profesion = "médico"; // agregar nueva propiedad
delete persona.ciudad;        // eliminar

console.log(persona);
```

### Objetos dentro de arrays

En la práctica, casi siempre trabajarás con **arrays de objetos**: una lista de fichas.

```js
let estudiantes = [
  { nombre: "Ana",   calificacion: 9.5 },
  { nombre: "Pedro", calificacion: 8.0 },
  { nombre: "Sofía", calificacion: 9.8 }
];

console.log(estudiantes[0].nombre);       // "Ana"
console.log(estudiantes[2].calificacion); // 9.8
```

---

## typeof — saber el tipo de un dato

```js
console.log(typeof "hola");   // "string"
console.log(typeof 42);       // "number"
console.log(typeof true);     // "boolean"
console.log(typeof null);     // "object" ← ¡ojo! esto es una rareza histórica de JS
console.log(typeof undefined);// "undefined"
console.log(typeof []);       // "object"
console.log(typeof {});       // "object"
```

---

## Resumen visual

```
Tipos básicos:
  "texto"      → string
  42 / 3.14    → number
  true / false → boolean
  null         → nada (intencional)
  undefined    → sin valor asignado

Estructuras:
  ["a", "b", "c"]           → array  (lista ordenada, índice numérico)
  { clave: "valor" }        → objeto (colección con nombre)
  [{ a: 1 }, { a: 2 }]     → array de objetos (lo más común en APIs)
```

---

[← Consola y navegador](14-js-consola-navegador.md) | [Siguiente: Programación básica →](16-js-programacion-basica.md)
