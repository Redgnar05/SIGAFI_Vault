# Inventario de Tablas
A continuación se listan todas las tablas que forman parte de SIGAFI, tanto tablas catálogo como tablas de datos. Se recomienda acompañar la lectura con el diagrama .pdf para mejorar su entendimiento.
## Usuarios
Este grupo de tablas concentra toda la información relevante a los usuarios, como: nombres, apellidos, ubicación, tipo de usuario y la relación con áreas productoras.
- **SIGAFI_Usuario:** Tabla principal para la gestión de usuarios, se guarda el nombre del usuario y contraseña hasheada, así como la fecha de creación y si se encuentra activo, esta tabla es 
- **SIGAFI_DatosUsuario:** Tabla secundaria que extiende de SIGAFI_Usuario, se guardan los datos personales del usuario como nombre, apellidos grado y cargo.
- **SIGAFI_CatConjuntoUsuario:** Tabla catálogo con los posibles conjuntos en los que puede ubicarse un usuario, ej: Conjunto Norte, Cojunto Sur, Postgrado, Minería, etc.
- **SIGAFI_UbicacionUsuario:** Tabla secundaria que guarda la ubicación específica del usuario, como su cubículo o edificio.
- **SIGAFI_CatTipoUsuario:** Catálogo importante para la asignación de tipos de usuario a los usuarios, es através de este catálogo que el sistema identifica si puede o no acceder a un módulo, ejemplos de tipos de usuario: Responsable de Archivística, Revisor, Admin, etc.
- **SIGAFI_Usuario_TipoUsuario**: Tabla principal para la asignación de tipos de usuario, mediante esta tabla se le puede asignar a un usuario en específico un tipo de usuario, lo que le permitiría acceder a otras vistas y módulos, esta tabla es el puente que enlaza a los usuarios con el tipo que pueden ser.
- **SIGAFI_Usuario_AreaProductora:** Tabla más importante para la asignación de áreas con los usuarios, es gracias a esta tabla puente que un usuario puede tener múltiples áreas productoras asignadas y en caso de requerirse, cambiar el usuario que es responsable de un área. **Importante:** La asignación de áreas no se dá de forma directa con los datos del área (históricos) se hace mediante un abstracción (anclas) debido a que las áreas tienden a evolucionar, cambiar de división, cambiar de clave, etc (Más adelante se eplica este concepto).
- **SIGAFI_HistorialAccesos:** Tabla bitácora que registra los accesos al aplicativo por parte de los usuarios, sobre todo la fecha de acceso.
- **SIGAFI_Notifications:** Tabla que guarda las notificaciones levantadas por el usuario hacia el admin.
- **SIGAFI_NotificationLogs**: Tabla que guarda los logs de eventos importantes del sistema, como errores, bugs, negaciones de acceso, etc.

## Áreas productoras y divisiones
Este grupo de tablas concentra la información relevante a las áreas productoras de la facultad de ingeniería así como la división a la que pertenecen
**Importante:** Este grupo de tablas tienen un tipo de comportamiento particular (Ancla-Histórico), debido a que un usuario no puede tener directamente asignado una área productura de forma estática, ya que tanto las divisiones como las áreas productoras evolucionan con el tiempo, cambiando entre dependendencias, clave o nombre (caso contrario, se perdería trazabilidad de dichos cambios). Por ello, se tiene una tabla Ancla y una tabla histórico tanto para la división como para el área productora, en la que la tabla Ancla representa la entidad base o estática (sin datos específicos) y la tabla Historico representa la entidad secundaria o dinámica que evoluciona sobre el tiempo, para poder consultar en un momento dado la estructura actual de aréas y divisiones se utilizan las vistas *vw_Division_Actual* y *vw_AreaProductora_Actual*.
**Cuidar mucho la eficiencia en joins hacia estas tablas ya que según el caso puede parecer necesario hacer un cruce de otras tablas hacia la del ancla y la historica, pero la historica guarda todos los cambios de la entidad, por lo que puede llegar a fallar o generar comportamientos incorrectos.**

