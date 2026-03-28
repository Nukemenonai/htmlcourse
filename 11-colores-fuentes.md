# 11 — Colores, fuentes, ancho y alto

[← Especificidad](10-especificidad.md) | [Siguiente: Modelo de caja →](12-modelo-caja.md)

---

## Colores

CSS ofrece varias formas de especificar un color.

### Por nombre

CSS tiene 140 nombres de colores predefinidos en inglés:

```css
color: red;
color: blue;
color: darkgreen;
color: coral;
color: tomato;
```

Útiles para aprender, pero limitados para diseños reales.

### Hexadecimal (`#RRGGBB`)

El formato más común. Combina valores de rojo, verde y azul en base 16 (00 a FF):

```css
color: #ff0000;   /* rojo puro */
color: #00ff00;   /* verde puro */
color: #0000ff;   /* azul puro */
color: #ffffff;   /* blanco */
color: #000000;   /* negro */
color: #3a86ff;   /* azul medio */
```

Si cada par de dígitos es igual, puedes abreviarlo a 3 dígitos:

```css
color: #fff;   /* equivale a #ffffff */
color: #f00;   /* equivale a #ff0000 */
```

### RGB

```css
color: rgb(255, 0, 0);       /* rojo */
color: rgb(58, 134, 255);    /* azul medio */
```

Cada valor va de 0 a 255.

### RGBA (con transparencia)

El cuarto valor (alpha) va de 0 (transparente) a 1 (opaco):

```css
color: rgba(0, 0, 0, 0.5);         /* negro al 50% de opacidad */
background-color: rgba(255, 0, 0, 0.2);  /* rojo muy transparente */
```

### HSL (Hue, Saturation, Lightness)

Muy intuitivo para elegir variaciones de un color:

```css
color: hsl(220, 80%, 55%);   /* tono azul, saturación 80%, luminosidad 55% */
```

---

## Propiedades de color

```css
selector {
  color: #333;                  /* color del texto */
  background-color: #f5f5f5;    /* color de fondo del elemento */
  border-color: #ccc;           /* color del borde */
  opacity: 0.8;                 /* transparencia del elemento entero (0-1) */
}
```

---

## Fuentes

### `font-family`

Define el tipo de letra. Se listan alternativas por si la primera no está instalada:

```css
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
```

El navegador prueba cada fuente en orden y usa la primera que encuentre. La última siempre debe ser una fuente genérica: `serif`, `sans-serif`, `monospace`, `cursive`.

### Fuentes de Google

Google Fonts ofrece cientos de fuentes gratuitas. Para usarlas:

1. Ve a [fonts.google.com](https://fonts.google.com), elige una fuente y copia el `<link>`.
2. Pégalo en el `<head>` de tu HTML **antes** de tu CSS:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet" />
```

3. Úsala en tu CSS:

```css
body {
  font-family: "Inter", sans-serif;
}
```

### Tamaño de fuente: `font-size`

```css
p     { font-size: 16px; }
h1    { font-size: 2rem; }     /* 2 veces el tamaño base del documento */
small { font-size: 0.85em; }   /* 85% del tamaño del elemento padre */
```

### Grosor: `font-weight`

```css
font-weight: normal;   /* igual a 400 */
font-weight: bold;     /* igual a 700 */
font-weight: 300;      /* delgado (si la fuente lo soporta) */
font-weight: 600;      /* semi-negrita */
```

### Estilo: `font-style`

```css
font-style: normal;
font-style: italic;
```

### Altura de línea: `line-height`

Controla el espacio entre líneas de texto. Un valor entre 1.4 y 1.8 mejora la legibilidad:

```css
p {
  line-height: 1.6;  /* sin unidad: relativo al font-size del elemento */
}
```

---

## Ancho y alto

### `width` y `height`

```css
img {
  width: 300px;
  height: 200px;
}

div {
  width: 50%;          /* 50% del ancho del elemento padre */
  height: 100vh;       /* 100% del alto de la ventana del navegador */
}
```

### `max-width` y `min-width`

Muy útiles para diseños adaptables:

```css
.contenedor {
  width: 100%;
  max-width: 1200px;  /* nunca más ancho que 1200px */
  min-width: 320px;   /* nunca más estrecho que 320px */
}
```

Un patrón muy común es centrar un contenedor:

```css
.contenedor {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;   /* auto en los lados centra el elemento horizontalmente */
}
```

---

## Ejemplo completo

```css
/* Tipografía base */
body {
  font-family: "Inter", sans-serif;
  font-size: 16px;
  color: #222;
  background-color: #fafafa;
  line-height: 1.6;
}

/* Títulos */
h1 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #1a1a2e;
}

h2 {
  font-size: 1.75rem;
  color: #16213e;
}

/* Enlace */
a {
  color: #3a86ff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

/* Contenedor principal */
.contenedor {
  width: 90%;
  max-width: 800px;
  margin: 0 auto;
}

/* Imagen responsiva */
img {
  width: 100%;
  height: auto;   /* mantiene la proporción */
}
```

---

[← Especificidad](10-especificidad.md) | [Siguiente: Modelo de caja →](12-modelo-caja.md)
