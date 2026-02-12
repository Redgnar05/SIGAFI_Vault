# 📅 Día 1 – 30 de junio de 2025

> [!abstract]  
> **Fecha:** 30 de junio de 2025  
> **Responsable:** Luis Manuel  
> **Objetivo:** Preparación del entorno de desarrollo

---

## 🖥️ 1. Instalación del Sistema Operativo

Se realizó la instalación del sistema operativo **[Ubuntu](../../Ingeniería%20de%20Software/Apoyo_Teorico/Linux.md#-qué-es-ubuntu) 24.04.2 LTS** en el equipo asignado.

> [!important]  
> Se eligió esta versión por ser:
> 
> - 🛡️ Estable
>     
> - 🔒 Segura
>     
> - 🔄 Actualizada (versión LTS – soporte prolongado)
>     

🔗 Enlace de descarga oficial:  
[https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)

---

### 🔐 Credenciales de acceso

> [!warning]  
> Las credenciales deben mantenerse confidenciales.

**Nota:** El carácter `#` se obtiene con `Alt Gr + 3` en teclado _Spanish Windows_.

- 👤 Usuario: *********
    
- 🔑 Contraseña: *********
    

---

## 💻 2. Instalación de Visual Studio Code

Se instaló el editor de código **Visual Studio Code** para el desarrollo y administración del proyecto.

> [!info]  
> VS Code permite:
> 
> - Soporte para múltiples lenguajes
>     
> - Integración con Git
>     
> - Extensiones para desarrollo web y backend
>     

🔗 Enlace de descarga oficial:  
[https://code.visualstudio.com/](https://code.visualstudio.com/)

---

## 🌐 3. Instalación de XAMPP

Se descargó **XAMPP versión 8.2.12** desde el sitio oficial:

🔗 [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)

---

### ⚙️ Permisos de ejecución

Se otorgaron permisos al archivo descargado mediante:

```Bash
sudo chmod 755 xampp
```

> [!note]  
> El comando `chmod 755` permite:
> 
> - Propietario → lectura, escritura y ejecución
>     
> - Grupo y otros → lectura y ejecución
>     

Posteriormente, se ejecutó el instalador desde la terminal con privilegios de administrador.

---

## 🔧 4. Instalación de GIT

Se instaló el sistema de control de versiones **Git** mediante el siguiente comando:

```Bash
sudo apt-get install git
```

> [!tip]  
> Git es fundamental para:
> 
> - Control de versiones
>     
> - Trabajo colaborativo
>     
> - Respaldo del código
>     
> - Integración con GitHub/GitLab
>     

---

## 📌 Resumen del Día 1

> [!success]  
> ✔️ Sistema operativo instalado  
> ✔️ Editor de código configurado  
> ✔️ Servidor local (XAMPP) instalado  
> ✔️ Control de versiones habilitado

El entorno base de desarrollo quedó completamente configurado y listo para comenzar el proyecto.


