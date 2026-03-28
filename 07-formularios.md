# 07 — Formularios

[← Etiquetas semánticas](06-etiquetas-semanticas.md) | [Siguiente: Sintaxis CSS →](08-sintaxis-css.md)

---

## ¿Qué es un formulario?

Un formulario es la forma en que una página web recibe información del usuario: iniciar sesión, registrarse, buscar algo, enviar un mensaje. Cada campo de texto, botón o casilla que llenas en internet es parte de un formulario HTML.

---

## La etiqueta `<form>`

Todo formulario empieza con `<form>`. Los campos van dentro:

```html
<form action="/enviar" method="post">
  <!-- campos aquí -->
</form>
```

| Atributo | Función |
|----------|---------|
| `action` | URL a donde se envían los datos (lo maneja el servidor) |
| `method` | Cómo se envían: `get` (datos en la URL) o `post` (datos ocultos) |

Por ahora no necesitas preocuparte por `action` y `method` — los usarás cuando aprendas un lenguaje de servidor. Por el momento puedes omitirlos.

---

## La etiqueta `<label>`

El `<label>` describe qué debe escribir el usuario en un campo. Siempre asocia cada label con su campo usando el atributo `for` que apunte al `id` del campo:

```html
<label for="nombre">Nombre:</label>
<input type="text" id="nombre" name="nombre" />
```

Cuando el usuario hace clic en el label, el campo recibe el foco automáticamente. Esto también ayuda a los lectores de pantalla.

---

## Input de texto: `type="text"`

El campo de texto de una sola línea es el más común:

```html
<label for="correo">Correo electrónico:</label>
<input type="text" id="correo" name="correo" placeholder="ejemplo@correo.com" />
```

| Atributo | Función |
|----------|---------|
| `type` | Tipo de campo |
| `id` | Identificador único (para conectarlo al label) |
| `name` | Nombre del dato al enviar el formulario |
| `placeholder` | Texto gris de ayuda que desaparece al escribir |
| `required` | El campo es obligatorio (el formulario no se envía si está vacío) |

### Otros tipos de input útiles

```html
<input type="email" />     <!-- valida que sea un correo -->
<input type="password" />  <!-- oculta lo que se escribe -->
<input type="number" />    <!-- solo acepta números -->
<input type="date" />      <!-- muestra un selector de fecha -->
```

---

## Botones de opción: `type="radio"`

Los radio buttons permiten elegir **una sola opción** de un grupo. Todos los del mismo grupo deben tener el mismo `name`:

```html
<p>¿Cuál es tu nivel de experiencia?</p>

<input type="radio" id="principiante" name="nivel" value="principiante" />
<label for="principiante">Principiante</label>

<input type="radio" id="intermedio" name="nivel" value="intermedio" />
<label for="intermedio">Intermedio</label>

<input type="radio" id="avanzado" name="nivel" value="avanzado" />
<label for="avanzado">Avanzado</label>
```

- `name` igual en todos → forman un grupo (solo uno puede estar seleccionado).
- `value` es el dato que se envía al servidor cuando se elige esa opción.

---

## Casillas de verificación: `type="checkbox"`

Los checkboxes permiten elegir **varias opciones** al mismo tiempo:

```html
<p>¿Qué tecnologías te interesan?</p>

<input type="checkbox" id="html" name="tecnologias" value="html" />
<label for="html">HTML</label>

<input type="checkbox" id="css" name="tecnologias" value="css" />
<label for="css">CSS</label>

<input type="checkbox" id="js" name="tecnologias" value="js" />
<label for="js">JavaScript</label>
```

Agrega el atributo `checked` para que una casilla empiece marcada:

```html
<input type="checkbox" id="html" name="tecnologias" value="html" checked />
```

---

## Botón de envío: `type="submit"`

El botón que envía el formulario:

```html
<button type="submit">Enviar formulario</button>
```

O usando `<input>`:

```html
<input type="submit" value="Enviar" />
```

La diferencia: `<button>` puede contener HTML dentro (como un ícono); `<input type="submit">` solo texto.

---

## Área de texto: `<textarea>`

Para texto de varias líneas (como un mensaje o comentario):

```html
<label for="mensaje">Mensaje:</label>
<textarea id="mensaje" name="mensaje" rows="5" cols="40" placeholder="Escribe aquí…"></textarea>
```

---

## Ejemplo completo

```html
<form>
  <h2>Formulario de contacto</h2>

  <label for="nombre">Nombre completo:</label>
  <input type="text" id="nombre" name="nombre" placeholder="Ana García" required />

  <label for="email">Correo electrónico:</label>
  <input type="email" id="email" name="email" placeholder="ana@ejemplo.com" required />

  <p>¿Cómo nos encontraste?</p>
  <input type="radio" id="buscador" name="origen" value="buscador" />
  <label for="buscador">Buscador</label>

  <input type="radio" id="recomendacion" name="origen" value="recomendacion" />
  <label for="recomendacion">Recomendación</label>

  <input type="radio" id="redes" name="origen" value="redes" />
  <label for="redes">Redes sociales</label>

  <p>¿Qué temas te interesan?</p>
  <input type="checkbox" id="diseno" name="temas" value="diseno" />
  <label for="diseno">Diseño</label>

  <input type="checkbox" id="desarrollo" name="temas" value="desarrollo" />
  <label for="desarrollo">Desarrollo</label>

  <label for="mensaje">Mensaje:</label>
  <textarea id="mensaje" name="mensaje" rows="4" placeholder="Escribe tu mensaje…"></textarea>

  <button type="submit">Enviar</button>
</form>
```

---

[← Etiquetas semánticas](06-etiquetas-semanticas.md) | [Siguiente: Sintaxis CSS →](08-sintaxis-css.md)
