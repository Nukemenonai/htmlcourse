# 10 — Especificidad y cascada

[← ¿Dónde escribir CSS?](09-donde-escribir-css.md) | [Siguiente: Colores y fuentes →](11-colores-fuentes.md)

---

## El problema que resuelve la especificidad

Imagina que tienes esto:

```css
p {
  color: blue;
}

.aviso {
  color: red;
}
```

Y en el HTML:

```html
<p class="aviso">¿De qué color soy?</p>
```

Este párrafo tiene las dos reglas. ¿Cuál gana? La respuesta la da la **especificidad**.

---

## ¿Qué es la cascada?

CSS significa *Cascading* Style Sheets — "en cascada". Esto significa que cuando varias reglas compiten por aplicarse al mismo elemento, el navegador sigue un orden de prioridad para decidir cuál gana.

Ese orden tiene tres niveles:

1. **Especificidad** — qué tan específico es el selector.
2. **Orden de aparición** — si la especificidad es igual, gana la que está más abajo en el código.
3. **Herencia** — algunas propiedades se heredan del elemento padre al hijo.

---

## Cómo se calcula la especificidad

La especificidad se puede pensar como un número de tres dígitos: **(A, B, C)**

| Nivel | Qué cuenta | Puntos |
|-------|-----------|--------|
| **A** | Estilos en línea (`style="…"`) | 1000 |
| **B** | IDs (`#id`) | 100 |
| **C** | Clases (`.clase`), atributos (`[type]`), pseudoclases (`:hover`) | 10 |
| **D** | Etiquetas (`p`, `h1`, `div`) y pseudoelementos (`::before`) | 1 |

Se suman los puntos de todos los selectores en una regla. **Gana el puntaje más alto.**

### Ejemplos

| Selector | A | B | C | D | Total |
|----------|---|---|---|---|-------|
| `p` | 0 | 0 | 0 | 1 | **1** |
| `.aviso` | 0 | 0 | 1 | 0 | **10** |
| `p.aviso` | 0 | 0 | 1 | 1 | **11** |
| `#logo` | 0 | 1 | 0 | 0 | **100** |
| `style="…"` | 1 | 0 | 0 | 0 | **1000** |

Volviendo al ejemplo inicial:

```css
p         { color: blue; }   /* especificidad: 1 */
.aviso    { color: red; }    /* especificidad: 10 */
```

`.aviso` tiene más especificidad → el párrafo será **rojo**.

---

## Nivel que sobreescribe a cuál

De menor a mayor prioridad:

```
1. Herencia del padre
       ↓
2. Selector de etiqueta (p, h1, div)    → especificidad: 1
       ↓
3. Selector de clase (.clase)           → especificidad: 10
       ↓
4. Selector de ID (#id)                 → especificidad: 100
       ↓
5. Estilo en línea (style="…")          → especificidad: 1000
       ↓
6. !important                           → siempre gana (evitar)
```

---

## El orden de aparición como desempate

Si dos reglas tienen la misma especificidad, **gana la que aparece después**:

```css
p { color: blue; }
p { color: green; } /* ← gana esta */
```

El texto será verde.

Esto también aplica entre archivos CSS: si enlazas dos archivos, el segundo puede sobreescribir al primero.

---

## `!important` — el comodín (que debes evitar)

Puedes forzar que una declaración gane sobre todas usando `!important`:

```css
p {
  color: blue !important;
}

#titulo {
  color: red; /* pierde, aunque tiene más especificidad */
}
```

**¿Por qué evitarlo?**
- Rompe el flujo natural de la cascada.
- Una vez que lo usas en un lugar, tienes que usarlo en todos los que quieras sobreescribir.
- Hace el código muy difícil de mantener.

Úsalo solo como último recurso, por ejemplo cuando necesitas sobreescribir CSS de una librería de terceros que no puedes modificar.

---

## Herencia

Algunas propiedades CSS se **heredan** automáticamente del padre al hijo:

```css
body {
  font-family: sans-serif;
  color: #333;
}
```

Todos los elementos dentro de `<body>` (párrafos, títulos, listas…) heredarán esa fuente y ese color **a menos que tengan una regla más específica que los sobreescriba**.

Propiedades que **sí se heredan**: `color`, `font-family`, `font-size`, `font-weight`, `line-height`, `text-align`…

Propiedades que **no se heredan**: `margin`, `padding`, `border`, `background`, `width`, `height`…

---

## Ejemplo práctico completo

```html
<p id="parrafo1" class="resaltado" style="color: orange;">
  ¿De qué color soy?
</p>
```

```css
p            { color: blue; }     /* especificidad 1    → azul */
.resaltado   { color: green; }    /* especificidad 10   → verde */
#parrafo1    { color: purple; }   /* especificidad 100  → morado */
/* style="color: orange"          /* especificidad 1000 → naranja */
```

El texto será **naranja** porque el estilo en línea tiene la mayor especificidad.

---

## Consejo práctico

Estructura tus selectores de menor a mayor especificidad en el archivo CSS:

1. Estilos generales para etiquetas (reset, tipografía base).
2. Estilos por clase para componentes.
3. Ajustes por ID solo cuando sea estrictamente necesario.
4. Nunca uses estilos en línea en producción.

---

## Recurso para practicar

**[CSS Diner](https://flukeout.github.io)** — un juego interactivo donde practicas selectores CSS seleccionando elementos de una mesa. Cubre selectores de etiqueta, clase, ID, combinadores, pseudoclases y más, con 32 niveles de dificultad progresiva.

---

[← ¿Dónde escribir CSS?](09-donde-escribir-css.md) | [Siguiente: Colores y fuentes →](11-colores-fuentes.md)
