## Security (NTFS) VS Sharing (SMB).
## Temas a tratar
- Introducción.
- Definición de Permisos Security (NTFS).
- Definición de Permisos Sharing (SMB).
- Ejemplo.


## Introducción.

Para muchos puede llegar a ser confuso para otro no, pero no está de más aclarar las diferencias de permiso NTFS y SMB.
en otra palabra (Security vs Sharing). Algo a tener bien presente es que al combinar ambos permisos se convierten en un conjunto de permisos
y cuando se accede desde la red, aplica el más restrictivo.

## Definición de Permisos Security (NTFS).
```
Full Control = Acceso total, esto incluye administrar permisos.
Modify = Acceso solo a Modificar
Read & Execute = Acceso a leer y ejecutar
List Folder contents = solo a listar el contenido, ósea es decir solo ver que tiene la carpeta.
Read = Solo lectura, puede ver el contenido y leer el contenido de un archivo existente pero no hacer más nada.
Write = Solo escritura, puede tomar. Por supuesto, incluye implica el uso del permiso para lectura.
Special Permissions = es como modificar un permiso, para un caso en específico.
```

## Definición de Permisos Sharing (SMB).

```
Full Control = Acceso total.
Change = Acceso a Modificar.
Read = Solo lectura, puede ver el contenido y leer el contenido de un archivo existente pero no hacer más nada.
```
### EJEMPLO 1

En una carpeta compartida (A) accesado via red tenemos lo siguiente permisos
```
Security NTFS = Read
Sharing SMB = Change
```
Cualquiera diría que, al acceder vía RED, tendríamos permiso de `Change`, pero no es así, debido a que `Security NTFS` tiene permiso de `Read`. y como la regla dice: Se aplica el más
restrictivo de los dos permiso. Entonces solo tendremos acceso de lectura para este ejemplo.

### EJEMPLO 2
```
Security NTFS = Full Control
Sharing SMB = Change
```

En este ejemplo tendremos el privilegio `Change`, aunque `Security NTFS` tenga “Full Control” por que la regla dice: Se aplica el más
restrictivo de los dos permiso.


## Creditos:
El contenido fue realizado por Jose Felix (Rookieヾ ⁿᵒᵛᵃᵗᵒ) también en compañía de Dayner Rolando Felix.
