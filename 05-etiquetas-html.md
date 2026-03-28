# 05 — Etiquetas HTML esenciales

[← Sintaxis HTML](04-sintaxis-html.md) | [Siguiente: Etiquetas semánticas →](06-etiquetas-semanticas.md)

---

## Títulos: `<h1>` al `<h6>`

Los títulos organizan el contenido jerárquicamente. Hay seis niveles:

```html
<h1>Título principal (el más grande)</h1>
<h2>Subtítulo</h2>
<h3>Sección dentro del subtítulo</h3>
<h4>Subsección</h4>
<h5>Nivel 5</h5>
<h6>Nivel 6 (el más pequeño)</h6>
```

**Reglas importantes:**
- Usa un solo `<h1>` por página — es el título principal.
- No uses los títulos solo para hacer texto grande. Úsalos para estructurar el contenido.
- El orden jerárquico importa: no saltes de `<h1>` a `<h4>` sin usar `<h2>` y `<h3>` antes.

---

## Párrafos: `<p>`

El párrafo es el bloque de texto más común:

```html
<p>Este es el primer párrafo. Puede tener todo el texto que necesites.</p>
<p>Este es el segundo párrafo. El navegador agrega espacio entre ellos automáticamente.</p>
```

El navegador ignora los saltos de línea dentro del código. Si necesitas forzar un salto de línea dentro de un párrafo usa `<br />`:

```html
<p>Primera línea.<br />Segunda línea en el mismo párrafo.</p>
```

---

## Imágenes: `<img>`

La etiqueta `<img>` muestra una imagen. Es una etiqueta vacía (no tiene cierre):

```html
<img src="imagenes/foto.jpg" alt="Descripción de la foto" />
```

| Atributo | Función |
|----------|---------|
| `src` | Ruta o URL de la imagen |
| `alt` | Texto alternativo (se muestra si la imagen no carga; también lo leen los lectores de pantalla) |
| `width` | Ancho en píxeles (opcional) |
| `height` | Alto en píxeles (opcional) |

### Rutas de archivos

- `src="foto.jpg"` — la imagen está en la misma carpeta que el HTML.
- `src="imagenes/foto.jpg"` — la imagen está dentro de la subcarpeta `imagenes`.
- `src="https://ejemplo.com/foto.jpg"` — imagen de internet (URL completa).

---

## Enlaces: `<a>`

La etiqueta `<a>` (anchor) crea un enlace:

```html
<a href="https://google.com">Ir a Google</a>
<a href="pagina2.html">Ir a mi segunda página</a>
```

### Atributo `target`

Por defecto el enlace abre en la misma pestaña. Para abrirlo en una pestaña nueva:

```html
<a href="https://google.com" target="_blank">Abrir en nueva pestaña</a>
```

### Enlace a una sección de la misma página

Primero pon un `id` en el elemento de destino, luego enlaza con `#`:

```html
<h2 id="contacto">Contacto</h2>

<!-- En otro lugar de la página: -->
<a href="#contacto">Ir a Contacto</a>
```

---

## Iframe: `<iframe>`

Un `<iframe>` incrusta otra página web (o un mapa, video, etc.) dentro de tu página:

```html
<iframe
  src="https://www.google.com/maps/embed?..."
  width="600"
  height="450"
  allowfullscreen
></iframe>
```

YouTube, Google Maps y otros servicios ofrecen el código `<iframe>` listo para copiar y pegar. Busca el botón "Compartir → Insertar" en esos servicios.

**Nota:** muchos sitios bloquean ser incrustados en iframes por razones de seguridad.

---

## Listas

### Lista desordenada: `<ul>`

Los elementos aparecen con viñetas (puntos):

```html
<ul>
  <li>Manzanas</li>
  <li>Naranjas</li>
  <li>Plátanos</li>
</ul>
```

Resultado:
- Manzanas
- Naranjas
- Plátanos

### Lista ordenada: `<ol>`

Los elementos aparecen numerados:

```html
<ol>
  <li>Abrir el horno a 180°C</li>
  <li>Preparar la masa</li>
  <li>Hornear por 30 minutos</li>
</ol>
```

Resultado:
1. Abrir el horno a 180°C
2. Preparar la masa
3. Hornear por 30 minutos

### Listas anidadas

Puedes poner una lista dentro de un `<li>`:

```html
<ul>
  <li>Frutas
    <ul>
      <li>Manzana</li>
      <li>Pera</li>
    </ul>
  </li>
  <li>Verduras</li>
</ul>
```

---

## Texto con énfasis

```html
<strong>Texto en negritas (importante)</strong>
<em>Texto en cursiva (énfasis)</em>
```

Usa `<strong>` y `<em>` en lugar de `<b>` e `<i>`, porque los primeros tienen significado semántico (importante para lectores de pantalla).

---

## Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi recetario</title>
  </head>
  <body>
    <h1>Recetas favoritas</h1>

    <h2>Pastel de chocolate</h2>
    <img src="imagenes/pastel.jpg" alt="Pastel de chocolate" width="400" />
    <p>Un clásico delicioso. Aprende a prepararlo en pocos pasos.</p>

    <h3>Ingredientes</h3>
    <ul>
      <li>200g de chocolate</li>
      <li>3 huevos</li>
      <li>150g de harina</li>
    </ul>

    <h3>Pasos</h3>
    <ol>
      <li>Derrite el chocolate a baño María.</li>
      <li>Mezcla con los huevos y la harina.</li>
      <li>Hornea a 180°C por 35 minutos.</li>
    </ol>

    <p>
      ¿Quieres más recetas?
      <a href="https://ejemplo.com/recetas" target="_blank">Visita este sitio</a>
    </p>
  </body>
</html>
```

---

[← Sintaxis HTML](04-sintaxis-html.md) | [Siguiente: Etiquetas semánticas →](06-etiquetas-semanticas.md)
