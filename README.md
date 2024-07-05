## ¿Que es Least Privilege?

El principio de privilegio mínimo (PoLP) se refiere a un concepto de seguridad de la información en el que se otorga a un usuario los niveles mínimos de acceso, o permisos, necesarios para realizar sus funciones laborales.Tambien se considera ampliamente como una buena práctica de ciberseguridad y es un paso fundamental para proteger el acceso privilegiado a datos y activos de alto valor. 

## ¿Por qué es importante el principio del mínimo privilegio (PoLP)?
Hoy en día, la mayoría de los ataques avanzados se basan en la explotación de credenciales privilegiadas. Al limitar los privilegios de superusuario y administrador, Reduce la superficie de ataque cibernético. 
Dicho todo esto, me enfocare he ir documentando diferente proceso y tecnica que debemos implementar en un entorno corporativo de cara a aplicar el menor privilegio posible en ambiente windows.

## Delegate Control Active Directory.

En Active Directory tiene la capacidad delegar controles a usuario estándar o usuario privilegiado de forma muy granular. En un entorno corporativo, un soporte técnico dedica tiempo improductivo a asistir a tickets relacionados con el restablecimiento de contraseñas, desbloquear usuarios, crear usuarios etc. Aunque son tareas simples, estas actividades consumen mucho tiempo. La delegación de control (Delegate Control), ayuda al área de seguridad de la información a permitir que este personal de soporte técnico pueda cumplir con este tipo de tareas, sin comprometer la seguridad. Agregándole privilegio innecesario por desconocimiento. Y al mismo tiempo erradicar esa mala práctica, donde se dan los accesos (Domain Admin u/o Administrador local).


## Security (NTFS) VS Sharing (SMB).
Para muchos puede llegar a ser confuso para otro nos, pero no está de más aclarar las diferencias de permiso NTFS y SMB. en otra palabra (Security vs Sharing). Algo a tener bien presente es que al combinar ambos permisos se convierten en un conjunto de permisos y cuando se accede desde la red, aplica el más restrictivo.


## Auditoría de archivos y carpetas.
Durante un tiempo estuve investigando cómo configurar la auditoría del sistema de archivos y carpetas en Windows sin instalar ninguna solución de tercero y de carpetas críticas. luego de muchas horas de investigación y con una curiosidad que me invadía debido a deseaba habilitar la auditoria, pero a carpeta críticas y no todas las carpetas de Windows. como muchos procesos en internet tenía documentados.
Mi conclusión fue la siguiente: He construido un script de PowerShell que se compone de dos archivos.
