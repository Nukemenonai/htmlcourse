# 02 — Configurar un proyecto en Windows

[← IDE](01-ide.md) | [Siguiente: Escribir un archivo →](03-escribir-archivo.md)

---

## ¿Qué es un proyecto?

Un **proyecto** es simplemente una carpeta en tu computadora donde viven todos los archivos de tu página web: el HTML, el CSS, las imágenes, etc. Mantener todo junto en una carpeta te permite abrirla en VS Code y trabajar con todos los archivos a la vez.

---

## Paso 1 — Crear la carpeta del proyecto

1. Abre el **Explorador de archivos** de Windows (la carpeta amarilla en la barra de tareas).
2. Navega a donde quieras guardar tus proyectos. Un buen lugar es `Documentos`.
3. Haz clic derecho en un espacio vacío y elige **Nuevo → Carpeta**.
4. Ponle un nombre sin espacios ni acentos, por ejemplo: `mi-sitio-web`.

> **Regla importante:** evita espacios y caracteres especiales (ñ, á, é…) en los nombres de carpetas y archivos de tus proyectos. Usa guiones (`-`) en lugar de espacios. Esto evita errores difíciles de detectar.

---

## Paso 2 — Abrir la carpeta en VS Code

Hay dos formas de hacerlo:

**Opción A — Arrastrar la carpeta**
Arrastra la carpeta directamente sobre el ícono de VS Code en el escritorio o en la barra de tareas.

**Opción B — Desde VS Code**
1. Abre VS Code.
2. Ve a **File → Open Folder…** (o presiona `Ctrl + K`, luego `Ctrl + O`).
3. Navega hasta tu carpeta `mi-sitio-web` y haz clic en **Seleccionar carpeta**.

Ahora VS Code muestra tu carpeta en el panel lateral izquierdo bajo **EXPLORER**.

---

## Paso 3 — Estructura básica de archivos

Para una página web sencilla, tu carpeta tendrá esta estructura:

```
mi-sitio-web/
├── index.html        ← página principal
├── style.css         ← estilos
└── imagenes/         ← carpeta para imágenes
    └── foto.jpg
```

- `index.html` es el nombre especial que los navegadores buscan primero cuando abres una carpeta. Siempre nombra tu página principal así.
- `style.css` contendrá todos tus estilos CSS.
- La carpeta `imagenes/` es opcional; la crearemos cuando la necesitemos.

---

## Paso 4 — Crear los archivos desde VS Code

1. En el panel lateral, haz clic en el ícono **New File** (hoja con un `+`) al lado del nombre de tu carpeta.
2. Escribe `index.html` y presiona `Enter`.
3. Repite el proceso para crear `style.css`.

Verás los archivos aparecer inmediatamente en el panel lateral.

---

## Paso 5 — Ver tu página en el navegador con Live Server

Una vez que tengas algo escrito en `index.html`:

1. Haz clic derecho sobre el archivo `index.html` en el panel lateral.
2. Elige **Open with Live Server**.
3. Tu navegador predeterminado abrirá la página automáticamente.

Cada vez que guardes un archivo (`Ctrl + S`), el navegador se actualizará solo.

---

## Resumen del flujo de trabajo

```
Crear carpeta → Abrir en VS Code → Crear index.html → Escribir código → Guardar → Ver en navegador
```

Este flujo lo repetirás en cada proyecto nuevo.

---

[← IDE](01-ide.md) | [Siguiente: Escribir un archivo →](03-escribir-archivo.md)
