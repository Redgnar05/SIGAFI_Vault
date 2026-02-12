# 🐧 ¿Qué es Ubuntu?

> [!abstract]  
> ** #Ubuntu** es una distribución de Linux basada en Debian, ampliamente utilizada en entornos de desarrollo y servidores.

Se usa comúnmente en:

- 🌐 Servidores web
    
- 💻 Desarrollo de software
    
- 🏢 Infraestructura empresarial
    

---

## 🔹 ¿Por qué usar Ubuntu en servidores?

- 🛡️ Versiones LTS (soporte a largo plazo)
    
- 🔐 Soporte de seguridad extendido
    
- 🔄 Gran compatibilidad con Apache, MySQL, PHP
    
- 📦 Gestión eficiente de paquetes mediante APT
    

> [!tip]  
> Ubuntu Server es una de las opciones más utilizadas en producción debido a su estabilidad.

---

# 📦 ¿Qué es APT?

> [!abstract]  
> **APT (Advanced Package Tool)** es el gestor de paquetes de Ubuntu.

Permite:

- Instalar software
    
- Actualizar paquetes
    
- Eliminar programas
    

Ejemplo:

`sudo apt-get install git`

Significado del comando:

- `sudo` → ejecutar como administrador
    
- `apt-get` → gestor de paquetes
    
- `install` → instalar
    
- `git` → paquete a instalar
    

> [!info]  
> APT automatiza la instalación y gestión de dependencias en el sistema.

---

# 🔐 ¿Qué hace el comando `chmod 755`?

En Linux, cada archivo tiene permisos numéricos basados en:

- 4 → lectura (r)
    
- 2 → escritura (w)
    
- 1 → ejecución (x)
    

Por lo tanto:

- `7` = 4 + 2 + 1 → lectura, escritura y ejecución
    
- `5` = 4 + 1 → lectura y ejecución
    

Ejemplo:

`sudo chmod 755 xampp`

Significa:

- 👤 Propietario → puede leer, escribir y ejecutar
    
- 👥 Grupo → puede leer y ejecutar
    
- 🌍 Otros → pueden leer y ejecutar
    

> [!warning]  
> Dar permisos incorrectos puede comprometer la seguridad del sistema.


---

## 📚 Conocimientos necesarios

- Instalación de sistemas operativos
    
- Particionado básico de disco
    
- Conceptos de usuario y contraseña
    
- Uso básico de terminal    