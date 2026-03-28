# 04 — Sintaxis básica y estructura HTML

[← Escribir un archivo](03-escribir-archivo.md) | [Siguiente: Etiquetas HTML →](05-etiquetas-html.md)

---

## ¿Qué es HTML?

**HTML** (HyperText Markup Language) es el lenguaje con el que describes el contenido de una página web. No es un lenguaje de programación — no tiene lógica ni cálculos — es un lenguaje de **marcado**: le pones etiquetas al contenido para decirle al navegador qué es cada cosa.

Por ejemplo, le dices: "esto es un título", "esto es un párrafo", "esto es una imagen". El navegador toma esa información y la muestra en pantalla.

---

## Las etiquetas (tags)

La unidad básica de HTML es la **etiqueta**. Se escribe con el nombre rodeado de signos `<` y `>`.

La mayoría de las etiquetas vienen en par: una de **apertura** y una de **cierre** (con una barra `/`):

```html
<etiqueta>contenido</etiqueta>
```

Ejemplo real:

```html
<p>Este es un párrafo de texto.</p>
```

- `<p>` — etiqueta de apertura
- `Este es un párrafo de texto.` — contenido
- `</p>` — etiqueta de cierre

Algunas etiquetas no tienen contenido y se cierran solas (se llaman **etiquetas vacías**):

```html
<img src="foto.jpg" alt="Una foto" />
<br />
<hr />
```

---

## Los atributos

Las etiquetas pueden tener **atributos**: información extra que va dentro de la etiqueta de apertura.

```html
<etiqueta atributo="valor">contenido</etiqueta>
```

Ejemplo:

```html
<a href="https://google.com">Ir a Google</a>
```

- `href` es el atributo
- `"https://google.com"` es el valor
- El atributo siempre va dentro de la etiqueta de apertura, nunca en la de cierre

---

## La estructura completa de un documento HTML

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Título de la página</title>
  </head>
  <body>
    <!-- Aquí va el contenido visible -->
  </body>
</html>
```

El texto entre `<!--` y `-->` es un **comentario**: el navegador lo ignora completamente. Úsalos para dejar notas en tu código.

---

## ¿Por qué HTML es un árbol?

Si observas la estructura anterior con atención, notarás que las etiquetas se **anidan** unas dentro de otras. Esto crea una jerarquía que los programadores llaman **árbol**.

```
html
├── head
│   ├── meta
│   └── title
└── body
    ├── h1
    ├── p
    └── div
        ├── p
        └── a
```

Esta estructura se llama el **DOM** (Document Object Model). Cada etiqueta es un **nodo** del árbol.

Las relaciones entre nodos tienen nombres específicos:

| Término | Significado |
|---------|-------------|
| **Padre** | La etiqueta que contiene a otra |
| **Hijo** | La etiqueta que está dentro de otra |
| **Hermano** | Etiquetas al mismo nivel dentro del mismo padre |

En el ejemplo de arriba:
- `html` es el padre de `head` y `body`
- `head` y `body` son hermanos
- `meta` y `title` son hijos de `head`

### ¿Por qué importa entender el árbol?

- El navegador construye la página siguiendo esta jerarquía.
- CSS usa la jerarquía para aplicar estilos (un estilo en el padre puede heredarse al hijo).
- JavaScript usa el árbol para encontrar y modificar elementos.
- Un error de anidación (cerrar una etiqueta en el orden incorrecto) puede romper toda la página.

---

## Regla de anidación: siempre cerrar en orden inverso

Las etiquetas deben cerrarse en el orden inverso en que se abrieron. Piénsalo como capas de una cebolla: la última que pusiste es la primera que quitas.

**Correcto:**
```html
<div>
  <p>Texto <strong>importante</strong></p>
</div>
```

**Incorrecto:**
```html
<div>
  <p>Texto <strong>importante</p></strong>  <!-- ¡MAL! -->
</div>
```

---

## Indentación: el código ordenado se lee mejor

Aunque el navegador ignora los espacios y saltos de línea extra, es buena práctica **indentar** (agregar espacios al inicio de la línea) cada nivel de anidación. VS Code lo hace automáticamente si presionas `Tab`.

```html
<!-- Sin indentación — difícil de leer -->
<body><div><p>Hola</p></div></body>

<!-- Con indentación — fácil de leer -->
<body>
  <div>
    <p>Hola</p>
  </div>
</body>
```

---

[← Escribir un archivo](03-escribir-archivo.md) | [Siguiente: Etiquetas HTML →](05-etiquetas-html.md)
