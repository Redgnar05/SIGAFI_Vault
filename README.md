# 📘 Guía completa para usar Obsidian con repositorios Markdown

Esta guía explica:

- ✅ Cómo instalar Obsidian en Windows, macOS y Linux

- ✅ Cómo descargar un repositorio con archivos .md

- ✅ Cómo crear un Vault en Obsidian

- ✅ Cómo cargar las notas descargadas

---

📥 1. Instalar Obsidian

Obsidian es una aplicación gratuita para trabajar con notas en formato Markdown (.md).

🌐 Sitio oficial: https://obsidian.md

<img width="853" height="573" alt="Image" src="https://github.com/user-attachments/assets/84d28a51-fa9c-45fd-9b5c-1ea738c4a948" />

Descarga la versión correspondiente a tu sistema operativo.

<img width="412" height="487" alt="Image" src="https://github.com/user-attachments/assets/27002220-9f32-449f-b477-c8e4471421bc" />

---

## 🪟 Windows

1. Descarga el instalador .exe

2. Ejecuta el archivo

3. Sigue los pasos del instalador

4. Abre Obsidian

---

## 🍎 macOS

1. Descarga el archivo .dmg

2. Ábrelo

3. Arrastra Obsidian a la carpeta Applications

4. Ejecuta Obsidian

---

## 🐧 Linux

**Opción 1: AppImage**

1. Descarga el archivo .AppImage

2. En la terminal ejecuta:

```bash
chmod +x Obsidian.AppImage
./Obsidian.AppImage
```

**Opción 2: Snap**

```bash
sudo snap install obsidian --classic
```

---

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

Un Vault es una carpeta donde Obsidian gestiona tus notas.

Pasos:

Abre Obsidian

En la pantalla inicial selecciona:

👉 Open folder as vault

Busca la carpeta descargada del repositorio

Selecciónala

Haz clic en Open

🎉 ¡Listo! Esa carpeta ahora es tu Vault.

📌 Obsidian leerá automáticamente todos los archivos .md dentro.

🔄 4. Cargar una carpeta existente (si ya usas Obsidian)

Ve a:

⚙️ Settings → Vault → Manage vaults

Selecciona:

➕ Open folder as vault

Elige la carpeta del repositorio

🧠 5. Estructura típica de un Vault

Ejemplo:

📁 Proyecto/
 ├─ README.md
 ├─ Ingeniería de Software.md
 ├─ Requerimientos.md
 ├─ Diseño.md
 ├─ Pruebas.md
 └─ Imágenes/


Obsidian mostrará todo en el panel izquierdo 📂

🔗 6. Enlaces entre notas

Dentro de cualquier archivo .md:

[[Nombre de la nota]]


Ejemplo:

La [[Modularidad]] es clave para el diseño.


👉 Al dar clic se abre esa nota o se crea automáticamente.

🏷️ 7. Etiquetas (tags)

Ejemplo:

#ingenieria_software #diseño #calidad


Sirven para clasificar notas por temas.

📊 8. Vista de grafo

En Obsidian:

🧭 Botón Graph View

Muestra:

🔵 Cada nota como nodo

🔗 Cada enlace como conexión

Ideal para proyectos grandes.

💡 Recomendaciones finales

✅ Usa enlaces [[ ]] para conectar conceptos

✅ Usa carpetas para organizar módulos

✅ Usa etiquetas para temas generales

✅ Usa checkboxes para seguimiento

🚀 Flujo típico de trabajo

Clonar repositorio

Abrir carpeta como Vault

Editar archivos .md

Conectar notas con [[enlaces]]

Subir cambios a GitHub
