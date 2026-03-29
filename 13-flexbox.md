# 13 — Flexbox

[← Modelo de caja](12-modelo-caja.md) | [← Índice](README.md)

---

## ¿Por qué necesitamos Flexbox?

Antes de Flexbox, alinear elementos en CSS era complicado y requería trucos. Flexbox es un sistema de diseño que hace que distribuir y alinear elementos sea sencillo e intuitivo.

---

## El concepto central: contenedor y elementos

Flexbox trabaja con dos niveles:

- **Contenedor flex** (flex container): el elemento padre al que le aplicas `display: flex`.
- **Elementos flex** (flex items): los hijos directos del contenedor.

```html
<div class="contenedor">    <!-- flex container -->
  <div class="item">A</div> <!-- flex item -->
  <div class="item">B</div> <!-- flex item -->
  <div class="item">C</div> <!-- flex item -->
</div>
```

```css
.contenedor {
  display: flex;
}
```

Con solo esa línea, los tres `div` (que normalmente se apilan verticalmente) aparecerán en fila horizontal.

---

## El eje principal y el eje cruzado

Flexbox tiene dos ejes:

```
── eje principal (main axis) ──→
│
▼  eje cruzado (cross axis)
```

- El **eje principal** es la dirección en que se colocan los elementos.
- El **eje cruzado** es el eje perpendicular.

Por defecto el eje principal es horizontal (de izquierda a derecha).

---

## Propiedades del contenedor

### `flex-direction` — dirección del eje principal

```css
.contenedor {
  flex-direction: row;            /* izquierda → derecha (default) */
  flex-direction: row-reverse;    /* derecha → izquierda */
  flex-direction: column;         /* arriba → abajo */
  flex-direction: column-reverse; /* abajo → arriba */
}
```

### `justify-content` — alineación en el eje principal

```css
.contenedor {
  justify-content: flex-start;    /* al inicio (default) */
  justify-content: flex-end;      /* al final */
  justify-content: center;        /* centrado */
  justify-content: space-between; /* espacio entre elementos, sin espacio en extremos */
  justify-content: space-around;  /* espacio alrededor de cada elemento */
  justify-content: space-evenly;  /* espacio igual entre todos */
}
```

### `align-items` — alineación en el eje cruzado

```css
.contenedor {
  align-items: stretch;     /* estira al alto del contenedor (default) */
  align-items: flex-start;  /* arriba */
  align-items: flex-end;    /* abajo */
  align-items: center;      /* centrado verticalmente */
  align-items: baseline;    /* alineado a la línea base del texto */
}
```

### `gap` — espacio entre elementos

```css
.contenedor {
  gap: 16px;          /* mismo espacio en filas y columnas */
  gap: 10px 20px;     /* fila | columna */
}
```

### `flex-wrap` — ¿qué hacer si no caben todos?

```css
.contenedor {
  flex-wrap: nowrap;   /* todos en una línea, aunque se salgan (default) */
  flex-wrap: wrap;     /* los que no caben pasan a la siguiente línea */
}
```

---

## Propiedades de los elementos (flex items)

### `flex` — cuánto espacio ocupa cada elemento

La propiedad `flex` es un atajo para tres propiedades (`flex-grow`, `flex-shrink`, `flex-basis`). La más común:

```css
.item {
  flex: 1;   /* todos los elementos comparten el espacio por igual */
}

.item-grande {
  flex: 2;   /* ocupa el doble que un elemento con flex: 1 */
}
```

### `align-self` — alineación individual en el eje cruzado

Sobreescribe `align-items` para un elemento específico:

```css
.item-especial {
  align-self: flex-end;
}
```

### `order` — cambiar el orden visual

```css
.primero { order: -1; }  /* aparece antes que todos */
.ultimo  { order: 1; }   /* aparece después que todos */
```

---

## Casos de uso comunes

### Centrar algo perfectamente (horizontal y vertical)

```css
.contenedor {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;  /* ocupa toda la altura de la ventana */
}
```

### Barra de navegación

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
}
```

```html
<nav>
  <div class="logo">Mi Sitio</div>
  <ul>
    <li><a href="/">Inicio</a></li>
    <li><a href="/blog">Blog</a></li>
    <li><a href="/contacto">Contacto</a></li>
  </ul>
</nav>
```

### Tarjetas en una fila que se adaptan

```css
.galeria {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.tarjeta {
  flex: 1 1 250px;   /* crece, se encoge, y mínimo 250px de ancho */
}
```

---

## Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Flexbox</title>
    <style>
      * { box-sizing: border-box; margin: 0; padding: 0; }

      body {
        font-family: sans-serif;
        min-height: 100vh;
        display: flex;
        flex-direction: column;
      }

      header {
        background: #1a1a2e;
        color: white;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 16px 32px;
      }

      nav a {
        color: white;
        text-decoration: none;
        margin-left: 24px;
      }

      main {
        flex: 1;
        padding: 40px 32px;
      }

      .tarjetas {
        display: flex;
        flex-wrap: wrap;
        gap: 24px;
        margin-top: 24px;
      }

      .tarjeta {
        flex: 1 1 220px;
        background: #f0f0f0;
        border-radius: 8px;
        padding: 24px;
        display: flex;
        flex-direction: column;
        gap: 12px;
      }

      footer {
        background: #333;
        color: white;
        text-align: center;
        padding: 16px;
      }
    </style>
  </head>
  <body>

    <header>
      <span>Mi Sitio</span>
      <nav>
        <a href="#">Inicio</a>
        <a href="#">Productos</a>
        <a href="#">Contacto</a>
      </nav>
    </header>

    <main>
      <h1>Nuestros productos</h1>
      <div class="tarjetas">
        <div class="tarjeta">
          <h2>Producto A</h2>
          <p>Descripción del producto A.</p>
          <a href="#">Ver más</a>
        </div>
        <div class="tarjeta">
          <h2>Producto B</h2>
          <p>Descripción del producto B.</p>
          <a href="#">Ver más</a>
        </div>
        <div class="tarjeta">
          <h2>Producto C</h2>
          <p>Descripción del producto C.</p>
          <a href="#">Ver más</a>
        </div>
      </div>
    </main>

    <footer>
      <p>© 2026 Mi Sitio Web</p>
    </footer>

  </body>
</html>
```

---

## Referencia visual rápida

| Propiedad | Aplica a | Valores clave |
|-----------|----------|---------------|
| `display: flex` | Contenedor | Activa Flexbox |
| `flex-direction` | Contenedor | `row`, `column` |
| `justify-content` | Contenedor | `center`, `space-between`, `space-evenly` |
| `align-items` | Contenedor | `center`, `flex-start`, `flex-end`, `stretch` |
| `flex-wrap` | Contenedor | `wrap`, `nowrap` |
| `gap` | Contenedor | `16px`, `10px 20px` |
| `flex` | Elemento | `1`, `2`, `1 1 200px` |
| `align-self` | Elemento | `center`, `flex-end` |
| `order` | Elemento | `-1`, `0`, `1` |

---

## Recurso para practicar

**[Flexbox Froggy](https://flexboxfroggy.com/#es)** — un juego interactivo donde guías a una rana hasta su lilypad usando propiedades de Flexbox. Cubre `justify-content`, `align-items`, `flex-direction`, `flex-wrap` y más en 24 niveles. Disponible en español.

---

[← Modelo de caja](12-modelo-caja.md) | [← Índice](README.md)
