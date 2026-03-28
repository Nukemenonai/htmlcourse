# 08 — Sintaxis de CSS

[← Formularios](07-formularios.md) | [Siguiente: ¿Dónde escribir CSS? →](09-donde-escribir-css.md)

---

## ¿Qué es CSS?

**CSS** (Cascading Style Sheets, u Hojas de Estilo en Cascada) es el lenguaje que controla cómo se ve una página web: colores, fuentes, tamaños, posiciones, animaciones…

HTML define el contenido y la estructura. CSS define la presentación. Son lenguajes distintos pero trabajan juntos.

---

## La regla CSS

La unidad básica de CSS se llama **regla**. Tiene esta forma:

```css
selector {
  propiedad: valor;
  propiedad: valor;
}
```

Ejemplo real:

```css
p {
  color: blue;
  font-size: 18px;
}
```

Esto le dice al navegador: "a todos los elementos `<p>`, ponles el texto azul y tamaño de 18 píxeles".

---

## Las partes de una regla CSS

```
    selector
       │
       ▼
   h1, h2 {
     color: red;        ◄── declaración
     ▲          ▲
  propiedad   valor
   }
```

| Parte | ¿Qué es? | Ejemplo |
|-------|----------|---------|
| **Selector** | A qué elementos HTML aplica el estilo | `p`, `h1`, `.titulo`, `#logo` |
| **Propiedad** | Qué aspecto visual se cambia | `color`, `font-size`, `background` |
| **Valor** | El valor concreto para esa propiedad | `red`, `20px`, `#fff` |
| **Declaración** | El par propiedad + valor | `color: red;` |

Cada declaración termina con punto y coma `;`. Olvidarlo es uno de los errores más comunes.

---

## Tipos de selectores

### Selector de etiqueta (tipo)

Selecciona todas las etiquetas de ese tipo:

```css
p {
  color: gray;
}
```

Afecta a **todos** los `<p>` de la página.

### Selector de clase (`.`)

Selecciona elementos que tengan ese `class` en el HTML. En CSS se escribe con un punto:

```css
.destacado {
  background-color: yellow;
}
```

En el HTML:
```html
<p class="destacado">Este párrafo tiene fondo amarillo.</p>
<p>Este no.</p>
```

Un elemento puede tener varias clases separadas por espacio:
```html
<p class="destacado grande">Texto grande y destacado</p>
```

### Selector de ID (`#`)

Selecciona el elemento con ese `id` específico. En CSS se escribe con `#`:

```css
#logo {
  width: 200px;
}
```

En el HTML:
```html
<img id="logo" src="logo.png" alt="Logo" />
```

Un `id` debe ser **único** en toda la página (no puede haber dos elementos con el mismo `id`).

### Selector universal (`*`)

Selecciona absolutamente todos los elementos:

```css
* {
  box-sizing: border-box;
}
```

### Selectores múltiples

Puedes aplicar la misma regla a varios selectores separándolos con coma:

```css
h1, h2, h3 {
  font-family: sans-serif;
}
```

---

## Comentarios en CSS

```css
/* Esto es un comentario y el navegador lo ignora */

p {
  color: red; /* Este también es un comentario */
}
```

---

## Propiedades básicas de texto

```css
p {
  color: navy;              /* color del texto */
  font-size: 16px;          /* tamaño de fuente */
  font-weight: bold;        /* grosor: normal, bold, o número 100-900 */
  font-style: italic;       /* cursiva */
  text-align: center;       /* alineación: left, right, center, justify */
  text-decoration: none;    /* subrayado: none, underline, line-through */
  line-height: 1.6;         /* espacio entre líneas */
  letter-spacing: 2px;      /* espacio entre letras */
}
```

---

## Unidades de medida

| Unidad | Tipo | Descripción |
|--------|------|-------------|
| `px` | Absoluta | Píxeles. Medida fija. |
| `%` | Relativa | Porcentaje del elemento padre |
| `em` | Relativa | Relativa al tamaño de fuente del elemento padre |
| `rem` | Relativa | Relativa al tamaño de fuente del elemento raíz (`html`) |
| `vw` | Relativa | Porcentaje del ancho de la ventana del navegador |
| `vh` | Relativa | Porcentaje del alto de la ventana del navegador |

Para empezar, usa `px` para tamaños fijos y `%` o `rem` cuando quieras que algo se adapte.

---

[← Formularios](07-formularios.md) | [Siguiente: ¿Dónde escribir CSS? →](09-donde-escribir-css.md)
