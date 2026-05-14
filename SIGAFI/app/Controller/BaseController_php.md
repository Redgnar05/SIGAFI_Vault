
## Descripción de `BaseController.php`

El archivo `BaseController.php` define una **clase base abstracta** que es utilizada por todos los controladores del sistema SIGAFI-APP. Su función principal es **centralizar configuraciones y lógica común**, permitiendo que los demás controladores hereden estas funcionalidades sin necesidad de reimplementarlas.

Entre sus responsabilidades principales se encuentran:

- Inicializar servicios globales como la sesión
- Proveer métodos reutilizables (sanitización de datos, validación de sesión)
- Estandarizar la información enviada a las vistas
- Facilitar el mantenimiento y la escalabilidad del sistema

---

## Documentación técnica del código

### Definición de la clase

```
abstract class BaseController extends Controller
```

La [[clase es abstracta]], lo que implica que no puede ser instanciada directamente. Está diseñada para ser heredada por otros controladores, asegurando que todos compartan una base común de comportamiento.

---

### Propiedades principales

```
protected $request;
```

Almacena la instancia de la solicitud HTTP o CLI. Permite acceder a datos enviados por el cliente, como parámetros GET o POST.

```
protected $helpers = [];
```

Define un arreglo de helpers que se cargarán automáticamente en todos los controladores que extiendan esta clase.

```
protected $session;
```

Contiene la instancia del servicio de sesión. Se declara explícitamente para cumplir con las restricciones de PHP 8.2 y evitar propiedades dinámicas.

---

### Inicialización del controlador

```
public function initController(RequestInterface $request, ResponseInterface $response, LoggerInterface $logger)
```

Este método se ejecuta automáticamente al crear una instancia de cualquier controlador que herede de `BaseController`.

```
parent::initController($request, $response, $logger);$this->session = \Config\Services::session();
```

Primero se llama al método padre para mantener el flujo interno del framework. Posteriormente, se inicializa el servicio de sesión, dejándolo disponible para toda la aplicación.

> [!important]  
> Este método es el punto ideal para cargar servicios globales como sesiones, modelos o librerías compartidas.

---

### Método `sanitizeInput()`

```
public function sanitizeInput($varNames)
```

Este método recibe un arreglo con nombres de variables provenientes de una petición POST y devuelve sus valores sanitizados.

```
foreach ($varNames as $varName) {    $sanitizedData[$varName] = filter_input(INPUT_POST, $varName, FILTER_SANITIZE_SPECIAL_CHARS);}
```

Se utiliza `filter_input` con `FILTER_SANITIZE_SPECIAL_CHARS` para evitar la ejecución de código malicioso, especialmente ataques XSS.

```
return $sanitizedData;
```

Devuelve un arreglo con los datos limpios.

> [!warning]  
> La sanitización de entradas es fundamental para prevenir vulnerabilidades de seguridad en aplicaciones web.

---

### Método `GetIndexViewData()`

```
protected function GetIndexViewData(string $title): array
```

Este método construye un arreglo con datos que serán enviados a las vistas, principalmente en el método `index` de los controladores.

```
$viewData = ['title' => $title];
```

Se inicializa el arreglo con el título de la página.

```
if (!$this->IsUserLogged()) {    $viewData['isLogged'] = false;    log_message('info', 'User is not logged in.');    return $viewData;}
```

Si el usuario no está autenticado:

- Se marca como no logueado
- Se registra un mensaje en el log
- Se retorna el arreglo sin más datos

```
$viewData['isLogged'] = true;$viewData['ID_Usuario'] = session()->get('ID_Usuario');$viewData['ID_CatTipoUsuario'] = session()->get('ID_CatTipoUsuario');$viewData['Nombre_TipoUsuario'] = session()->get('Nombre_TipoUsuario');$viewData['Nombre_Perfil'] = session()->get('Nombre_Perfil');
```

Si el usuario está autenticado, se agregan datos relevantes de la sesión.

Este enfoque permite que todas las vistas tengan acceso a información del usuario sin repetir código en cada controlador.

---

### Método `IsUserLogged()`

```
protected function IsUserLogged(): bool
```

Verifica si existe una sesión activa en el sistema.

```
return (bool)Session()->get('ID_Usuario');
```

Retorna `true` si el identificador del usuario está presente en la sesión, o `false` en caso contrario.

> [!important]  
> Este método encapsula la lógica de autenticación, facilitando su reutilización y mantenimiento.

---

