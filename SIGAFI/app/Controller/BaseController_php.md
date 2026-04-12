
# **BaseController.php**

El archivo `BaseController.php`, ubicado en el espacio de nombres `App\Controllers`, define una clase abstracta que extiende de `CodeIgniter\Controller` y constituye la base estructural de todos los controladores del sistema SIGAFI-APP. Su finalidad es centralizar la configuración inicial, la carga de servicios y la implementación de funciones comunes, permitiendo que los controladores derivados mantengan una estructura homogénea y reutilizable dentro de la aplicación.

> [!abstract] Resumen  
> SIGAFI es un sistema de gestión institucional.

> [!info] Información  
> SIGAFI está desarrollado con CodeIgniter y PHP.

Desde el punto de vista arquitectónico, este controlador es fundamental, ya que establece los elementos base que serán utilizados en todo el sistema. Entre sus atributos principales se encuentra `$request`, que representa la solicitud HTTP actual, permitiendo acceder a los datos enviados por el cliente. Asimismo, el arreglo `$helpers` define los helpers que se cargarán automáticamente, facilitando el uso de funciones auxiliares en los controladores hijos. Por otro lado, la propiedad `$session` permite gestionar la sesión del usuario, lo cual es esencial para mantener información persistente entre peticiones.

> [!important] Importante  
> La carpeta app/ contiene toda la lógica principal.

> ⚠️ **Callout importante:**  
> La gestión de sesiones mediante `$session` es esencial para mantener el estado del usuario, incluyendo autenticación, roles y permisos dentro del sistema.

El método `initController` se ejecuta automáticamente en cada solicitud y tiene como objetivo inicializar el controlador base. En su implementación, primero se invoca el método del padre (`parent::initController`) para asegurar la correcta configuración del framework, y posteriormente se inicializa el servicio de sesión mediante `\Config\Services::session()`. Este comportamiento permite que todos los controladores que hereden de esta clase tengan acceso inmediato a la sesión del usuario.

> ⚠️ **Callout importante:**  
> Este método actúa como un mecanismo similar a un _middleware global_, ejecutándose antes de cualquier lógica en los controladores derivados.

En relación con la seguridad de los datos, el método `sanitizeInput` permite limpiar variables recibidas mediante el método POST. Este proceso se realiza aplicando el filtro `FILTER_SANITIZE_SPECIAL_CHARS`, con el objetivo de eliminar caracteres potencialmente peligrosos y devolver un arreglo con datos seguros para su uso posterior.

> [!danger] Riesgo  
> Mala configuración puede causar fallos de seguridad.

> ⚠️ **Callout importante (SEGURIDAD):**  
> La sanitización de datos ayuda a prevenir ataques como Cross-Site Scripting (XSS), protegiendo la integridad del sistema.

Por otro lado, el método `GetIndexViewData` se encarga de preparar la información necesaria para las vistas, especialmente en métodos tipo `index`. Este método recibe el título de la página y construye un arreglo base con dicha información. Posteriormente, verifica si el usuario está autenticado mediante el método `IsUserLogged`. Si no lo está, se establece la variable `isLogged` como falsa y se registra un mensaje en el sistema de logs; en caso contrario, se agregan datos relevantes de la sesión, como el identificador del usuario, el tipo de usuario y la información del perfil.

> ⚠️ **Callout importante:**  
> Este método centraliza la información enviada a las vistas, evitando duplicidad de código y asegurando consistencia en la interfaz del sistema.

El método `IsUserLogged` permite verificar si existe una sesión activa, evaluando la presencia del identificador del usuario en la sesión. Retorna un valor booleano que indica si el usuario se encuentra autenticado, siendo un componente clave para el control de acceso dentro del sistema.

> ⚠️ **Callout importante (SEGURIDAD):**  
> Este método es esencial para restringir funcionalidades únicamente a usuarios autenticados.

En conjunto, el `BaseController` establece una base sólida para la arquitectura de SIGAFI-APP, proporcionando mecanismos fundamentales como la gestión de sesiones, la sanitización de entradas, la validación de autenticación y la estandarización de datos para vistas. Su correcta implementación garantiza consistencia, seguridad y mantenibilidad en el desarrollo del sistema.

> [!warning] ⚠️ Advertencia  
> No modifiques public/index.php sin respaldo.

> 🚨 **Callout final (MUY IMPORTANTE):**  
> Una implementación incorrecta o modificaciones en este controlador pueden provocar errores globales, pérdida de sesiones o vulnerabilidades de seguridad en todo el sistema.

---