- **SIGAFI_DivisionAncla:** Entidad base que representa una división de la facultad de ingeniería (sin datos específicos). Ej: DIE, DIMEI, DCB, etc.
- **SIGAFI_DivisionHistorico:** Entidades secundarias que representan la evolución de una división en el tiempo, como los cambios de nombre. Ej: DIE -> DIE2, DCB -> DCByA
- **SIGAFI_AreaProductoraAncla:** Entidad base que representa una área productora de la facultad de ingeniería (sin datos específicos). Ej: Coordinación de planeación y desarrollo. 
- **SIGAFI_AreaProductoraHistorico:** Entidad secundaria que representa la evolución de una área productora en el tiempo, como los cambios de nombre o de clave. Ej: Clave 1.0.1 -> 12.5.6

## Catálogos ACA
Este grupo de tablas concentra la estructura de los códigos de clasificación, así como su sección, serie y subserie, proporcionados por el ACA para categorizar y ordenar los inventarios generales. Son los catálogos más importantes de todo el sistema ya que en torno a ellos se hacen validaciones de estructura al cargar nuevos registros en las tablas de inventario general.
- **SIGAFI_VigenciaCatACA:** Catálogo de vigencias de los nuevos códigos de clasificación, ya que anualmente el ACA UNAM proporciona los códigos de clasificación e instrumentos, que entran en vigencia a partir de un día en específico (no el el primero de enero), por lo que es importante contar con el inicio de la vigencia de un catálogo.
- **SIGAFI_CatSeccionACA:** Catálogo de secciones de los códigos de clasificación, usualmente son 16 y se dividen en 2 grupos según su función $Completar$ . Ej: 1C, 2C, 3C, 1S, 2S, etc.
- **SIGAFI_CatSerieSubserieACA:** Catálogo con las series y subseries de los códigos de clasificación. Ej: 1, 1.1, 2, 2.2, 2.12, etc.
- **SIGAFI_CatDescrSerieSubserieACA:** Catálogo con las descripciones de las series y subseries, este catálogo es una extensión del *SIGAFI_CatSerieSubserieACA*, con el objetivo de tener separada la descripción que en ocasiones es bastante extensa.
## Inventario General
Este grupo de tablas es el más importante de todo el aplicativo SIGAFI, ya que concentra todos los registros de inventarios generales en sus distintas etapas (cuando es registro nuevo, cuando ya es definitivo, cuando se está modificando y los históricos de sus modificaciones).
- **SIGAFI_NuevoInventarioGeneral:** Tabla con los registros de inventario general que están en proceso de nueva captura/alta, estos inventarios no se consideran cuando se produce el excel que se entrega al ACA.
- **SIGAFI_InventarioGeneral:** Tabla con los registros de inventario general definitivos, es decir, los que si se van a contemplar para producir el excel que se entrega al ACA.
  **Importante:** Esta tabla está desnormalizada, es decir, no guarda claves foráneas a las tablas de catálogos del aca y por lo mismo guarda la sección, serie y subserie sin referencias desde la BD
- **SIGAFI_ModificarInventarioGeneral**: Tabla con los registros de inventario general que están en proceso de modificación, estás modificaciones no son tomadas en cuenta para producir el excel que se entrega al ACA.
- **SIGAFI_InventarioGeneral_Historico:** Tabla que conserva el estado anterior que tenía un registro de inventario general, previo a la aceptación de nuevas modificaciones que se propagan a la tabla de SIGAFI_InventarioGeneral, esta tabla tiene más un propósito de auditoria en caso de mandar cambios incorrectos.

## Proceso de Revisión
Este conjunto de tablas son auxiliares al proceso de revisión y validación de registros de inventarios generales cuando se están modificando o cuando se dan de alta nuevos registros.
- **SIGAFI_CatTipoExpediente:** Catálogo con los tipos de expediente que puede tener un inventario general. Ej: Mixto, Físico o dígital.
- **SIGAFI_CatStatusInventarioGeneral:** Catálogo con los estatus que puede tener un registro de inventario general según el proceso en el que se encuentre.
  Del 0 al 3 corresponden a estados que participan cuando se da de alta un nuevo registro en la tabla de SIGAFI_NuevoInventarioGeneral, del 4 al 7 corresponden a estados que participan cuando se está modificando un registro de inventario general en la tabla SIGAFI_ModificarInventarioGeneral.
