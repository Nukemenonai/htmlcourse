# 01 — Usar un editor de código (IDE)

[← Índice](README.md) | [Siguiente: Configurar proyecto →](02-configurar-proyecto.md)

---

## ¿Qué es un IDE?

Un **IDE** (Integrated Development Environment, o Entorno de Desarrollo Integrado) es un programa que usas para escribir código. Es como un procesador de texto (Word, por ejemplo), pero diseñado específicamente para programar.

Un IDE te ayuda con:

- **Coloreado de sintaxis** — pinta las palabras del código de diferentes colores para que sea más fácil leerlo.
- **Autocompletado** — sugiere palabras mientras escribes para ir más rápido.
- **Detección de errores** — muestra líneas o advertencias cuando algo está mal escrito.
- **Organización de archivos** — puedes ver todos los archivos de tu proyecto en un panel lateral.

---

## ¿Qué IDE usaremos?

Para este curso usaremos **Visual Studio Code** (también llamado VS Code). Es gratuito, muy popular y funciona en Windows, Mac y Linux.

### Cómo instalarlo

1. Ve a [https://code.visualstudio.com](https://code.visualstudio.com)
2. Haz clic en el botón azul de descarga. Detectará automáticamente tu sistema operativo.
3. Abre el instalador descargado y sigue los pasos (puedes dejar todas las opciones por defecto).
4. Al terminar, abre VS Code desde el menú de inicio.

---

## Conociendo la interfaz de VS Code

Cuando abres VS Code por primera vez verás estas áreas principales:

```
┌─────────────────────────────────────────────┐
│  Barra de menús (File, Edit, View…)          │
├───────┬─────────────────────────────────────┤
│       │                                     │
│ Panel │        Editor (aquí escribes)        │
│lateral│                                     │
│       │                                     │
├───────┴─────────────────────────────────────┤
│  Terminal integrada (Ctrl + `)               │
└─────────────────────────────────────────────┘
```

- **Panel lateral izquierdo** — muestra los archivos de tu proyecto (ícono de carpeta).
- **Editor central** — donde escribes tu código.
- **Terminal integrada** — una consola de comandos. La abriremos más adelante.

---

## Extensiones recomendadas

Las extensiones son complementos que agregan funciones extra a VS Code. Para este curso instala:

### Prettier — Code formatter
Formatea tu código automáticamente para que se vea ordenado.

1. Haz clic en el ícono de extensiones en el panel lateral (parece cuatro cuadrados).
2. Busca `Prettier - Code formatter`.
3. Haz clic en **Install**.

### Live Server
Lanza un servidor local para ver tus páginas web en el navegador y que se actualicen automáticamente al guardar.

1. Busca `Live Server` (autor: Ritwick Dey).
2. Haz clic en **Install**.

Una vez instalado, verás el botón **Go Live** en la barra inferior de VS Code.

---

## Atajos de teclado esenciales

| Acción | Windows |
|--------|---------|
| Guardar archivo | `Ctrl + S` |
| Deshacer | `Ctrl + Z` |
| Rehacer | `Ctrl + Y` |
| Copiar línea hacia abajo | `Shift + Alt + ↓` |
| Abrir/cerrar terminal | `` Ctrl + ` `` |
| Buscar en el archivo | `Ctrl + F` |
| Comentar/descomentar línea | `Ctrl + /` |

---

[← Índice](index.md) | [Siguiente: Configurar proyecto →](02-configurar-proyecto.md)
