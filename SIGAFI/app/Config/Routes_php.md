# Archivo de Rutas (`Routes.php`)

## Descripción general

El archivo **`Routes.php`** define el **sistema de enrutamiento de la aplicación**, es decir, la forma en que las solicitudes HTTP entrantes son dirigidas hacia los **controladores y métodos correspondientes** dentro del sistema.

En el framework **[[CodeIgniter]]**, las rutas permiten asociar una **URL específica** con un **método de un controlador**, facilitando la organización de la aplicación y la separación de responsabilidades dentro de la arquitectura **[[MVC]] (Model–View–Controller)**.

Las rutas se registran utilizando el objeto:

```PHP
RouteCollection $routes
```

El cual pertenece al sistema de enrutamiento del framework.

---

El archivo de rutas define un conjunto amplio y estructurado de **URLs** que cubren prácticamente todas las funcionalidades del sistema, organizadas por módulos como autenticación (`/Ingresar`), notificaciones (`/GetNotificationsAjax`), gestión de usuarios (`/Usuarios/...`), datos personales, asignación de roles, administración de contraseñas, inventario general (carga, consulta, modificación, revisión, historial y generación), así como la gestión documental (generación y descarga de oficios en PDF). Estas URLs siguen una convención clara basada en prefijos que identifican el módulo al que pertenecen (por ejemplo, `/CargaInventarioGeneral/`, `/ConsultarInventarioGeneral/`, `/RevisionInventarioGeneral/`), lo que facilita su identificación y mantenimiento.

En cuanto a los **controladores**, el sistema implementa una arquitectura modular basada en el patrón MVC, utilizando controladores específicos para cada dominio funcional, tales como `LoginController`, `NotificationsController`, `UsuariosController`, `AreaRoleAssignerController`, `UpdatePasswordController` y diversos controladores dentro del módulo de inventario general como `CargaInventarioGeneralController`, `ConsultarInventarioGeneralController`, `RevisionInventarioGeneralController`, `HistorialInventarioGeneralController`, `ModificacionRegistrosInventarioGeneralController` y `GeneracionInventarioGeneralController`. Esta separación permite encapsular la lógica de negocio de forma organizada y escalable, además de facilitar el mantenimiento y la extensión del sistema.

La **navegación del sistema** se basa principalmente en un flujo dinámico soportado por peticiones AJAX mediante rutas de tipo POST, lo que permite interactuar con la aplicación sin recargar la página. El usuario inicia sesión, accede a sus datos y posteriormente interactúa con distintos módulos según sus permisos. En el caso del inventario general, el flujo está claramente definido: comienza con la **captura de datos**, continúa con su **consulta**, posible **edición o modificación**, seguido de un proceso de **revisión y validación**, para finalmente pasar a su **aprobación, almacenamiento histórico y generación de documentos oficiales**. Este flujo refleja un sistema robusto orientado a la gestión completa del ciclo de vida de la información, con control de estados, trazabilidad y separación clara de responsabilidades.

---
---

# Estructura del archivo

El archivo está dividido principalmente en dos tipos de solicitudes HTTP:

- **GET Requests**
    
- **POST Requests**
    

Cada tipo de solicitud define rutas específicas dependiendo de la operación que se desea realizar dentro del sistema.

---

## 1. Importación de clases

```PHP
use CodeIgniter\Router\RouteCollection;
```

Esta línea importa la clase **RouteCollection**, que proporciona los métodos necesarios para registrar rutas dentro de la aplicación.

---

# 2. Definición del objeto de rutas

```PHP
/**  
 * @var RouteCollection $routes  
 */
```

Esta anotación indica que la variable **`$routes`** es una instancia de la clase **RouteCollection**, lo que permite acceder a los métodos:

- `get()`
    
- `post()`
    
- `put()`
    
- `delete()`
    

En este archivo se utilizan principalmente **GET y POST**.

---
---
---

# Rutas GET

Las rutas **GET** se utilizan principalmente para **cargar vistas o páginas del sistema**.

---

## Sección: Rutas Comunes (Common)

Esta sección define las rutas básicas del sistema, las cuales corresponden a funcionalidades generales accesibles desde la interfaz principal de la aplicación. Estas rutas permiten el acceso a páginas informativas o de uso frecuente dentro del sistema.

---

### Ruta: Página de inicio

```PHP
$routes->get('/', 'HomeController::index');
```

**Descripción:**  
Define la ruta raíz de la aplicación. Cuando un usuario accede a la URL principal (`/`), se ejecuta el método `index` del controlador `HomeController`.

**Funcionalidad:**

- Carga la página principal del sistema.
    
- Actúa como punto de entrada para los usuarios.
    
- Puede mostrar información general, panel principal o dashboard.
    

---

### Ruta: Control de versión

```PHP
$routes->get('/Version', 'changeControl\ChangeControlController::index');
```

**Descripción:**  
Define la ruta para acceder a la sección de control de versiones del sistema.

> [!info] **Funcionalidad:**
>
> - Muestra información relacionada con la versión actual de la aplicación.
> - Puede incluir historial de cambios, actualizaciones o control de versiones implementadas.
> - Es útil para fines de mantenimiento, auditoría o seguimiento del sistema.

---
---

## Sección: Búsqueda de Códigos (Code Search)

Esta sección agrupa las rutas relacionadas con los módulos de **búsqueda y consulta de información**, permitiendo a los usuarios acceder a herramientas especializadas para localizar códigos dentro del sistema, así como funcionalidades complementarias asociadas.

---

### Ruta: Búsqueda de códigos

```PHP
$routes->get('/BuscarCodigo', 'CodeSearch\CodeSearchController::index');
```

**Descripción:**  
Define la ruta para acceder al módulo de búsqueda de códigos. Al ingresar a la URL `/BuscarCodigo`, se ejecuta el método `index` del controlador `CodeSearchController`.

