
---

- [x]  Catálogos ACA correcto
- [ ] Áreas correcto
- [x] Usuarios correcto
- [x] Inventario correcto
- [ ] Revisión correcto
- [ ] Histórico correcto
- [ ] Tablas aisladas correcto

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


