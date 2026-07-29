
---

- [x]  Catálogos ACA 
- [x] Áreas
- [x] Usuarios
- [x] Inventario
- [ ] Revisión
- [ ] Histórico
- [ ] Tablas aisladas

---

## Metodología propuesta:

Tomar una tabla, encontrar sus PK y FK en SQL, y luego validar que el Drawio represente correctamente la relación y cardinalidad.


---

La idea es responder para cada relación:

```
¿La FK existe en SQL?
↓
¿Está dibujada en Drawio?
↓
¿Apunta a la tabla correcta?
↓
¿La cardinalidad es correcta?
```

---

### Grupo 1. Catálogos ACA

Según el SQL existen estas FK:

```SQL
FOREIGN KEY (Anio)
REFERENCES SIGAFI_VigenciaCatACA(Anio)

FOREIGN KEY (ID_CatSeccion)
REFERENCES SIGAFI_CatSeccionACA(ID_CatSeccion)

FOREIGN KEY (ID_CatSerieSubserie)
REFERENCES SIGAFI_CatSerieSubserieACA(ID_CatSerieSubserie)
```

Por lo tanto se verifico la siguiente cardinalidad:

```
SIGAFI_VigenciaCatACA
        |        
        | 1:N        
        |
SIGAFI_CatSeccionACA
        |        
        | 1:N        
        |
SIGAFI_CatSerieSubserieACA
        |        
        | 1:N        
        |
SIGAFI_CatDescrSerieSubserieACA
```

---

### Grupo 2. Áreas

#### Paso 1. Localizar los `CREATE TABLE` por medio del SQL en VS Code

```SQL
/* ÁREAS PRODUCTORAS Y DIVISIONES DE LA FACULTAD */

CREATE TABLE SIGAFI_DivisionAncla (

ID_DivisionAncla INT AUTO_INCREMENT PRIMARY KEY,

IsActive BOOLEAN NOT NULL DEFAULT TRUE

);

  

CREATE TABLE SIGAFI_DivisionHistorico (

ID_DivisionHistorico INT AUTO_INCREMENT PRIMARY KEY,

ID_DivisionAncla INT NOT NULL,

Nombre_Division VARCHAR(150) NOT NULL,

Acronimo_Division VARCHAR(20) NOT NULL,

Motivo_Cambio VARCHAR(100) NOT NULL,

Created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,

FOREIGN KEY (ID_DivisionAncla) REFERENCES SIGAFI_DivisionAncla(ID_DivisionAncla) ON DELETE NO ACTION

);

CREATE INDEX idx_ID_DivisionAncla_Created_at ON SIGAFI_DivisionHistorico (ID_DivisionAncla, Created_at DESC);



CREATE TABLE SIGAFI_AreaProductoraAncla (

ID_AreaProductoraAncla INT AUTO_INCREMENT PRIMARY KEY,

ID_AreaProductoraAnterior INT NULL DEFAULT NULL,

IsActive BOOLEAN NOT NULL DEFAULT TRUE,

FOREIGN KEY (ID_AreaProductoraAnterior) REFERENCES SIGAFI_AreaProductoraAncla(ID_AreaProductoraAncla)

);

  

CREATE TABLE SIGAFI_AreaProductoraHistorico (

ID_AreaProductoraHistorico INT AUTO_INCREMENT PRIMARY KEY,

ID_AreaProductoraAncla INT NOT NULL,

ID_DivisionAncla INT NOT NULL,

Nombre_AreaProductora VARCHAR(200) NOT NULL,

Clave_AreaProductora VARCHAR(15) NOT NULL,

Motivo_Cambio VARCHAR(100) NOT NULL,

Created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,

FOREIGN KEY (ID_AreaProductoraAncla) REFERENCES SIGAFI_AreaProductoraAncla(ID_AreaProductoraAncla) ON DELETE NO ACTION,

FOREIGN KEY (ID_DivisionAncla) REFERENCES SIGAFI_DivisionAncla(ID_DivisionAncla) ON DELETE NO ACTION

);

CREATE INDEX idx_ID_AreaProductoraAncla_Created_at ON SIGAFI_AreaProductoraHistorico (ID_AreaProductoraAncla, Created_at DESC);
```

#### Paso 2. Identificamos PK y FK por tabla 

##### 1. SIGAFI_DivisionAncla

```SQL
CREATE TABLE SIGAFI_DivisionAncla (
    ID_DivisionAncla INT AUTO_INCREMENT PRIMARY KEY,    
    IsActive BOOLEAN NOT NULL DEFAULT TRUE
);
```

| Campo            | Tipo |
| ---------------- | ---- |
| ID_DivisionAncla | PK   |
Relaciones: No tiene FK.

##### 2. SIGAFI_DivisionHistorico

```SQL
ID_DivisionHistorico INT AUTO_INCREMENT PRIMARY KEY,
ID_DivisionAncla INT NOT NULL,

FOREIGN KEY (ID_DivisionAncla)
REFERENCES SIGAFI_DivisionAncla(ID_DivisionAncla)
```

