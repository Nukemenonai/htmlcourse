# 06 — Etiquetas semánticas

[← Etiquetas HTML](05-etiquetas-html.md) | [Siguiente: Formularios →](07-formularios.md)

---

## ¿Qué significa "semántico"?

**Semántica** significa significado. Una etiqueta semántica es aquella cuyo nombre describe el rol o el propósito del contenido que envuelve, no solo cómo se ve.

Compara estas dos opciones:

```html
<!-- Sin semántica: solo dice "es un bloque" -->
<div>
  <div>Logo y menú de navegación</div>
  <div>Artículo principal</div>
  <div>Barra lateral</div>
  <div>Pie de página</div>
</div>

<!-- Con semántica: describe qué es cada parte -->
<body>
  <header>Logo y menú de navegación</header>
  <main>Artículo principal</main>
  <aside>Barra lateral</aside>
  <footer>Pie de página</footer>
</body>
```

Ambas se ven igual en el navegador, pero la versión semántica comunica estructura y significado.

---

## ¿Por qué usar etiquetas semánticas?

1. **Accesibilidad** — los lectores de pantalla para personas con discapacidad visual usan las etiquetas para navegar la página ("ir al menú principal", "saltar al contenido").
2. **SEO** — los motores de búsqueda como Google entienden mejor el contenido y pueden posicionarlo mejor.
3. **Mantenibilidad** — es más fácil leer y editar código que dice `<nav>` que uno lleno de `<div id="div3">`.

---

## Las etiquetas semánticas principales

### `<header>`
Cabecera de la página o de una sección. Generalmente contiene el logo, el nombre del sitio y la navegación principal.

```html
<header>
  <h1>Mi Blog</h1>
  <nav>
    <a href="index.html">Inicio</a>
    <a href="sobre-mi.html">Sobre mí</a>
  </nav>
</header>
```

### `<nav>`
Bloque de navegación: los menús y enlaces principales del sitio.

```html
<nav>
  <ul>
    <li><a href="/">Inicio</a></li>
    <li><a href="/productos">Productos</a></li>
    <li><a href="/contacto">Contacto</a></li>
  </ul>
</nav>
```

### `<main>`
El contenido principal de la página. Solo debe haber uno por página.

```html
<main>
  <h2>Bienvenido</h2>
  <p>Este es el contenido principal del sitio.</p>
</main>
```

### `<article>`
Contenido independiente que tiene sentido por sí solo: una entrada de blog, una noticia, un comentario.

```html
<article>
  <h2>El futuro de la web</h2>
  <p>Publicado el 28 de marzo de 2026</p>
  <p>La web está evolucionando rápidamente…</p>
</article>
```

### `<section>`
Un grupo temático de contenido. A diferencia de `<article>`, no necesita tener sentido fuera de la página.

```html
<section>
  <h2>Nuestros servicios</h2>
  <p>Descripción de los servicios…</p>
</section>
```

### `<aside>`
Contenido complementario, relacionado pero no esencial: barras laterales, publicidad, datos relacionados.

```html
<aside>
  <h3>Artículos relacionados</h3>
  <ul>
    <li><a href="#">Otro artículo</a></li>
  </ul>
</aside>
```

### `<footer>`
Pie de página: derechos de autor, enlaces legales, información de contacto.

```html
<footer>
  <p>© 2026 Mi Sitio Web. Todos los derechos reservados.</p>
  <a href="privacidad.html">Política de privacidad</a>
</footer>
```

---

## Estructura típica de una página con semántica

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi sitio</title>
  </head>
  <body>

    <header>
      <h1>Mi Blog</h1>
      <nav>
        <a href="/">Inicio</a>
        <a href="/archivo">Archivo</a>
      </nav>
    </header>

    <main>
      <article>
        <h2>Mi primer artículo</h2>
        <p>Contenido del artículo…</p>
      </article>

      <aside>
        <h3>Sobre el autor</h3>
        <p>Información del autor…</p>
      </aside>
    </main>

    <footer>
      <p>© 2026 Mi Blog</p>
    </footer>

  </body>
</html>
```

---

## `<div>` y `<span>`: cuando no hay una etiqueta semántica adecuada

- `<div>` — contenedor de bloque genérico. Úsalo cuando ninguna etiqueta semántica encaja.
- `<span>` — contenedor en línea genérico. Úsalo para dar estilo a una parte del texto.

```html
<p>El precio es <span style="color: red;">$100</span> por unidad.</p>
```

La regla general: **primero busca una etiqueta semántica; solo usa `<div>` o `<span>` si no encuentras una que aplique.**

---

[← Etiquetas HTML](05-etiquetas-html.md) | [Siguiente: Formularios →](07-formularios.md)
