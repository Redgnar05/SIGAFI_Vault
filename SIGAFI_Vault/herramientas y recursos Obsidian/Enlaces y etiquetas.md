# 🔗 Enlaces y etiquetas en Obsidian (guía práctica)

---

> [!info] Enlaces entre notas (`[[ ]]`)  
> Son la base de Obsidian.  
> Permiten conectar conceptos, temas o archivos completos y crear una red de conocimiento.

---

## ✨ Sintaxis básica

`[[Nombre de la nota]]`

---

## 📄 Ejemplo práctico

Si tienes un archivo llamado:

`Modularidad.md`

En otra nota escribes:

`La [[Modularidad]] es un principio fundamental del diseño de software.`

👉 Al dar clic:

- Te lleva al archivo enlazado
    
- Si no existe, Obsidian lo crea automáticamente
    

---

> [!tip] Texto visible diferente al nombre del archivo  
> Útil cuando quieres que el enlace se vea más natural dentro del párrafo.

`[[Modularidad|principio de modularidad]]`

Se muestra así:

[[Modularidad|principio de modularidad]]

---

> [!note] Enlazar a una sección específica

`[[Ingeniería de Software#Modularidad]]`

👉 Te lleva directamente a ese subtítulo dentro del archivo.

---

---

# 🏷️ Etiquetas (tags con `#`)

> [!abstract] ¿Para qué sirven?  
> Las etiquetas permiten clasificar y agrupar notas por temas generales.

---

## ✨ Sintaxis

`#ingenieria_software #swebok #requerimientos #diseño #calidad`

---

## 📌 Ejemplo en contexto

`Este tema pertenece a #ingenieria_software y #diseño.`

👉 Luego puedes buscar una etiqueta y ver TODAS las notas relacionadas.

---

---

# 🧠 Diferencia clave entre enlaces y etiquetas

|Método|Uso principal|Ejemplo|
|---|---|---|
|`[[ ]]`|Conectar notas o conceptos específicos|[[Modularidad]]|
|`#tag`|Clasificar por áreas generales|#diseño|

> [!important] Recomendación  
> Usa enlaces para ideas importantes y etiquetas para organizar por temas.

---

---

# 🚀 Ejemplo PRO (para proyectos como SIGAFI)

`# 📘 Modularidad  #diseño #arquitectura  La [[Modularidad]] permite dividir sistemas complejos en partes manejables.  Se relaciona con:  - [[Calidad del software]] - [[Diseño de software]] - [[Mantenibilidad]]`

---

---

# 📊 Bonus: Grafo de conocimiento

> [!success] Visualización poderosa  
> Obsidian genera automáticamente un mapa de relaciones.

### Para verlo:

🧭 Abre **Graph View**

Verás:

🔵 Cada nota como un nodo  
🔗 Cada `[[enlace]]` como conexión

👉 Ideal para estudiar y entender proyectos grandes.