**Funcionalidad:**

- Carga la interfaz principal de búsqueda.
    
- Permite al usuario consultar códigos mediante diferentes criterios.
    
- Sirve como punto de entrada para operaciones de búsqueda más complejas (generalmente soportadas por peticiones AJAX).
    

---

### Ruta: Contraseña genérica

```PHP
$routes->get('/GenericPassword', 'GenericPasswordController::index');
```

**Descripción:**  
Define la ruta para acceder al módulo de gestión o consulta de contraseñas genéricas.

**Funcionalidad:**

- Muestra la interfaz asociada a la generación o consulta de contraseñas genéricas.
    
- Puede utilizarse como herramienta auxiliar dentro del sistema, ya sea para administración o soporte.
    
- Facilita el acceso a funcionalidades relacionadas con credenciales predeterminadas o temporales.

---
---

## Sección: Autenticación (Login & Logout)

Esta sección define las rutas encargadas de la **gestión de autenticación de usuarios**, permitiendo el acceso al sistema mediante credenciales y la finalización de la sesión activa. Estas rutas son fundamentales para el control de acceso y la seguridad de la aplicación.

---

### Ruta: Inicio de sesión (Login)

```PHP
$routes->get('/Ingresar', 'Login\LoginController::index');
```

**Descripción:**  
Define la ruta para acceder a la interfaz de inicio de sesión. Al ingresar a la URL `/Ingresar`, se ejecuta el método `index` del controlador `LoginController`.

**Funcionalidad:**

- Muestra el formulario de autenticación.
- Permite al usuario ingresar sus credenciales (usuario y contraseña).
- Actúa como punto de entrada para usuarios no autenticados.

---

### Ruta: Cierre de sesión (Logout)

```PHP
$routes->get('/Salir', 'Login\LoginController::Logout');
```

**Descripción:**  
Define la ruta para cerrar la sesión del usuario. Al acceder a la URL `/Salir`, se ejecuta el método `Logout` del controlador `LoginController`.

**Funcionalidad:**

- Finaliza la sesión activa del usuario.
- Elimina o invalida los datos de sesión almacenados.
- Redirige al usuario a la página principal o de inicio de sesión.

---
---

## Sección: Perfil de Usuario (Profile)

Esta sección define la ruta asociada a la visualización del **perfil del usuario autenticado**, permitiendo el acceso a información general relacionada con su cuenta dentro del sistema.

---

### Ruta: Perfil

```PHP
$routes->get('/Perfil', 'Profile\ProfileController::index');
```

**Descripción:**  
Define la ruta para acceder al perfil del usuario. Al ingresar a la URL `/Perfil`, se ejecuta el método `index` del controlador `ProfileController`.

**Funcionalidad:**

- Muestra la información general del usuario autenticado.
- Permite visualizar datos relevantes de la cuenta.
- Puede servir como punto de acceso a otras funcionalidades relacionadas con la cuenta del usuario.

---
---

## Sección: Información Personal (Personal Info)

Esta sección agrupa las rutas relacionadas con la **consulta y administración de los datos personales de los usuarios**, diferenciando entre funcionalidades para usuarios comunes y administradores del sistema.

---

### Ruta: Datos personales (usuario)

```PHP
$routes->get('/DatosPersonales', 'DatosPersonales\DatosPersonalesController::index');
```

**Descripción:**  
Define la ruta para que un usuario acceda a la visualización y gestión de sus propios datos personales.

**Funcionalidad:**

- Permite consultar la información personal registrada en el sistema.
- Facilita la actualización de datos por parte del propio usuario.
- Proporciona una interfaz para la gestión básica de su información.

---

### Ruta: Administración de datos personales

```PHP
$routes->get('/AdminDatosPersonales', 'DatosPersonales\AdminDatosPersonalesController::index');
```

**Descripción:**  
Define la ruta para la administración de datos personales desde un perfil con privilegios elevados (administrador).

**Funcionalidad:**

- Permite gestionar la información de múltiples usuarios.
- Facilita la asignación o modificación de datos asociados a usuarios.
- Proporciona herramientas administrativas para el control de información personal dentro del sistema.

---
---

## Sección: Notificaciones (Notifications)

Esta sección define la ruta encargada de la visualización de las **notificaciones del sistema**, permitiendo al usuario consultar información relevante generada por distintos módulos de la aplicación.

---

### Ruta: Notificaciones

```PHP
$routes->get('/Notificaciones', 'Notifications\NotificationsController::index');
```

**Descripción:**  
Define la ruta para acceder al módulo de notificaciones. Al ingresar a la URL `/Notificaciones`, se ejecuta el método `index` del controlador `NotificationsController`.

**Funcionalidad:**

- Muestra las notificaciones asociadas al usuario.
- Permite visualizar alertas, avisos o eventos generados por el sistema.
- Centraliza la comunicación interna entre el sistema y el usuario.

---
---

## Sección: Administración de Contraseñas (Admin Update Passwords)

Esta sección agrupa la ruta destinada a la **gestión administrativa de contraseñas**, facilitando su actualización dentro del sistema.

---

### Ruta: Actualización de contraseñas

```PHP
$routes->get('/UpdatePassword', 'UpdatePassword\UpdatePasswordController::index');
```

**Descripción:**  
Define la ruta para acceder al módulo de actualización de contraseñas. Al ingresar a la URL `/UpdatePassword`, se ejecuta el método `index` del controlador `UpdatePasswordController`.

**Funcionalidad:**

- Permite actualizar contraseñas de usuarios.
- Puede incluir funcionalidades tanto para usuarios como para administradores.
- Refuerza la seguridad del sistema mediante la gestión de credenciales.

---
---

