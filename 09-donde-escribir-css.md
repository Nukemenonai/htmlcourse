# 09 — ¿Dónde escribir CSS?

[← Sintaxis CSS](08-sintaxis-css.md) | [Siguiente: Especificidad →](10-especificidad.md)

---

## Tres formas de añadir CSS a una página

Hay tres lugares donde puedes escribir CSS, cada uno con sus ventajas y desventajas:

---

## 1. CSS en línea (inline)

Se escribe directamente en el atributo `style` de una etiqueta HTML:

```html
<p style="color: red; font-size: 20px;">Este párrafo es rojo y grande.</p>
```

**Ventajas:**
- Se aplica inmediatamente a ese elemento.
- Útil para pruebas rápidas.

**Desventajas:**
- No es reutilizable: si quieres el mismo estilo en 10 párrafos, lo repites 10 veces.
- Mezcla la estructura (HTML) con la presentación (CSS).
- Tiene la prioridad más alta en especificidad, lo que puede causar problemas (ver lección 10).

**Conclusión:** evita el CSS en línea excepto para pruebas o ajustes muy puntuales.

---

## 2. CSS interno (embedded)

Se escribe dentro del `<head>` del HTML, usando la etiqueta `<style>`:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi página</title>
    <style>
      body {
        font-family: sans-serif;
        background-color: #f0f0f0;
      }
      h1 {
        color: darkblue;
      }
    </style>
  </head>
  <body>
    <h1>Título</h1>
    <p>Texto</p>
  </body>
</html>
```

**Ventajas:**
- Todo en un solo archivo.
- Los estilos aplican a toda la página (reutilizable dentro del documento).

**Desventajas:**
- No es reutilizable entre distintas páginas HTML.
- Mezcla HTML y CSS en el mismo archivo.

**Conclusión:** útil para páginas únicas o para aprender. Para proyectos reales, usa CSS externo.

---

## 3. CSS externo (recomendado)

Se escribe en un archivo `.css` separado y se enlaza al HTML con la etiqueta `<link>` dentro del `<head>`:

**Archivo `style.css`:**
```css
body {
  font-family: sans-serif;
  background-color: #f0f0f0;
}

h1 {
  color: darkblue;
}

p {
  line-height: 1.6;
}
```

**Archivo `index.html`:**
```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Mi página</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <h1>Título</h1>
    <p>Texto</p>
  </body>
</html>
```

El atributo `href` apunta al archivo CSS. Si está en una subcarpeta:
```html
<link rel="stylesheet" href="css/style.css" />
```

**Ventajas:**
- El mismo archivo CSS puede ser usado por múltiples páginas.
- HTML y CSS están separados — más fácil de mantener.
- El navegador guarda el CSS en caché, lo que hace el sitio más rápido.

**Conclusión:** siempre usa CSS externo en proyectos reales.

---

## Resumen comparativo

| Método | Dónde se escribe | Reutilizable | Recomendado para |
|--------|-----------------|--------------|-----------------|
| Inline | Atributo `style` del HTML | No | Pruebas rápidas |
| Interno | Etiqueta `<style>` en `<head>` | Solo en esa página | Ejemplos pequeños |
| Externo | Archivo `.css` separado | Sí, en todo el sitio | Proyectos reales |

---

## El orden importa: múltiples hojas de estilo

Puedes enlazar más de un archivo CSS:

```html
<link rel="stylesheet" href="reset.css" />
<link rel="stylesheet" href="style.css" />
```

Si dos reglas en distintos archivos afectan al mismo elemento, **gana la que aparece después** (siempre que tengan la misma especificidad). Aprenderemos más sobre esto en la siguiente lección.

---

[← Sintaxis CSS](08-sintaxis-css.md) | [Siguiente: Especificidad →](10-especificidad.md)