- **SIGAFI_CatTextosProhibidos:** #

## Auxiliares al Sistema
Estas tablas son tablas que no tienen una participación tan explícita con otras tablas y cuyo propósito es apoyar en otros procesos:
- **SIGAFI_CortesParciales:** #
- **SIGAFI_CortesAnuales:** #
- **SIGAFI_ErrorLogs:** #

---

### Vistas encontradas: 2

```
vw_Division_Actual
vw_AreaProductora_Actual
```


==Hay dos tablas que no se logran ver en el diagrama:==

```
SIGAFI_CatConjuntoUsuario
SIGAFI_CatTextosProhibidos
```

---
---

### SIGAFI_CatTextosProhibidos

SIGAFI_CatTextosProhibidos es una tabla aislada, la definición es:

```SQL
CREATE TABLE SIGAFI_CatTextosProhibidos (
	ID INT AUTO_INCREMENT PRIMARY KEY,    
	TextoProhibido VARCHAR(255) NOT NULL,    
	Sustituto VARCHAR(255) NOT NULL,    
	IsActive BOOLEAN DEFAULT TRUE,     
	CreatedAt DATETIME DEFAULT CURRENT_TIMESTAMP);
```

No tiene:

```
FOREIGN KEY
REFERENCES
```

---
---

### SIGAFI_DatosUsuario

La tabla original:

```SQL
CREATE TABLE SIGAFI_DatosUsuario (    
	ID_Usuario INT PRIMARY KEY,    
	Nombre_Responsable VARCHAR(50) NOT NULL,    
	ApePaterno VARCHAR(40) NOT NULL,    
	ApeMaterno VARCHAR(40) NOT NULL,    
	GradoAcademico VARCHAR(30) NOT NULL,    
	Cargo VARCHAR(100) NOT NULL,    
	ID_Conjunto_FK TINYINT NULL,    
	FOREIGN KEY (ID_Usuario)        
		REFERENCES SIGAFI_Usuario(ID_Usuario)        
		ON DELETE CASCADE);
```

Se altero la tabla:

```SQL
ALTER TABLE sigafi_datosusuario
ADD CONSTRAINT fk_conjunto_usuario
FOREIGN KEY (ID_Conjunto_FK)
REFERENCES SIGAFI_CatConjuntoUsuario(ID_CatConjuntoUsuario)
ON DELETE SET NULL;
```

El modelo propuesto es el siguiente:

```
SIGAFI_CatConjuntoUsuario
            │
            │ 1:N
            ▼
SIGAFI_DatosUsuario
            │
            │ 1:1            
            ▼
    SIGAFI_Usuario
```

---
---
## Actualización del Daigrama en Draw.io

La tabla **SIGAFI_CatConjuntoUsuario**  sí participa en relaciones, y queda dentro del bloque **Usuarios**.
#### Estructura

```
SIGAFI_CatConjuntoUsuario
---------------------------
PK  ID_CatConjuntoUsuario    

	Is_Active    
	Created_At    
	Nombre_Conjunto
```

Se actualizo **SIGAFI_DatosUsuario**, según el SQL actual debe quedar:

#### Estructura

```
SIGAFI_DatosUsuario
---------------------------
PK/FK ID_Usuario

	  Nombre_Responsable    
	  ApePaterno    
	  ApeMaterno    
	  GradoAcademico    
	  Cargo
FK    ID_Conjunto_FK
```

La tabla **SIGAFI_CatTextosProhibidos** actualmente no tiene relaciones.

La pondré en un nuevo bloque sin etiquetar .
#### Estructura

```
SIGAFI_CatTextosProhibidos

PK  ID    
	TextoProhibido    
	Sustituto    
	IsActive    
	CreatedAt
```

 Relaciones: Ninguna.