## Sección: Asignación de Roles por Área (Area Role Assigner)

Esta sección define la ruta para la gestión de **roles asociados a áreas productoras**, permitiendo la asignación de responsabilidades dentro del sistema.

---

### Ruta: Asignación de áreas

```PHP
$routes->get('/AsignadoDeAreas', 'AreaRoleAssigner\AreaRoleAssignerController::index');
```

**Descripción:**  
Define la ruta para acceder al módulo de asignación de roles por área. Al ingresar a la URL `/AsignadoDeAreas`, se ejecuta el método `index` del controlador `AreaRoleAssignerController`.

**Funcionalidad:**

- Permite asignar usuarios responsables a áreas productoras.
- Facilita la administración de roles dentro de la organización.
- Apoya la estructuración jerárquica y funcional del sistema.

---
---

## Sección: Cortes Parciales (CortesParciales)

Esta sección agrupa la ruta relacionada con la **programación de cortes parciales**, los cuales forman parte de la gestión operativa del sistema.

---

### Ruta: Programar cortes parciales

```PHP
$routes->get('/CortesParciales/Programar', 'CortesParciales\CortesParcialesController::Programar');
```

**Descripción:**  
Define la ruta para acceder a la funcionalidad de programación de cortes parciales. Al ingresar a la URL `/CortesParciales/Programar`, se ejecuta el método `Programar` del controlador `CortesParcialesController`.

**Funcionalidad:**

- Permite programar cortes parciales dentro del sistema.
- Facilita la planificación de procesos o periodos específicos.
- Forma parte de la gestión temporal de operaciones o registros.

---
---

## Sección: Gestión de Usuarios (Usuarios)

Esta sección agrupa las rutas relacionadas con la **administración de usuarios del sistema**, incluyendo la creación, eliminación, consulta y monitoreo de accesos. Estas funcionalidades están orientadas principalmente a perfiles con privilegios administrativos.

---

### Ruta: Crear usuario

```PHP
$routes->get('/Usuarios/CrearUsuario', 'Usuarios\UsuariosController::CrearUsuarioView');
```

**Descripción:**  
Define la ruta para acceder a la interfaz de creación de nuevos usuarios.

**Funcionalidad:**

- Muestra el formulario para registrar un nuevo usuario.
- Permite capturar información necesaria para el alta en el sistema.

---

### Ruta: Eliminar usuario

```PHP
$routes->get('/Usuarios/EliminarUsuario', 'Usuarios\UsuariosController::EliminarUsuarioView');
```

**Descripción:**  
Define la ruta para acceder a la interfaz de eliminación de usuarios.

**Funcionalidad:**

- Permite buscar y seleccionar usuarios existentes.
- Facilita la eliminación de registros de usuarios del sistema.

---

### Ruta: Consultar usuarios

```PHP
$routes->get('/Usuarios/ConsultarUsuarios', 'Usuarios\UsuariosController::ConsultarUsuariosView');
```

**Descripción:**  
Define la ruta para visualizar la lista de usuarios registrados.

**Funcionalidad:**

- Muestra información general de los usuarios.
- Permite realizar consultas y filtrados.

---

### Ruta: Historial de acceso (vista)

```PHP
$routes->get('/Usuarios/HistorialAcceso', 'HistorialAcceso\HistorialAccesoController::HistorialAccesoView');
```

**Descripción:**  
Define la ruta para acceder a la interfaz de visualización del historial de accesos.

**Funcionalidad:**

- Permite consultar los registros de inicio y cierre de sesión.
- Facilita el monitoreo de actividad de los usuarios.

---

### Ruta: Historial de acceso (formato JSON)

```PHP
$routes->get('/Usuarios/HistorialAcceso/json', 'HistorialAcceso\HistorialAccesoController::ObtenerHistorialJson');
```

**Descripción:**  
Define la ruta para obtener el historial de accesos en formato JSON.

**Funcionalidad:**

- Proporciona datos estructurados para consumo mediante AJAX.
- Permite la integración con componentes dinámicos en la interfaz.

---
---

## Sección: Inventario General

Esta sección define las rutas correspondientes al módulo de **Inventario General**, el cual permite gestionar el ciclo completo de los registros: carga, revisión, consulta, modificación e historial.

---

### Ruta: Carga de inventario

```PHP
$routes->get('/InventarioGeneral/Cargar', 'InventarioGeneral\CargaInventarioGeneralController::Index');
```

**Descripción:**  
Acceso al módulo de carga de inventario general.

**Funcionalidad:**

- Permite registrar nuevos datos en el inventario.
- Facilita la captura inicial de información.

---

### Ruta: Revisión de inventario

```PHP
$routes->get('/InventarioGeneral/Revisar', 'InventarioGeneral\RevisionInventarioGeneralController::Index');
```

**Descripción:**  
Acceso al módulo de revisión de inventario.

**Funcionalidad:**

- Permite validar y aprobar registros.
- Facilita el control de calidad de la información.

---

### Ruta: Consulta de inventario

```PHP
$routes->get('/InventarioGeneral/Consultar', 'InventarioGeneral\ConsultarInventarioGeneralController::Index');
```

**Descripción:**  
Acceso al módulo de consulta de inventario.

**Funcionalidad:**

- Permite buscar y visualizar registros existentes.
- Facilita el acceso a información almacenada.

---

### Ruta: Modificación de inventario

```PHP
$routes->get('/InventarioGeneral/Modificar', 'InventarioGeneral\ModificacionRegistrosInventarioGeneralController::Index');
```

**Descripción:**  
Acceso al módulo de modificación de registros.

**Funcionalidad:**

- Permite editar información previamente registrada.
- Facilita la actualización de datos del inventario.

---

### Ruta: Historial de registros

