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

**Funcionalidad:**

- Muestra información relacionada con la versión actual de la aplicación.
    
- Puede incluir historial de cambios, actualizaciones o control de versiones implementadas.
    
- Es útil para fines de mantenimiento, auditoría o seguimiento del sistema.

---

---

## Sección: Búsqueda de Códigos (Code Search)

Esta sección agrupa las rutas relacionadas con los módulos de **búsqueda y consulta de información**, permitiendo a los usuarios acceder a herramientas especializadas para localizar códigos dentro del sistema, así como funcionalidades complementarias asociadas.

---

### Ruta: Búsqueda de códigos

$routes->get('/BuscarCodigo', 'CodeSearch\CodeSearchController::index');

**Descripción:**  
Define la ruta para acceder al módulo de búsqueda de códigos. Al ingresar a la URL `/BuscarCodigo`, se ejecuta el método `index` del controlador `CodeSearchController`.

**Funcionalidad:**

- Carga la interfaz principal de búsqueda.
    
- Permite al usuario consultar códigos mediante diferentes criterios.
    
- Sirve como punto de entrada para operaciones de búsqueda más complejas (generalmente soportadas por peticiones AJAX).
    

---

### Ruta: Contraseña genérica

$routes->get('/GenericPassword', 'GenericPasswordController::index');

**Descripción:**  
Define la ruta para acceder al módulo de gestión o consulta de contraseñas genéricas.

**Funcionalidad:**

- Muestra la interfaz asociada a la generación o consulta de contraseñas genéricas.
    
- Puede utilizarse como herramienta auxiliar dentro del sistema, ya sea para administración o soporte.
    
- Facilita el acceso a funcionalidades relacionadas con credenciales predeterminadas o temporales.

---

### Autenticación

|Ruta|Controlador|
|---|---|
|`/Ingresar`|`LoginController::index`|
|`/Salir`|`LoginController::Logout`|

Gestionan el acceso y cierre de sesión de los usuarios.

---

### Perfil de usuario

|Ruta|Controlador|
|---|---|
|`/Perfil`|`ProfileController::index`|

Permite visualizar la información del perfil del usuario.

---

### Datos personales

|Ruta|Controlador|
|---|---|
|`/DatosPersonales`|`DatosPersonalesController::index`|
|`/AdminDatosPersonales`|`AdminDatosPersonalesController::index`|

Sección para visualizar y administrar los datos personales de los usuarios.

---

### Notificaciones

|Ruta|Controlador|
|---|---|
|`/Notificaciones`|`NotificationsController::index`|

Permite visualizar notificaciones dentro del sistema.

---

### Administración de usuarios

|Ruta|Controlador|
|---|---|
|`/Usuarios/CrearUsuario`|`UsuariosController::CrearUsuarioView`|
|`/Usuarios/EliminarUsuario`|`UsuariosController::EliminarUsuarioView`|
|`/Usuarios/ConsultarUsuarios`|`UsuariosController::ConsultarUsuariosView`|
|`/Usuarios/HistorialAcceso`|`HistorialAccesoController::HistorialAccesoView`|

Estas rutas permiten acceder a las vistas para la gestión de usuarios.

---

### Inventario General

|Ruta|Controlador|
|---|---|
|`/InventarioGeneral/Cargar`|`CargaInventarioGeneralController::Index`|
|`/InventarioGeneral/Revisar`|`RevisionInventarioGeneralController::Index`|
|`/InventarioGeneral/Consultar`|`ConsultarInventarioGeneralController::Index`|
|`/InventarioGeneral/Modificar`|`ModificacionRegistrosInventarioGeneralController::Index`|
|`/InventarioGeneral/HistorialRegistros`|`HistorialInventarioGeneralController::index`|

Estas rutas corresponden al **módulo de inventario general**, donde se gestionan registros, revisiones y modificaciones.

---

# 4. Rutas POST

Las rutas **POST** se utilizan principalmente para:

- Enviar datos desde formularios
    
- Realizar consultas AJAX
    
- Guardar o modificar información en la base de datos
    

---

## Ejemplo de ruta POST

```PHP
$routes->post('/CodeSearchAjax', 'CodeSearchController::searchCode');
```

Esta ruta recibe una solicitud **POST** enviada generalmente mediante **AJAX** y ejecuta el método `searchCode`.

---

# Principales módulos con rutas POST

## 1. Búsqueda de códigos

Permiten obtener información relacionada con códigos archivísticos.

Ejemplos:

- `searchCode`
    
- `searchCodeKeyword`
    
- `GetCatalogYears`
    
- `GetCatalogSections`
    
- `GetCatalogSeries`
    
- `GetCatalogSubseries`
    

---

## 2. Gestión de datos de usuario

Incluye rutas para:

- Obtener información del usuario
    
- Actualizar datos personales
    
- Administrar usuarios por área o división
    

---

## 3. Sistema de notificaciones

Permite:

- Obtener notificaciones
    
- Contar notificaciones pendientes
    
- Insertar nuevas notificaciones
    

---

## 4. Autenticación

```PHP
$routes->post('/Ingresar', 'Login\LoginController::Login');
```

Esta ruta procesa las credenciales enviadas desde el formulario de inicio de sesión.

---

## 5. Administración de contraseñas

Incluye rutas para:

- Obtener usuarios
    
- Consultar áreas productoras
    
- Actualizar contraseñas
    

---

## 6. Gestión de áreas y roles

Permite asignar responsables a áreas productoras y gestionar los roles correspondientes.

---

## 7. Cortes parciales

Rutas para:

- Programar cortes
    
- Crear registros
    
- Editar información
    
- Eliminar registros
    

---

## 8. Inventario general

Este es uno de los módulos más extensos del sistema y contiene rutas para:

- Carga de inventario
    
- Consulta de inventario
    
- Modificación de registros
    
- Revisión de inventario
    
- Historial de registros
    

---

## 9. Generación de documentos

El módulo **Descarga de Oficios** permite:

- Obtener información del usuario
    
- Generar documentos PDF
    
- Guardar archivos generados



