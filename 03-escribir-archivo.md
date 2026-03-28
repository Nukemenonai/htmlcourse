# 03 — Escribir y guardar tu primer archivo

[← Configurar proyecto](02-configurar-proyecto.md) | [Siguiente: Sintaxis HTML →](04-sintaxis-html.md)

---

## Tu primer archivo HTML

Abre el archivo `index.html` que creaste en la lección anterior. Estará vacío. Escribe lo siguiente exactamente:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Mi primera página</title>
  </head>
  <body>
    <h1>¡Hola, mundo!</h1>
    <p>Esta es mi primera página web.</p>
  </body>
</html>
```

Guarda con `Ctrl + S` y ábrelo con Live Server. Deberías ver el título y el párrafo en el navegador.

---

## El truco del autocompletado: Emmet

VS Code incluye una herramienta llamada **Emmet** que te genera código HTML automáticamente.

Prueba esto:
1. Abre un archivo `.html` vacío.
2. Escribe solo un signo de exclamación: `!`
3. Presiona `Tab` o `Enter`.

VS Code generará automáticamente la estructura base completa:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body></body>
</html>
```

Solo tendrás que cambiar `lang="en"` por `lang="es"` y editar el `<title>`.

---

## ¿Qué significan esas primeras líneas?

| Línea | Qué hace |
|-------|----------|
| `<!DOCTYPE html>` | Le dice al navegador que este es un documento HTML5 moderno |
| `<html lang="es">` | Inicio del documento; `lang="es"` indica que el idioma es español |
| `<head>` | Sección de configuración; el navegador la lee pero no la muestra en pantalla |
| `<meta charset="UTF-8">` | Permite mostrar tildes, eñes y otros caracteres especiales |
| `<meta name="viewport"…>` | Hace que la página se vea bien en teléfonos móviles |
| `<title>` | El texto que aparece en la pestaña del navegador |
| `<body>` | Todo lo que escribas aquí será visible en la página |

No es necesario memorizar esto ahora. Con el tiempo lo escribirás de memoria porque lo usarás en cada proyecto.

---

## Guardar siempre antes de ver cambios

Un error muy común es editar el código y olvidarse de guardar. El navegador siempre muestra la última versión **guardada** del archivo, no lo que está escrito en el editor.

**Atajo:** `Ctrl + S` guarda el archivo activo.

Puedes activar el guardado automático en VS Code: **File → Auto Save**. Esto guarda el archivo cada vez que dejas de escribir por un momento.

---

## Errores comunes al empezar

| Error | Cómo evitarlo |
|-------|---------------|
| La página no muestra tildes | Asegúrate de tener `<meta charset="UTF-8">` en el `<head>` |
| El navegador no actualiza | Verifica que guardaste el archivo (`Ctrl + S`) |
| La página aparece en blanco | Abre las herramientas de desarrollador (`F12`) y revisa la pestaña Console |
| VS Code no colorea el código | Asegúrate de que el archivo se guardó con extensión `.html` o `.css` |

---

[← Configurar proyecto](02-configurar-proyecto.md) | [Siguiente: Sintaxis HTML →](04-sintaxis-html.md)