```PHP
$routes->get('/InventarioGeneral/HistorialRegistros', 'InventarioGeneral\HistorialInventarioGeneralController::index');
```

**Descripción:**  
Acceso al historial del inventario general.

**Funcionalidad:**

- Permite consultar cambios realizados en los registros.
- Facilita auditorías y seguimiento de modificaciones.

---

# Rutas POST

Las rutas **POST** se utilizan principalmente para:

- Enviar datos desde formularios
    
- Realizar consultas AJAX
    
- Guardar o modificar información en la base de datos
    

---
---

## Sección: Búsqueda de Códigos (Code Search - POST)

Esta sección define las rutas de tipo **POST** asociadas al módulo de **búsqueda de códigos**, las cuales están diseñadas para procesar solicitudes asíncronas (AJAX) y proporcionar datos dinámicos a la interfaz de usuario.

Estas rutas permiten realizar consultas específicas y obtener información estructurada relacionada con catálogos, facilitando la navegación jerárquica y la recuperación eficiente de datos.

---

### Ruta: Búsqueda de código

```PHP
$routes->post('/CodeSearchAjax', 'CodeSearch\CodeSearchController::searchCode');
```

**Descripción:**  
Procesa la solicitud de búsqueda de códigos enviada desde la interfaz.

**Funcionalidad:**

- Recibe parámetros de búsqueda.
- Retorna resultados coincidentes.
- Permite consultas dinámicas sin recargar la página.

---

### Ruta: Búsqueda por palabra clave
```PHP
$routes->post('/CodeSearchKeywordAjax', 'CodeSearch\CodeSearchController::searchCodeKeyword');
```

**Descripción:**  
Permite realizar búsquedas utilizando palabras clave específicas.

**Funcionalidad:**

- Filtra resultados en función de términos ingresados.
- Mejora la precisión en la localización de códigos.

---

### Ruta: Obtener años de catálogo

```PHP
$routes->post('/GetCatalogYearsAjax', 'CodeSearch\CodeSearchController::GetCatalogYears');
```

**Descripción:**  
Obtiene la lista de años disponibles en el catálogo.

**Funcionalidad:**

- Proporciona datos para poblar listas desplegables.
- Permite segmentar la búsqueda por año.

---

### Ruta: Obtener secciones del catálogo

```PHP
$routes->post('/GetCatalogSectionsAjax', 'CodeSearch\CodeSearchController::GetCatalogSections');
```

**Descripción:**  
Recupera las secciones disponibles dentro de un catálogo.

**Funcionalidad:**

- Permite organizar la información en categorías.
- Facilita la navegación jerárquica.

---

### Ruta: Obtener series del catálogo

```PHP
$routes->post('/GetCatalogSeriesAjax', 'CodeSearch\CodeSearchController::GetCatalogSeries');
```

**Descripción:**  
Obtiene las series correspondientes a una sección específica.

**Funcionalidad:**

- Refina la búsqueda dentro de una estructura jerárquica.
- Permite filtrar información de manera progresiva.

---

### Ruta: Obtener subseries del catálogo

```PHP
$routes->post('/GetCatalogSubseriesAjax', 'CodeSearch\CodeSearchController::GetCatalogSubseries');
```

**Descripción:**  
Recupera las subseries asociadas a una serie determinada.

**Funcionalidad:**

- Permite un nivel más detallado de clasificación.
- Mejora la precisión en la consulta de datos.

---
---

## Sección: Gestión de Datos de Usuario (Datos de Usuario - POST)

Esta sección define las rutas de tipo **POST** encargadas de la **consulta y actualización de datos personales de los usuarios**, diferenciando entre operaciones realizadas por **administradores del sistema** y aquellas realizadas por **usuarios comunes**.

Estas rutas están diseñadas para ser consumidas mediante **peticiones AJAX**, permitiendo la interacción dinámica con la información sin necesidad de recargar la interfaz.

---

## Sub-sección: Administración de datos (Administrador)

Las siguientes rutas están destinadas a usuarios con privilegios administrativos, permitiendo la gestión de información de múltiples usuarios dentro del sistema.

---

### Ruta: Obtener divisiones

```PHP
$routes->post('/Admin/GetDivisionsAjax', 'DatosPersonales\AdminDatosPersonalesController::GetDivisions');
```

**Descripción:**  
Recupera la lista de divisiones disponibles en el sistema.

**Funcionalidad:**

- Proporciona datos para segmentar usuarios.
- Permite organizar la información por estructura organizacional.

---

### Ruta: Obtener áreas productoras

```PHP
$routes->post('/Admin/GetAreaProductoraAjax', 'DatosPersonales\AdminDatosPersonalesController::GetAreaProductora');
```

**Descripción:**  
Obtiene las áreas productoras asociadas a una división.

**Funcionalidad:**

- Facilita la clasificación de usuarios.
- Permite una gestión jerárquica de la información.

---

### Ruta: Obtener usuarios no asignados

```PHP
$routes->post('/Admin/GetNotAsignedUsersAjax', 'DatosPersonales\AdminDatosPersonalesController::GetNotAsignedUsers');
```

**Descripción:**  
Recupera la lista de usuarios que no han sido asignados a un área productora.

**Funcionalidad:**

- Identifica usuarios pendientes de asignación.
- Apoya la administración de recursos humanos dentro del sistema.

---

### Ruta: Obtener usuarios por área productora

```PHP
$routes->post('/Admin/GetUsersByAreaProductoraAjax', 'DatosPersonales\AdminDatosPersonalesController::GetUsersByAreaProductora');
```

**Descripción:**  
Obtiene los usuarios asociados a un área productora específica.

**Funcionalidad:**

- Permite visualizar la distribución de usuarios.
- Facilita la gestión por áreas.

---

### Ruta: Obtener datos de usuario (administrador)

