
## Índice

[[#Capítulo 1. Introducción]]



----

# Capítulo 1. Introducción

## Objetivo del documento

El presente documento tiene como finalidad describir de manera integral la arquitectura de una aplicación web desarrollada con **PHP** y el framework **CodeIgniter 4**, tomando como base la interpretación de la sesión técnica documentada en la reunión de análisis del proyecto. Su propósito es servir como una guía de referencia para comprender cómo interactúan los distintos componentes que conforman una aplicación web moderna, desde el momento en que un usuario realiza una petición mediante un navegador o un cliente HTTP, hasta que el servidor procesa la solicitud y devuelve una respuesta.

A diferencia de un manual de programación o un tutorial de desarrollo, este documento aborda la arquitectura desde una perspectiva de ingeniería de software, describiendo el papel que desempeña cada tecnología involucrada dentro del ecosistema de una aplicación web. Se analizan conceptos relacionados con infraestructura, protocolos de comunicación, seguridad, arquitectura MVC, funcionamiento interno de CodeIgniter 4, comunicación con bases de datos, construcción de APIs REST y flujo completo de procesamiento de solicitudes HTTP.

Asimismo, este documento busca proporcionar una visión global del sistema antes de profundizar en aspectos específicos de implementación. Comprender la arquitectura completa permite identificar con claridad las responsabilidades de cada componente, facilitando el mantenimiento, la escalabilidad, la integración con otros sistemas y la incorporación de nuevos desarrolladores al proyecto.

> [!info] Propósito principal  
> El objetivo no es únicamente aprender a utilizar CodeIgniter 4, sino comprender cómo todas las tecnologías involucradas colaboran para construir una aplicación web empresarial, desde la infraestructura del servidor hasta la generación de la respuesta enviada al cliente.

---

# Alcance

El contenido desarrollado en este documento cubre el funcionamiento de una arquitectura web basada en el modelo **Cliente–Servidor**, utilizando como tecnologías principales **Apache o NGINX**, **PHP**, **CodeIgniter 4** y un sistema gestor de bases de datos relacional como **MySQL**.

Se estudia el recorrido completo de una petición HTTP, iniciando con la interacción del usuario mediante un navegador web o una herramienta de pruebas como Postman, continuando con el procesamiento realizado por el servidor web y el framework, hasta finalizar con la construcción y envío de la respuesta correspondiente.

Dentro del alcance del documento se incluyen los siguientes temas:

- Arquitectura Cliente–Servidor.
- Funcionamiento de los protocolos HTTP y HTTPS.
- Métodos HTTP (GET, POST, PUT, PATCH y DELETE).
- Infraestructura del servidor web.
- Certificados digitales y protocolo TLS.
- Arquitectura MVC implementada por CodeIgniter 4.
- Flujo interno de procesamiento de solicitudes.
- Enrutamiento mediante _Routing_.
- Controladores, modelos y vistas.
- Comunicación con bases de datos mediante SQL.
- Desarrollo y consumo de APIs REST.
- Seguridad básica en aplicaciones web.
- Herramientas utilizadas durante el desarrollo, como Postman.

El documento no pretende sustituir la documentación oficial de PHP ni de CodeIgniter 4, sino establecer una base conceptual sólida que permita comprender el comportamiento general de la plataforma antes de profundizar en aspectos particulares de programación o configuración avanzada.

> [!note]  Nota
> Aunque algunos ejemplos se encuentran orientados al contexto de una aplicación empresarial similar a **SIGAFI**, los conceptos explicados son aplicables a cualquier aplicación web desarrollada con PHP y CodeIgniter 4.

---

# Público objetivo

Este documento está dirigido principalmente a estudiantes, desarrolladores y miembros de equipos de desarrollo que requieran comprender la arquitectura de una aplicación web desarrollada bajo tecnologías PHP.

En particular, resulta de utilidad para:

- Estudiantes que comienzan a desarrollar aplicaciones web utilizando PHP y CodeIgniter 4.
- Desarrolladores que se integran por primera vez a un proyecto construido bajo esta arquitectura.
- Analistas de sistemas interesados en comprender el flujo de información dentro de una aplicación web.
- Arquitectos de software que requieran documentar o comunicar la estructura general del sistema.
- Integrantes del equipo de mantenimiento encargados de diagnosticar problemas, implementar nuevas funcionalidades o realizar mejoras sobre aplicaciones existentes.

No se asume que el lector posea experiencia previa con CodeIgniter 4; sin embargo, es recomendable contar con conocimientos básicos sobre programación en PHP, bases de datos relacionales y conceptos generales de redes de computadoras para facilitar la comprensión de algunos apartados técnicos.

---

# Tecnologías utilizadas

La arquitectura descrita en este documento se fundamenta en un conjunto de tecnologías ampliamente utilizadas en el desarrollo de aplicaciones web empresariales. Cada una cumple una función específica dentro del ciclo de vida de una petición HTTP y, en conjunto, permiten construir aplicaciones escalables, mantenibles y seguras.

## Cliente Web

El cliente representa el punto de interacción entre el usuario y la aplicación. Generalmente corresponde a un navegador web moderno, aunque también puede tratarse de aplicaciones móviles, clientes de escritorio o herramientas especializadas para pruebas de servicios web.

Entre sus responsabilidades se encuentran:

- Enviar solicitudes HTTP o HTTPS.
- Mostrar el contenido HTML generado por el servidor.
- Ejecutar código JavaScript.
- Administrar cookies y sesiones del usuario.
- Renderizar interfaces gráficas.

---

## HTTP y HTTPS

HTTP constituye el protocolo de comunicación utilizado para el intercambio de información entre clientes y servidores. Su versión segura, HTTPS, incorpora mecanismos de cifrado mediante certificados digitales y el protocolo TLS, garantizando la confidencialidad e integridad de los datos transmitidos.

Dentro de este protocolo se emplean distintos métodos para indicar la operación que debe realizar el servidor, siendo los más comunes GET, POST, PUT, PATCH y DELETE.

---

## Apache HTTP Server / NGINX

Apache y NGINX son servidores web encargados de recibir las solicitudes provenientes de Internet y dirigirlas hacia la aplicación PHP correspondiente.

Entre sus principales funciones destacan:

- Escuchar solicitudes en los puertos 80 y 443.
- Administrar conexiones concurrentes.
- Servir archivos estáticos.
- Redirigir solicitudes al intérprete de PHP.
- Gestionar certificados SSL/TLS.
- Aplicar reglas de seguridad y configuración.

La elección entre Apache y NGINX depende de los requerimientos del proyecto, aunque ambos son ampliamente compatibles con aplicaciones desarrolladas en CodeIgniter 4.

---

## PHP

PHP constituye el lenguaje de programación responsable de implementar la lógica de negocio del sistema. Es un lenguaje interpretado del lado del servidor, diseñado especialmente para el desarrollo de aplicaciones web dinámicas.

Dentro de esta arquitectura, PHP ejecuta el framework CodeIgniter 4, procesa la información recibida del cliente, interactúa con la base de datos y genera la respuesta que será enviada nuevamente al navegador.

---

## CodeIgniter 4

CodeIgniter 4 es un framework MVC desarrollado para facilitar la construcción de aplicaciones web estructuradas, reutilizables y fáciles de mantener.

Entre sus principales características se encuentran:

- Arquitectura Modelo–Vista–Controlador (MVC).
- Sistema de enrutamiento flexible.
- Filtros de seguridad.
- Integración con múltiples motores de bases de datos.
- Soporte para desarrollo de APIs REST.
- Gestión de sesiones.
- Validación de datos.
- Sistema de migraciones y _seeders_.
- Herramientas de línea de comandos mediante Spark.

Su objetivo principal es separar las responsabilidades de cada componente del sistema, favoreciendo una arquitectura limpia y organizada.

---

## Base de Datos MySQL

MySQL actúa como el sistema gestor de bases de datos encargado del almacenamiento persistente de la información de la aplicación.

A través de los modelos de CodeIgniter 4, el sistema ejecuta consultas SQL para:

- Consultar registros.
- Insertar nuevos datos.
- Actualizar información existente.
- Eliminar registros.
- Mantener la integridad de la información.

La comunicación entre la aplicación y la base de datos se realiza mediante los controladores y modelos definidos dentro de la arquitectura MVC.

---

## Postman

Postman es una herramienta utilizada durante las etapas de desarrollo y pruebas para consumir servicios HTTP sin necesidad de utilizar un navegador web.

Permite:

- Enviar solicitudes GET, POST, PUT, PATCH y DELETE.
- Configurar encabezados HTTP.
- Adjuntar cuerpos de petición en formato JSON, XML o formularios.
- Validar respuestas del servidor.
- Probar APIs REST antes de integrarlas con aplicaciones cliente.

Su utilización facilita la depuración de servicios web y la validación del comportamiento de los diferentes endpoints implementados por la aplicación.

> [!tip]  
> A lo largo de este documento se utilizarán ejemplos basados en Postman para ilustrar el funcionamiento de las peticiones HTTP y demostrar el flujo de comunicación entre el cliente y una aplicación desarrollada con CodeIgniter 4.

# Capítulo 2. Arquitectura General del Sistema 


# Capítulo 3. Infraestructura del Servidor 


# Capitulo 4. Protocolo HTTP


# Capítulo 5. Métodos HTTP


# Capítulo 6. Flujo completo de una petición 



# Capítuo 7. Arquitectura MVC



# Capítulo 8. Funcionamiento interno de CodeIgniter 4

### ¿Cómo CodeIgniter organiza el patrón MVC

#### Estructura de carpetas

```

mini-ci-mvc/
│
├── app/ ← Todo el código de TU aplicación vive aquí
│ │
│ ├── Config/
│ │ └── Routes.php ← Mapa de URLs → Controlador::método
│ │
│ ├── Controllers/
│ │ └── Tareas.php ← El "C" de MVC: recibe la petición,
│ │ pide datos al Model, elige la View
│ │
│ ├── Models/
│ │ └── TareaModel.php ← El "M" de MVC: habla con la base de
│ │ datos y devuelve datos "puros"
│ │
│ └── Views/
│ └── tareas/
│ ├── index.php ← El "V" de MVC: HTML + variables,
│ └── detalle.php sin lógica de negocio
│
├── public/
│ └── index.php ← Único punto de entrada público
│ (aquí apunta el servidor web)
│
├── writable/ ← Carpeta con permisos de escritura
│ ├── logs/ (logs, caché, archivos subidos).
│ ├── cache/ Nunca es accesible desde el navegador.
│ └── uploads/
│
└── README.md

```



# Capítulo 9. APIs REST



# Capítulo 10. Seguridad



# Capítulo 11. Bases de Datos



# Capítulo 12. Postman



# Capítulo 13. Caso práctico: Login



# Capítulo 14. Caso práctico: API de pagos 



# Capítulo 15. Diagramas UML



# Capítulo 16. Conlusiones 



