20/06/26

Tablas encontradas: 28
# Inventario de Tablas

## Usuarios
- SIGAFI_Usuario
- SIGAFI_DatosUsuario
- SIGAFI_CatConjuntoUsuario
- SIGAFI_UbicacionUsuario
- SIGAFI_CatTipoUsuario
- SIGAFI_Usuario_TipoUsuario
- SIGAFI_Usuario_AreaProductora
- SIGAFI_HistorialAccesos
- SIGAFI_Notifications
- SIGAFI_NotificationLogs

## Áreas
- SIGAFI_DivisionAncla
- SIGAFI_DivisionHistorico
- SIGAFI_AreaProductoraAncla
- SIGAFI_AreaProductoraHistorico

## Catálogos ACA
- SIGAFI_VigenciaCatACA
- SIGAFI_CatSeccionACA
- SIGAFI_CatSerieSubserieACA
- SIGAFI_CatDescrSerieSubserieACA

## Inventario
- SIGAFI_InventarioGeneral
- SIGAFI_ModificarInventarioGeneral
- SIGAFI_InventarioGeneral_Historico

## Revisión
- SIGAFI_NuevoInventarioGeneral
- SIGAFI_CatTipoExpediente
- SIGAFI_CatStatusInventarioGeneral

## Sistema
- SIGAFI_CortesParciales
- SIGAFI_CortesAnuales
- SIGAFI_ErrorLogs
- SIGAFI_CatTextosProhibidos

---

### Vistas encontradas: 2

```
vw_Division_Actual
vw_AreaProductora_Actual
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