```PHP
$routes->post('/AdminGetUserDataAjax', 'DatosPersonales\AdminDatosPersonalesController::GetAdminUserData');
```

**Descripción:**  
Recupera la información detallada de un usuario específico.

**Funcionalidad:**

- Permite visualizar datos personales completos.
- Facilita la edición de información por parte del administrador.

---

### Ruta: Actualizar datos de usuario (administrador)

```PHP
$routes->post('/AdminUpdateUserDataAjax', 'DatosPersonales\AdminDatosPersonalesController::UpdateAdminUserData');
```

**Descripción:**  
Permite actualizar la información de un usuario desde el perfil administrativo.

**Funcionalidad:**

- Modifica datos personales de cualquier usuario.
- Garantiza la administración centralizada de la información.

---

## Sub-sección: Gestión de datos (Usuario común)

Las siguientes rutas están destinadas a usuarios autenticados sin privilegios administrativos, permitiendo la gestión de su propia información personal.

---

### Ruta: Obtener datos personales

```PHP
$routes->post('/GetUserDataAjax', 'DatosPersonales\DatosPersonalesController::GetUserData');
```

**Descripción:**  
Recupera la información personal del usuario autenticado.

**Funcionalidad:**

- Permite visualizar datos propios.
- Proporciona información para su edición.

---

### Ruta: Actualizar datos personales

```PHP
$routes->post('/UpdateUserDataAjax', 'DatosPersonales\DatosPersonalesController::UpdateUserData');
```

**Descripción:**  
Permite al usuario actualizar su información personal.

**Funcionalidad:**

- Modifica datos registrados en el sistema.
- Facilita la autogestión de la información del usuario.

---
---

## Sección: Notificaciones (Notifications - POST)

Esta sección define las rutas de tipo **POST** relacionadas con la **gestión de notificaciones del sistema**, permitiendo la consulta, conteo e inserción de notificaciones mediante solicitudes asíncronas (AJAX).

---

### Ruta: Obtener notificaciones

```PHP
$routes->post('/GetNotificationsAjax', 'Notifications\NotificationsController::GetNotifications');
```

**Descripción:**  
Recupera la lista de notificaciones asociadas al usuario.

**Funcionalidad:**

- Obtiene notificaciones almacenadas en el sistema.
- Permite su visualización dinámica en la interfaz.
- Soporta la actualización sin recarga de página.

---

### Ruta: Obtener conteo de notificaciones

```PHP
$routes->post('/GetNotificationsCountAjax', 'Notifications\NotificationsController::GetNotificationsCount');
```

**Descripción:**  
Obtiene el número total de notificaciones, generalmente no leídas.

**Funcionalidad:**

- Permite mostrar indicadores visuales (badges).
- Facilita la notificación en tiempo real al usuario.

---

### Ruta: Insertar notificación

```PHP
$routes->post('/InsertNotificationAjax', 'Notifications\NotificationsController::InsertNotification');
```

**Descripción:**  
Permite registrar una nueva notificación en el sistema.

**Funcionalidad:**

- Inserta eventos o avisos generados por el sistema.
- Facilita la comunicación interna entre módulos.

---
---

## Sección: Autenticación (Login - POST)

Esta sección agrupa las rutas encargadas del **procesamiento de credenciales de acceso**, permitiendo validar la identidad del usuario y controlar el acceso al sistema.

---

### Ruta: Inicio de sesión

```PHP
$routes->post('/Ingresar', 'Login\LoginController::Login');
```

**Descripción:**  
Procesa las credenciales enviadas desde el formulario de inicio de sesión.

**Funcionalidad:**

- Valida usuario y contraseña.
- Inicia la sesión del usuario si las credenciales son correctas.
- Gestiona errores de autenticación.

---

### Ruta: Inicio de sesión (Generador)

```PHP
$routes->post('/IngresarGenerador', 'Login\LoginController::LoginGenerador');
```

**Descripción:**  
Permite un tipo alternativo de autenticación, posiblemente asociado a un perfil o módulo específico denominado “Generador”.

**Funcionalidad:**

- Procesa credenciales bajo un contexto específico.
- Permite acceso diferenciado según el tipo de usuario.

---

> [!warning] Nota importante  
> ```php
> $routes->post('/Ingresar', 'Login\LoginController::Login');
> ```
> Esta ruta se encuentra duplicada, lo cual puede generar redundancia o comportamientos inesperados.  
> Se recomienda revisar su definición para evitar conflictos en el enrutamiento.

---
---

## Sección: Datos de Vista (View Data)

Esta sección define una ruta para la obtención de datos necesarios para la carga de vistas principales del sistema.

---

### Ruta: Obtener datos para la vista principal

```PHP
$routes->post('/GetIndexViewData', 'BaseController::GetIndexViewData');
```

**Descripción:**  
Recupera información necesaria para la inicialización de la vista principal del sistema.

**Funcionalidad:**

- Proporciona datos base para la carga del dashboard o página inicial.
- Centraliza la obtención de información común a múltiples vistas.
- Facilita la renderización dinámica de contenido.

---
---

## Sección: Administración de Contraseñas (Admin Update Passwords - POST)

Esta sección define las rutas de tipo **POST** destinadas a la **gestión y actualización de contraseñas de usuarios**, principalmente desde un contexto administrativo. Estas rutas permiten obtener información estructurada de usuarios y ejecutar cambios en sus credenciales.

---

### Sub-sección: Obtención de usuarios

Las siguientes rutas permiten recuperar información necesaria para identificar y seleccionar usuarios dentro de la estructura organizacional.

#### Funcionalidades:

- Obtener divisiones disponibles.
- Consultar áreas productoras asociadas.
- Identificar usuarios no asignados.
- Listar usuarios por área productora.

Estas operaciones permiten establecer un flujo jerárquico de selección:  
**División → Área Productora → Usuario**

