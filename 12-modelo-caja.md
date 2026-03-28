# 12 — El modelo de caja y el inspector de Chrome

[← Colores y fuentes](11-colores-fuentes.md) | [Siguiente: Flexbox →](13-flexbox.md)

---

## Cada elemento es una caja

En CSS, **cada elemento HTML es una caja rectangular**. Aunque no lo veas, un párrafo, una imagen, un botón — todos son cajas. Entender cómo funcionan esas cajas es fundamental para controlar el diseño de tu página.

---

## Las capas del modelo de caja

El modelo de caja tiene cuatro capas, de adentro hacia afuera:

```
┌─────────────────────────────────────────┐
│               MARGIN                    │  ← espacio fuera del elemento
│  ┌───────────────────────────────────┐  │
│  │             BORDER                │  │  ← el borde
│  │  ┌─────────────────────────────┐  │  │
│  │  │           PADDING           │  │  │  ← espacio interior
│  │  │  ┌───────────────────────┐  │  │  │
│  │  │  │                       │  │  │  │
│  │  │  │       CONTENT         │  │  │  │  ← el contenido real
│  │  │  │                       │  │  │  │
│  │  │  └───────────────────────┘  │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

| Capa | Propiedad CSS | ¿Qué es? |
|------|--------------|----------|
| Content | `width`, `height` | El contenido del elemento (texto, imagen…) |
| Padding | `padding` | Espacio entre el contenido y el borde |
| Border | `border` | La línea que rodea el padding y el contenido |
| Margin | `margin` | Espacio entre el borde y los elementos vecinos |

---

## Padding

Espacio interior entre el contenido y el borde:

```css
div {
  padding: 20px;                     /* los 4 lados iguales */
  padding: 10px 20px;                /* arriba/abajo  |  izq/der */
  padding: 10px 20px 15px 5px;       /* arriba | der | abajo | izq (sentido horario) */

  /* También por lado: */
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 10px;
  padding-left: 20px;
}
```

---

## Border

```css
div {
  border: 2px solid #333;      /* grosor  estilo  color */
  border-radius: 8px;          /* esquinas redondeadas */
}
```

Estilos de borde: `solid`, `dashed`, `dotted`, `double`, `none`.

Por lado:
```css
border-top: 3px solid red;
border-bottom: 1px dashed gray;
```

---

## Margin

Espacio exterior entre el elemento y sus vecinos:

```css
div {
  margin: 20px;
  margin: 10px auto;   /* auto en los lados: centra el elemento */
  margin-top: 40px;
  margin-bottom: 0;
}
```

**Colapso de márgenes:** cuando dos elementos bloque están uno encima del otro, sus márgenes verticales se fusionan (el mayor de los dos gana). Es un comportamiento normal de CSS, pero puede sorprender al principio.

---

## `box-sizing: border-box`

Por defecto, `width` en CSS mide solo el **contenido**. Si le agregas padding y border, el elemento se vuelve más grande que `width`. Esto es confuso.

La solución es usar `box-sizing: border-box`, que hace que `width` incluya el padding y el border:

```css
/* Recomendado: pon esto al inicio de tu CSS */
*, *::before, *::after {
  box-sizing: border-box;
}
```

Con `border-box`, un elemento con `width: 200px`, `padding: 20px` y `border: 2px solid` seguirá midiendo **200px** en total. Sin él, mediría 244px.

---

## Elementos de bloque vs. elementos en línea

Esta distinción afecta cómo se comportan las cajas:

| Tipo | Comportamiento | Ejemplos |
|------|---------------|---------|
| **Bloque** | Ocupa todo el ancho disponible. El siguiente elemento baja a una nueva línea. Acepta `width`, `height`, `margin` y `padding` en todos los lados. | `div`, `p`, `h1`-`h6`, `section`, `article` |
| **En línea** | Solo ocupa lo que necesita. No fuerza salto de línea. `width` y `height` no tienen efecto. | `span`, `a`, `strong`, `em`, `img` |
| **Inline-block** | Fluye en línea pero acepta `width`, `height` y todos los márgenes. | (configurado con CSS) |

```css
span {
  display: inline-block;
  width: 100px;
  padding: 10px;
}
```

---

## El inspector de Chrome

El **inspector de Chrome** (también llamado DevTools) es tu mejor herramienta para depurar CSS. Te muestra exactamente cómo el navegador interpreta tu código.

### Cómo abrirlo

- Atajo: `F12` o `Ctrl + Shift + I`
- Clic derecho sobre cualquier elemento → **Inspeccionar**

### La pestaña Elements

Muestra el HTML de la página. Al hacer clic en un elemento, el panel de la derecha muestra sus estilos CSS.

### El panel Styles

Muestra todas las reglas CSS aplicadas al elemento seleccionado, en orden de especificidad (las más específicas arriba). Las reglas tachadas fueron sobreescritas.

Puedes **editar los valores directamente** en el inspector. Los cambios son temporales (se pierden al recargar), pero son perfectos para experimentar.

### El diagrama del modelo de caja

En la pestaña **Computed** (o al final del panel **Styles**) verás un diagrama interactivo del modelo de caja:

```
┌─────────────────────┐
│       margin        │
│  ┌───────────────┐  │
│  │    border     │  │
│  │  ┌─────────┐  │  │
│  │  │ padding │  │  │
│  │  │ ┌─────┐ │  │  │
│  │  │ │ 200 │ │  │  │
│  │  │ │  x  │ │  │  │
│  │  │ │ 100 │ │  │  │
│  │  │ └─────┘ │  │  │
│  │  └─────────┘  │  │
│  └───────────────┘  │
└─────────────────────┘
```

Muestra los valores exactos de cada capa. Puedes hacer clic en cualquier número y editarlo.

### Trucos útiles del inspector

- **Hover sobre un elemento en el panel Elements** → el navegador resalta ese elemento en la página.
- **Añadir una clase temporal** → en el panel Styles, haz clic en `.cls` para agregar clases sin editar el HTML.
- **Forzar estados** → haz clic en `:hov` para simular `:hover`, `:focus`, etc.
- **Ver en responsive** → `Ctrl + Shift + M` activa el modo de dispositivo móvil.

---

[← Colores y fuentes](11-colores-fuentes.md) | [Siguiente: Flexbox →](13-flexbox.md)
