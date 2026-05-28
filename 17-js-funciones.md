# 17 — Funciones

[← Programación básica](16-js-programacion-basica.md) | [Siguiente: Fetch y promesas →](18-js-fetch-promesas.md)

---

## ¿Qué es una función?

Una **función** es un bloque de código con nombre al que puedes llamar cuando lo necesites. Es como una receta: la escribes una vez y la usas cuantas veces quieras.

Sin funciones, tendrías que copiar y pegar el mismo código en muchos lugares. Con funciones, lo escribes una vez y lo reutilizas.

---

## Declarar y llamar una función

```js
function saludar() {
  console.log("¡Hola!");
  console.log("Bienvenido al curso.");
}

saludar(); // llamar la función
saludar(); // llamarla de nuevo
```

La función no se ejecuta cuando la declaras — solo cuando la **llamas** con `()`.

---

## Parámetros y argumentos

Los **parámetros** son variables que la función recibe como entrada. Los **argumentos** son los valores que le pasas al llamarla.

```js
function saludar(nombre) {       // "nombre" es el parámetro
  console.log(`¡Hola, ${nombre}!`);
}

saludar("Ana");   // "Ana" es el argumento → ¡Hola, Ana!
saludar("Luis");  // → ¡Hola, Luis!
```

Puedes tener varios parámetros:

```js
function sumar(a, b) {
  console.log(a + b);
}

sumar(5, 3);   // → 8
sumar(10, 20); // → 30
```

---

## `return` — devolver un resultado

Hasta ahora las funciones solo hacen cosas (imprimen en consola). Pero lo más útil es que **devuelvan** un valor para usarlo después.

```js
function sumar(a, b) {
  return a + b;    // devuelve el resultado
}

let resultado = sumar(5, 3);
console.log(resultado);  // 8

console.log(sumar(10, 20) * 2); // 60 — puedes usar el resultado directamente
```

Cuando JavaScript llega a `return`, la función termina inmediatamente y devuelve ese valor.

---

## Parámetros con valores por defecto

Si no pasas un argumento, puedes definir un valor predeterminado:

```js
function saludar(nombre = "visitante") {
  console.log(`¡Hola, ${nombre}!`);
}

saludar("María"); // → ¡Hola, María!
saludar();        // → ¡Hola, visitante!
```

---

## Funciones flecha (arrow functions)

Las **arrow functions** son una forma más corta de escribir funciones. Son muy comunes en el código moderno.

```js
// Función tradicional
function multiplicar(a, b) {
  return a * b;
}

// Arrow function equivalente
const multiplicar = (a, b) => {
  return a * b;
};

// Forma aún más corta (cuando solo hay un return)
const multiplicar = (a, b) => a * b;
```

Si la función recibe **un solo parámetro**, puedes omitir los paréntesis:

```js
const doble = n => n * 2;

console.log(doble(5));  // 10
console.log(doble(8));  // 16
```

---

## Funciones como valores

En JavaScript las funciones son valores como cualquier otro — las puedes guardar en variables, pasarlas como argumento, o devolver desde otra función.

```js
const numeros = [1, 2, 3, 4, 5];

// Pasamos una función como argumento a .map()
const dobles = numeros.map(n => n * 2);
console.log(dobles); // [2, 4, 6, 8, 10]

// .filter() devuelve los elementos que cumplen la condición
const pares = numeros.filter(n => n % 2 === 0);
console.log(pares); // [2, 4]
```

---

## Alcance (scope)

Las variables declaradas dentro de una función solo existen dentro de ella. Esto se llama **alcance local**.

```js
function calcular() {
  let resultado = 100;
  console.log(resultado); // 100 — funciona
}

calcular();
console.log(resultado); // ¡ERROR! resultado no existe fuera de la función
```

Las variables declaradas fuera de cualquier función tienen **alcance global** y son accesibles desde cualquier lugar.

---

## Ejemplo integrador

```js
function calcularPromedio(calificaciones) {
  if (calificaciones.length === 0) return 0;

  let suma = 0;
  for (let cal of calificaciones) {
    suma += cal;
  }

  return suma / calificaciones.length;
}

function evaluarEstudiante(nombre, calificaciones) {
  const promedio = calcularPromedio(calificaciones);
  const estado = promedio >= 6 ? "APROBADO" : "REPROBADO";

  return {
    nombre,
    promedio: promedio.toFixed(1),
    estado
  };
}

const alumnos = [
  { nombre: "Ana",   notas: [8, 9, 7, 10] },
  { nombre: "Pedro", notas: [5, 4, 6, 3]  },
  { nombre: "Sofía", notas: [9, 10, 8, 9] }
];

for (let alumno of alumnos) {
  const reporte = evaluarEstudiante(alumno.nombre, alumno.notas);
  console.log(`${reporte.nombre}: promedio ${reporte.promedio} — ${reporte.estado}`);
}
// → Ana: promedio 8.5 — APROBADO
// → Pedro: promedio 4.5 — REPROBADO
// → Sofía: promedio 9.0 — APROBADO
```

> El `?` en `promedio >= 6 ? "APROBADO" : "REPROBADO"` se llama **operador ternario**. Es un `if/else` corto: `condición ? valorSiTrue : valorSiFalse`.

---

## Resumen

| Concepto | Ejemplo |
|----------|---------|
| Declarar función | `function nombre(params) { }` |
| Arrow function | `const nombre = (params) => { }` |
| Arrow compacta | `const doble = n => n * 2` |
| Devolver valor | `return valor` |
| Valor por defecto | `function f(x = 10) { }` |
| Pasar función | `array.map(n => n * 2)` |

---

[← Programación básica](16-js-programacion-basica.md) | [Siguiente: Fetch y promesas →](18-js-fetch-promesas.md)