| Campo                | Tipo |
| -------------------- | ---- |
| ID_DivisionHistorico | PK   |
| ID_DivisionAncla     | FK   |
|                      |      |
###### 3. SIGAFI_AreaProductoraAncla

```SQL
CREATE TABLE SIGAFI_AreaProductoraAncla (
	ID_AreaProductoraAncla INT AUTO_INCREMENT PRIMARY KEY,   
	ID_AreaProductoraAnterior INT NULL,    
	
	FOREIGN KEY (ID_AreaProductoraAnterior)
        REFERENCES SIGAFI_AreaProductoraAncla(ID_AreaProductoraAncla)
);
```

La tabla se referencia a sí misma. Esto modela renombramientos o sustituciones.

Una área anterior puede dar origen a varias áreas nuevas.
- Es una relación recursiva.

Se verifica que:

```SQL
FK ID_AreaProductoraAnterior
```

Si existe.

##### 4. SIGAFI_AreaProductoraHistorico

```SQL
ID_AreaProductoraHistorico INT PRIMARY KEY,
ID_AreaProductoraAncla INT NOT NULL,
ID_DivisionAncla INT NOT NULL,

FOREIGN KEY (ID_AreaProductoraAncla)
REFERENCES SIGAFI_AreaProductoraAncla

FOREIGN KEY (ID_DivisionAncla)
REFERENCES SIGAFI_DivisionAncla
```

Aquí hay dos relaciones.

**Relación A**

```
SIGAFI_AreaProductoraAncla
                1
                |                
                |                
                N
SIGAFI_AreaProductoraHistorico
```

Suponiendo que una misma área puede tener múltiples versiones históricas.

**Relación B**

```
SIGAFI_DivisionAncla
          1          
          |          
          |          
          N
SIGAFI_AreaProductoraHistorico
```

Suponiendo que varias áreas pueden pertenecer a la misma división.

#### Paso 3. Validar el Diagrama en Draw

**Relación 1**

```
SIGAFI_DivisionAncla 
		|1
        |            
        |N
SIGAFI_DivisionHistorico
```

**Relación 2**

```
SIGAFI_DivisionAncla
		|1
        |            
        |N
SIGAFI_AreaProductoraHistorico
```

**Relación 3**

```
SIGAFI_AreaProductoraAncla
		|1
        |            
        |N
SIGAFI_AreaProductoraHistorico
```

**Relación 4 (recursiva)**

```
SIGAFI_AreaProductoraAncla
		|1
        |            
        |N
SIGAFI_AreaProductoraAncla
```

mediante:

```
ID_AreaProductoraAnterior
```


---
### Grupo 3. Usuarios
#### 3.1 DatosUsuario

Debe existir:

```
SIGAFI_Usuario
      |
      | 1:1
      |
SIGAFI_DatosUsuario
```

porque:

```
ID_Usuario INT PRIMARY KEY

FOREIGN KEY(ID_Usuario)
REFERENCES SIGAFI_Usuario(ID_Usuario)
```

#### 3.2 UbicacionUsuario

Debe existir:

```
SIGAFI_Usuario
      |      
      | 1:1      
      |
SIGAFI_UbicacionUsuario
```

#### 3.3 HistorialAccesos

Debe existir:

```
SIGAFI_Usuario
      |      
      | 1:N      
      |
SIGAFI_HistorialAccesos
```

#### 3.4 Notifications

Debe existir:

```
SIGAFI_Usuario
      |      
      | 1:N      
      |
SIGAFI_Notifications
```

#### 3.5 NotificationLogs

Debe existir:

```
SIGAFI_Notifications
      |      
      | 1:N      
      |
SIGAFI_NotificationLogs
```

#### 3.6 Usuario_TipoUsuario

Debe existir:

```
SIGAFI_Usuario
        |
        | 1:N        
        |
SIGAFI_Usuario_TipoUsuario
        |
        | N:1        
        |
SIGAFI_CatTipoUsuario
```

Es una tabla puente.

#### 3.7 Usuario_AreaProductora

Debe existir:

```
SIGAFI_Usuario
        |
        |
SIGAFI_Usuario_AreaProductora
        |        
        |
SIGAFI_AreaProductoraAncla
```

También es tabla puente.

#### 3.8 CatConjuntoUsuario

Nueva relación.

Debe existir:

```
SIGAFI_CatConjuntoUsuario
             |             
             | 1:N             
             |
	SIGAFI_DatosUsuario
```

---

### Grupo 4. Inventario

Se verificó:

```
FOREIGN KEY(ID_AreaProductoraAncla)
FOREIGN KEY(ID_Subserie)
FOREIGN KEY(ID_TipoExpediente)
```

Por lo tanto:

```
SIGAFI_AreaProductoraAncla
            |            
            |
SIGAFI_InventarioGeneral
            |            
            |
SIGAFI_CatSerieSubserieACA

SIGAFI_CatTipoExpediente            
            |            
            |
SIGAFI_InventarioGeneral
```

---

### Grupo 5. Revisión


---

### Grupo 6. Histórico


---

### Grupo 7. Tablas aisladas


---


