# 📘 Guía completa para usar Obsidian con repositorios Markdown

Esta guía explica:

✅ Cómo instalar Obsidian en Windows, macOS y Linux
✅ Cómo descargar un repositorio con archivos .md
✅ Cómo crear un Vault en Obsidian
✅ Cómo cargar las notas descargadas

📥 1. Instalar Obsidian

Obsidian es una aplicación gratuita para trabajar con notas en formato Markdown (.md).

🌐 Sitio oficial:
👉 https://obsidian.md

Descarga según tu sistema operativo.

🪟 Windows

Descarga el instalador .exe

Ejecuta el archivo

Sigue los pasos del instalador

Abre Obsidian

🍎 macOS

Descarga el archivo .dmg

Ábrelo

Arrastra Obsidian a la carpeta Applications

Ejecuta Obsidian

🐧 Linux
Opción sencilla (AppImage):

Descarga el archivo .AppImage

En terminal:

chmod +x Obsidian.AppImage
./Obsidian.AppImage

O con Snap:
sudo snap install obsidian --classic


ℹ️ Obsidian trabaja directamente con archivos .md, no usa bases de datos ocultas.

📂 2. Descargar un repositorio con archivos Markdown
✅ Opción recomendada: usando Git

En tu terminal:

git clone https://github.com/USUARIO/NOMBRE-REPOSITORIO.git


Ejemplo:

git clone https://github.com/bryan-velasco/SIGAFI-APP.git


Esto creará una carpeta con todos los archivos del proyecto.

📦 Opción alternativa: descargar ZIP

En GitHub haz clic en Code → Download ZIP

Extrae el archivo comprimido

Obtendrás una carpeta con los .md

⚠️ Es mejor usar git clone si piensas actualizar el proyecto después.

📁 3. Crear un Vault en Obsidian

Un Vault es simplemente una carpeta donde Obsidian gestiona tus notas.

Pasos:

Abre Obsidian

En la pantalla inicial selecciona:

👉 Open folder as vault

Busca la carpeta descargada del repositorio

Selecciónala

Clic en Open

🎉 ¡Listo! Esa carpeta ahora es tu Vault

📌 Obsidian leerá automáticamente todos los archivos .md dentro.

🔄 4. Cargar una carpeta existente (si ya tienes Obsidian abierto)

Si ya estás dentro de Obsidian:

Ve a:

⚙️ Settings → Vault → Manage vaults

Selecciona:

➕ Open folder as vault

Elige la carpeta del repositorio

🧠 5. Estructura típica de un Vault

Dentro del Vault puedes tener:

📁 Proyecto/
 ├─ README.md
 ├─ Ingeniería de Software.md
 ├─ Requerimientos.md
 ├─ Diseño.md
 ├─ Pruebas.md
 └─ Imágenes/


Obsidian mostrará todo en el panel izquierdo 📂

🔗 6. Cómo funcionan los enlaces entre notas

Dentro de cualquier archivo .md puedes usar:

[[Nombre de la nota]]


Ejemplo:

La [[Modularidad]] es clave para el diseño.


👉 Al dar clic se abre esa nota (o se crea si no existe).

🏷️ 7. Uso de etiquetas (tags)
#ingenieria_software #diseño #calidad


Sirven para clasificar notas y buscarlas fácilmente.

📊 8. Vista de grafo (opcional pero poderosa)

En Obsidian:

🧭 Botón Graph View

Muestra:

🔵 Cada nota como nodo
🔗 Cada enlace como conexión

Ideal para proyectos grandes de ingeniería.

💡 Recomendaciones finales

✅ Usa enlaces [[ ]] para conectar conceptos
✅ Usa carpetas para organizar módulos
✅ Usa tags para temas generales
✅ Usa checkboxes para seguimiento de tareas

🚀 Flujo típico de trabajo
1. Clonar repositorio
2. Abrir carpeta como Vault
3. Editar archivos .md
4. Conectar notas con [[enlaces]]
5. Guardar y subir cambios a GitHub


Si quieres, el siguiente paso puede ser:
