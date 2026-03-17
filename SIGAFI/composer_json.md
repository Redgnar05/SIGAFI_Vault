
# 📑 Índice

- [📌 Identidad del Proyecto](#identidad-del-proyecto)
- [⚙️ Requisitos de versión de PHP](#requisitos-de-versión-de-php)
- [🧩 Framework utilizado](#framework-utilizado)
- [📚 Librerías externas](#librerías-externas)
- [🛠️ Dependencias de desarrollo](#dependencias-de-desarrollo)
- [🔄 Sistema de Autoload](#sistema-de-autoload)
- [📦 Configuración de Composer](#configuración-de-composer)

El archivo `composer.json` es el archivo de configuración central del proyecto PHP que utiliza Composer, el gestor de dependencias estándar. Define qué librerías externas necesita este proyecto.

> [!info]
> **Composer** es el administrador de dependencias estándar para PHP, esencial para gestionar bibliotecas de terceros. Permite declarar, instalar y actualizar automáticamente las librerías necesarias, descargando las dependencias recursivas y facilitando la carga automática de clases (autoloading), similar a npm en Node.js.

---
---
---

# Identidad del Proyecto

```JSON
"name": "codeigniter4/appstarter",
"description": "CodeIgniter4 starter app",
"type": "project"
```

---

### Base Tecnológica del Proyecto

El sistema está construido sobre el [[Framework]] **CodeIgniter 4 (versión 4.5.4)** utilizando la plantilla oficial _App Starter_.  
El proyecto fue inicializado como un tipo `project` en Composer, lo que indica que es una aplicación web completa y no una librería reutilizable.
https://codeigniter.com/

---

### Arquitectura Base del Sistema

El sistema está desarrollado sobre el framework CodeIgniter 4 (versión 4.5.4), el cual implementa el patrón arquitectónico MVC.  
La aplicación fue creada utilizando la plantilla oficial "App Starter", que proporciona la estructura inicial del proyecto, incluyendo configuración base, sistema de rutas y punto de entrada público.

---


```JSON
"require": {
	"php": "^8.1",
	"codeigniter4/framework": "4.5.4",
	"dompdf/dompdf": "^3.1"
}
```

---
---
---

# Requisitos de versión de PHP

La aplicación requiere como mínimo la versión **8.1 de PHP** para su correcto funcionamiento. Esta dependencia está definida en el archivo `composer.json` mediante la siguiente configuración:

```JSON
"php": "^8.1"
```

El operador `^` indica que el sistema es compatible con la versión **8.1 de PHP y versiones posteriores dentro de la misma serie mayor**, siempre que mantengan compatibilidad con dicha versión.

El uso de **PHP 8.1 o superior** permite aprovechar mejoras en el lenguaje, optimizaciones de rendimiento y características modernas que son utilizadas por el framework CodeIgniter 4 sobre el cual está construida la aplicación.

---
---
---

# Framework utilizado

La aplicación está desarrollada utilizando el framework **CodeIgniter 4**, el cual proporciona la estructura base para el desarrollo de aplicaciones web en PHP y sigue el patrón arquitectónico **Modelo-Vista-Controlador (MVC)**.

La dependencia del framework se encuentra definida en el archivo `composer.json` mediante la siguiente configuración:

```JSON
"codeigniter4/framework": "4.5.4"
```

La versión especificada indica que el proyecto utiliza **exactamente la versión 4.5.4 del framework**, lo que significa que no se permite la instalación automática de versiones superiores o inferiores. Esta restricción garantiza la estabilidad del sistema y evita posibles incompatibilidades derivadas de cambios en versiones posteriores del framework.

> [!quote] 
>
> Esta estructura permite organizar el código de la aplicación de forma modular, facilitando su mantenimiento, escalabilidad y desarrollo.

---
---
---

# Librerías externas

### Generación de documentos PDF

La aplicación utiliza la librería **Dompdf**, la cual permite generar archivos **PDF a partir de contenido HTML y CSS**. Esta librería es comúnmente utilizada en aplicaciones web para producir documentos descargables o imprimibles directamente desde el sistema, permitiendo transformar vistas o plantillas HTML del sistema en documentos PDF de manera automatizada en un formato estandarizado

La dependencia se encuentra declarada en el archivo `composer.json` de la siguiente forma:

```JSON
"dompdf/dompdf": "^3.1"
```

El operador `^` indica que la aplicación es compatible con la **versión 3.1 o superior**, siempre que las actualizaciones pertenezcan a la misma versión mayor y mantengan compatibilidad con la interfaz de la librería.

---
---
---

# Dependencias de desarrollo

El proyecto incluye un conjunto de dependencias destinadas exclusivamente al **entorno de desarrollo**, definidas en la sección `require-dev` del archivo `composer.json`. Estas librerías se utilizan para facilitar tareas como **generación de datos de prueba, depuración del código y ejecución de pruebas automatizadas**.

```JSON
"require-dev": {
    "fakerphp/faker": "^1.9",
    "kint-php/kint": "5.0.1",
    "mikey179/vfsstream": "^1.6",
    "phpunit/phpunit": "^10.5.16"
}
```

> [!warning] 
>
> Es importante señalar que estas dependencias **no forman parte del entorno de producción**, ya que su propósito principal es apoyar el desarrollo, la depuración y la validación del sistema durante su construcción y mantenimiento.

---

## Generación de datos de prueba

La aplicación utiliza la librería **Faker**, la cual permite generar **datos ficticios de forma automática** para realizar pruebas o poblar bases de datos durante el desarrollo.

---

## Herramientas de depuración

Para facilitar la inspección y análisis del comportamiento del código durante el desarrollo, el proyecto incluye la librería **Kint**.

El uso de herramientas de depuración como Kint contribuye a identificar errores, comprender el flujo de ejecución del programa y acelerar el proceso de desarrollo.

---

## Pruebas automatizadas

El proyecto también incluye el framework de pruebas **PHPUnit**, el cual permite implementar **pruebas automatizadas** para verificar el correcto funcionamiento de los componentes del sistema.

Las pruebas pueden ejecutarse mediante el siguiente script definido en el archivo `composer.json`:

```JSON
"scripts": {  
    "test": "phpunit"  
}
```

Esto permite ejecutar la suite de pruebas del proyecto utilizando el siguiente comando:

```Bash
composer test
```

---
---
---

# Sistema de Autoload

La aplicación utiliza el mecanismo de **autoloading** definido por el estándar **PSR-4**, el cual permite cargar automáticamente las clases del proyecto sin necesidad de incluir manualmente archivos mediante instrucciones como `require` o `include`.

La configuración del autoload se encuentra definida en el archivo `composer.json` de la siguiente forma:

```JSON
"autoload": {  
    "psr-4": {  
        "App\\": "app/",  
        "Config\\": "app/Config/"  
    }  
}
```

De acuerdo con esta configuración, el proyecto establece un mapeo entre **namespaces** y directorios dentro de la estructura del sistema:

- El **namespace `App`** se encuentra asociado al directorio `app/`, donde se ubica la mayor parte del código de la aplicación, incluyendo controladores, modelos, librerías y otros componentes propios del sistema.
    
- El **namespace `Config`** se encuentra asociado al directorio `app/Config/`, el cual contiene los archivos de configuración utilizados por la aplicación, tales como configuraciones del sistema, rutas, base de datos y otros parámetros necesarios para su funcionamiento.

---
---
---

# Configuración de Composer

El archivo `composer.json` incluye la sección de configuración que define el comportamiento del gestor de dependencias **Composer** durante la instalación y administración de los paquetes utilizados por el proyecto.

```JSON
"config": {  
    "optimize-autoloader": true,  
    "preferred-install": "dist",  
    "sort-packages": true  
}
```

### Optimización del autoload

La opción:
```JSON
"optimize-autoloader": true
```

- Composer debe **optimizar el sistema de autoload de clases** durante la instalación de las dependencias. 
	- Genera un mapa de clases más eficiente que permite cargar archivos de forma más rápida. 
		
	- Mejora el rendimiento de la aplicación, particularmente en entornos de producción.

### Método de instalación de paquetes

La configuración:
```JSON
"preferred-install": "dist"
```

Establece que los paquetes se instalen preferentemente a partir de **distribuciones empaquetadas (dist)** en lugar de clonar directamente los repositorios de código fuente. Esto reduce el tiempo de instalación y el tamaño de las dependencias descargadas.

### Organización automática de dependencias

La opción:
```JSON
"sort-packages": true
```

Composer debe **ordenar automáticamente las dependencias dentro del archivo `composer.json`**, lo que facilita la lectura y mantenimiento del archivo de configuración.

En conjunto, estas opciones reflejan **buenas prácticas en la gestión de dependencias**, ya que contribuyen a mejorar el rendimiento del sistema, mantener un archivo de configuración organizado y optimizar el proceso de instalación de paquetes dentro del proyecto.