---

### Sub-sección: Actualización de contraseñas

```PHP
$routes->post('/UpdatePasswordAjax', 'UpdatePassword\UpdatePasswordController::updatePassword');
```

**Descripción:**  
Permite actualizar la contraseña de un usuario seleccionado.

**Funcionalidad:**

- Modifica credenciales en el sistema.
- Refuerza la seguridad mediante gestión centralizada.
- Puede ser utilizada en procesos de recuperación o administración.

---
---

## Sección: Asignación de Roles por Área (Area Role Assigner - POST)

Esta sección agrupa las rutas relacionadas con la **gestión de roles dentro de áreas productoras**, permitiendo asignar o remover responsabilidades a usuarios específicos.

---

### Funcionalidades principales

- Obtener áreas no asignadas.
- Consultar usuarios responsables por área.
- Obtener áreas asociadas a usuarios.
- Asignar jefe de área.
- Remover jefe de área.

---

### Rutas destacadas

```PHP
$routes->post('/SetAreaChief', 'AreaRoleAssigner\AreaRoleAssignerController::SetAreaChief');  
$routes->post('/UnsetAreaChief', 'AreaRoleAssigner\AreaRoleAssignerController::UnsetAreaChief');
```

**Descripción:**  
Permiten asignar o remover el rol de responsable (jefe) de un área productora.

**Funcionalidad:**

- Gestiona jerarquías dentro del sistema.
- Define responsables de áreas operativas.

---
---

## Sección: Cortes Parciales (CortesParciales - POST)

Esta sección define las rutas para la **gestión completa de cortes parciales**, permitiendo su administración a través de operaciones CRUD (Crear, Leer, Actualizar y Eliminar).

---

### Funcionalidades

- Programar cortes parciales.
- Crear nuevos registros.
- Editar información existente.
- Eliminar registros.

---

### Rutas

```PHP
$routes->post('/CortesParciales/Programar', 'CortesParciales\CortesParcialesController::Programar');  
$routes->post('/CortesParciales/Crear', 'CortesParciales\CortesParcialesController::Crear');  
$routes->post('/CortesParciales/Editar', 'CortesParciales\CortesParcialesController::Editar');  
$routes->post('/CortesParciales/Eliminar', 'CortesParciales\CortesParcialesController::Eliminar');
```

---
---

## Sección: Gestión de Usuarios (Usuarios - POST)

Esta sección define las rutas para la **administración de usuarios mediante operaciones dinámicas**, incluyendo creación, búsqueda, eliminación y consulta de información.

---

### Funcionalidades principales

- Crear nuevos usuarios.
- Buscar usuarios para eliminación o consulta.
- Eliminar usuarios del sistema.
- Obtener áreas por división.
- Consultar historial de acceso.

---

### Rutas destacadas

```PHP
$routes->post('/Usuarios/CrearUsuarioAjax', 'Usuarios\UsuariosController::CrearUsuario');  
$routes->post('/Usuarios/EliminarUsuario', 'Usuarios\UsuariosController::EliminarUsuario');
```

**Descripción:**  
Permiten la creación y eliminación de usuarios dentro del sistema.

---

### Ruta: Historial de acceso

```PHP
$routes->post('/Usuarios/GetHistorialAccesoAjax', 'HistorialAcceso\HistorialAccesoController::GetHistorialAcceso');
```

**Descripción:**  
Recupera el historial de accesos de los usuarios.

**Funcionalidad:**

- Permite auditoría de actividades.
- Facilita el monitoreo de uso del sistema.

---
---

## Sección: Carga de Inventario General (POST)

Esta sección agrupa las rutas encargadas de la **gestión, captura y envío a revisión del inventario general**, permitiendo al usuario interactuar con catálogos, registrar información y administrar registros en estado de aprobación.

---

### Sub-sección: Obtención de catálogos y estructuras

Las siguientes rutas permiten obtener información necesaria para la correcta clasificación del inventario:

- Vigencias aplicables.
- Años de catálogo disponibles.
- Secciones por año.
- Series y subseries asociadas a un año.

**Funcionalidad:**

- Proporcionan datos estructurados para la captura del inventario.
- Permiten mantener consistencia con la clasificación archivística.
- Facilitan la navegación jerárquica de los datos.

---

### Sub-sección: Gestión de inventario en aprobación

```PHP
$routes->post('/CargaInventarioGeneral/GetInventarioGeneralEnAprobacionAjax', 'InventarioGeneral\CargaInventarioGeneralController::GetInventarioGeneralEnAprobacion');  
$routes->post('/CargaInventarioGeneral/DeleteInventarioGeneralEnAprobacionAjax', 'InventarioGeneral\CargaInventarioGeneralController::DeleteInventarioGeneralEnAprobacion');
```

**Descripción:**  
Permiten consultar y eliminar registros de inventario que se encuentran en estado de aprobación.

**Funcionalidad:**

- Recuperar registros pendientes de revisión.
- Eliminar registros antes de su validación final.

---

### Sub-sección: Registro y almacenamiento de datos
```PHP
$routes->post('/CargaInventarioGeneral/SaveNewRowsAjax', 'InventarioGeneral\CargaInventarioGeneralController::saveNewRows');  
$routes->post('/CargaInventarioGeneral/SaveAlreadySavedRowsAjax', 'InventarioGeneral\CargaInventarioGeneralController::saveAlreadySavedRows');
```

**Descripción:**  
Permiten almacenar registros de inventario, diferenciando entre datos nuevos y previamente guardados.

**Funcionalidad:**

- Guardar nuevas entradas en el sistema.
- Actualizar registros existentes.
- Mantener persistencia de la información capturada.

---

### Sub-sección: Envío a revisión

```PHP
$routes->post('/CargaInventarioGeneral/SendToReviewAjax', 'InventarioGeneral\CargaInventarioGeneralController::SendToReview');
```

**Descripción:**  
Envía los registros capturados a un proceso de revisión.

**Funcionalidad:**

- Cambia el estado del inventario a “en revisión”.
- Inicia el flujo de validación dentro del sistema.

---
---

## Sección: Consulta de Inventario General (POST)

Esta sección define las rutas para la **consulta y visualización del inventario general**, filtrando la información según usuario, área, año y mes.

---

### Funcionalidades principales

- Obtener datos del usuario.
- Consultar años y meses disponibles.
- Recuperar inventario filtrado.
- Obtener áreas productoras asociadas al usuario.

---

### Rutas relevantes

```PHP
$routes->post('/ConsultarInventarioGeneral/GetInventarioGeneralAjax', 'InventarioGeneral\ConsultarInventarioGeneralController::GetInventarioByUsuarioAreaAnioMes');
```

**Descripción:**  
Permite obtener los registros de inventario en función de filtros específicos.

**Funcionalidad:**

- Consulta dinámica del inventario.
- Filtrado por usuario, área, año y mes.

---

### Sub-sección: Edición de registros

```PHP
$routes->post('/ConsultarInventarioGeneral/SendToEditRegistrosDelInventarioAjax', 'InventarioGeneral\ConsultarInventarioGeneralController::SendInventarioToEdit');
```

**Descripción:**  
Envía registros seleccionados a un estado editable.

**Funcionalidad:**

- Permite modificar registros previamente capturados.
- Habilita el flujo de corrección de información.

---
---

## Sección: Modificación de Inventario General (POST)

Esta sección contempla las rutas necesarias para la **modificación, actualización y reenvío a revisión de registros del inventario general**.

---

### Funcionalidades principales

- Obtener registros en proceso de modificación.
- Guardar cambios realizados.
- Enviar modificaciones a revisión.
- Eliminar registros modificados.

---

### Rutas principales

```PHP
$routes->post('/ModificacionRegistrosInventarioGeneral/GetInventarioGeneralModificacion', 'InventarioGeneral\ModificacionRegistrosInventarioGeneralController::GetInventarioGeneralModificacion');  
$routes->post('/ModificacionRegistrosInventarioGeneral/GuardarModificacionesIG', 'InventarioGeneral\ModificacionRegistrosInventarioGeneralController::GuardarModificacionesIG');
```

**Descripción:**  
Permiten la gestión de registros en proceso de modificación.

---

### Sub-sección: Envío y eliminación

```PHP
$routes->post('/ModificacionRegistrosInventarioGeneral/EnviarARevision', 'InventarioGeneral\ModificacionRegistrosInventarioGeneralController::EnviarARevision');  
$routes->post('/ModificacionRegistrosInventarioGeneral/DeleteModificacionesInventarioGeneralAjax', 'InventarioGeneral\ModificacionRegistrosInventarioGeneralController::DeleteModificacionesInventarioGeneral');
```

**Descripción:**  
Permiten enviar los cambios a revisión o eliminar registros modificados.

---
---

## Sección: Revisión de Inventario General (POST)

Esta sección define las rutas encargadas del **proceso de revisión, validación y control de calidad del inventario general**, permitiendo a los usuarios con permisos adecuados evaluar, aprobar o devolver registros.

---

### Funcionalidades principales

- Obtener registros pendientes por área productora.
- Consultar el estatus de inventarios por área.
- Actualizar el estado de los registros.
- Filtrar inventario por divisiones y áreas productoras.
- Realizar búsquedas específicas de inventario.
- Agregar comentarios de revisión.
- Devolver registros para corrección.
- Aprobar registros y convertirlos en definitivos.

---

### Rutas relevantes

```PHP
$routes->post('/GetRegistrosPendientesByAreaAjax', 'InventarioGeneral\RevisionInventarioGeneralController::GetRegistrosPendientesByAreaProductora');  
$routes->post('/UpdateInventoryStatusAjax', 'InventarioGeneral\RevisionInventarioGeneralController::UpdateInventoryStatus');  
$routes->post('/RevisionInventarioGeneral/SearchInventarioAjax', 'InventarioGeneral\RevisionInventarioGeneralController::SearchInventario');
```

**Descripción:**  
Permiten gestionar el flujo principal de revisión del inventario.

---

### Sub-sección: Gestión de comentarios y validación

```PHP
$routes->post('/RevisionInventarioGeneral/UpdateComentarioAjax', 'InventarioGeneral\RevisionInventarioGeneralController::ActualizarComentario');  
$routes->post('/RevisionInventarioGeneral/DevolverInventariosAjax', 'InventarioGeneral\RevisionInventarioGeneralController::DevolverInventarios');  
$routes->post('/RevisionInventarioGeneral/NuevoInventarioToDefinitivoAjax', 'InventarioGeneral\RevisionInventarioGeneralController::NuevoInventarioToDefinitivo');
```

**Descripción:**  
Permiten al revisor interactuar directamente con los registros mediante observaciones y decisiones de aprobación o rechazo.

**Funcionalidad:**

- Registrar observaciones.
- Devolver registros para corrección.
- Aprobar registros y marcarlos como definitivos.

---
---

## Sección: Historial de Inventario General (POST)

Esta sección permite la **consulta, auditoría y gestión histórica de los registros del inventario general**, incluyendo versiones nuevas, antiguas y transiciones de estado.

---

### Funcionalidades principales

- Obtener divisiones y áreas con inventario histórico.
- Consultar registros nuevos y antiguos.
- Actualizar comentarios del revisor.
- Rechazar registros.
- Transferir registros entre estados (actual ↔ histórico).

---

### Rutas principales

```PHP
$routes->post('/HistorialInventarioGeneral/GetNewRegistrosAjax', 'InventarioGeneral\HistorialInventarioGeneralController::SearchInventario_2');  
$routes->post('/HistorialInventarioGeneral/GetOldRegistrosAjax', 'InventarioGeneral\HistorialInventarioGeneralController::GetOldInventarioGeneral');
```

**Descripción:**  
Permiten consultar diferentes versiones de los registros de inventario.

---

### Sub-sección: Control de estados

```PHP
$routes->post('/HistorialInventarioGeneral/InventarioTOHistoricoAJAX', 'InventarioGeneral\HistorialInventarioGeneralController::InventarioGeneralTOHistorico');  
$routes->post('/HistorialInventarioGeneral/ModificadoTOInventarioAJAX', 'InventarioGeneral\HistorialInventarioGeneralController::InventarioModificadoTOInventarioGeneral');
```

**Descripción:**  
Permiten la transición de registros entre estados dentro del sistema.

**Funcionalidad:**

- Mover registros a histórico.
- Restaurar registros modificados al inventario activo.

---
---

## Sección: Gestión de Oficios y Generación de PDF (GET/POST)

Esta sección contempla las rutas para la **generación, almacenamiento y descarga de documentos oficiales (oficios)** en formato PDF.

---

### Ruta de acceso principal

```PHP
$routes->get('/DescargaOficios', 'DescargaOficios\DescargaOficiosController::index');
```

**Descripción:**  
Carga la vista principal para la gestión de oficios.

---

### Funcionalidades principales

- Obtener áreas asociadas al usuario.
- Recuperar información del usuario.
- Generar documentos PDF.
- Consultar periodos (trimestres).
- Guardar archivos generados.

---

### Rutas relevantes

```PHP
$routes->post('/GeneratePDF', 'DescargaOficios\DescargaOficiosController::GeneratePDF');  
$routes->post('/SaveFile', 'DescargaOficios\DescargaOficiosController::SaveFile');
```

**Descripción:**  
Permiten la generación y almacenamiento de documentos oficiales.

**Funcionalidad:**

- Crear archivos PDF dinámicamente.
- Persistir documentos en el sistema.

---
---

## Sección: Generación de Inventario General (POST)

Esta sección define las rutas encargadas de la **generación consolidada del inventario general**, integrando información proveniente de distintas entidades del sistema, como áreas productoras, cortes parciales y responsables administrativos.

---

### Funcionalidades principales

- Obtener áreas productoras.
- Consultar cortes parciales disponibles.
- Recuperar registros del inventario general.
- Obtener responsables asociados:
    - Responsable del área productora.
    - Responsable archivístico.
    - Titular del área universitaria.

---

### Rutas relevantes

```PHP
$routes->post('/GeneracionInventarioGeneral/GetAreasProductoras', 'InventarioGeneral\GeneracionInventarioGeneralController::GetAreasProductoras');  
$routes->post('/GeneracionInventarioGeneral/GetRegistrosInventarioGeneral', 'InventarioGeneral\GeneracionInventarioGeneralController::GetRegistrosInventarioGeneral');
```

**Descripción:**  
Permiten obtener los datos base necesarios para la generación del inventario.

---

### Sub-sección: Obtención de responsables

```PHP
$routes->post('/GeneracionInventarioGeneral/GetResponsableAreaProductora', 'InventarioGeneral\GeneracionInventarioGeneralController::GetResponsableAreaProductora');  
$routes->post('/GeneracionInventarioGeneral/GetResponsableArchivistica', 'InventarioGeneral\GeneracionInventarioGeneralController::GetResponsableArchivistica');  
$routes->post('/GeneracionInventarioGeneral/GetTitularAreaUniversitaria', 'InventarioGeneral\GeneracionInventarioGeneralController::GetTitularAreaUniversitaria');
```

**Descripción:**  
Permiten recuperar la información de los responsables necesarios para la validación y formalización del inventario.

**Funcionalidad:**

- Integrar firmas o responsables en documentos finales.
- Garantizar la validez administrativa del inventario generado.

---
---

## Sección: Inserción de Inventario General (GET/POST)

Esta sección define las rutas para la **inserción manual de registros de inventario general**, permitiendo registrar información directamente en el sistema.

---

### Ruta de acceso principal
```PHP
$routes->get('/InventarioGeneral/Insert', 'InventarioGeneral\InsertInventarioController::index');
```

**Descripción:**  
Carga la vista principal para la inserción de inventario.

---

### Funcionalidades principales

- Obtener información de áreas productoras mediante clave.
- Insertar registros de inventario en formato estructurado (JSON).

---

### Rutas relevantes

```PHP
$routes->get('/InventarioGeneral/Insert/GetAreaAjax', 'InventarioGeneral\InsertInventarioController::GetAreaProductoraByClave');  
$routes->post('/InventarioGeneral/Insert/DoInsertAjax', 'InventarioGeneral\InsertInventarioController::InsertInventarioJSON');
```

**Descripción:**  
Permiten la consulta de datos y la inserción de nuevos registros.

**Funcionalidad:**

- Validar datos antes de inserción.
- Registrar información directamente en la base de datos.
- Soportar estructuras complejas mediante JSON.

---
---

## Sección: Hashing de Contraseñas (GET)

Esta sección define una ruta destinada al **procesamiento o visualización de hashing de contraseñas**, comúnmente utilizada con fines de seguridad o pruebas.

---

### Ruta

```PHP
$routes->get('/HashingPassword', 'HashingPasswordController::index');
```

**Descripción:**  
Permite acceder a una funcionalidad relacionada con el cifrado (hashing) de contraseñas.

---

### Funcionalidad

- Generar representaciones hash de contraseñas.
- Validar mecanismos de seguridad.
- Servir como herramienta de prueba o demostración.

---
