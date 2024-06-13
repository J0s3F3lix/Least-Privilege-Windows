## Delegate Control Active Directory .
## Contenido
- Introducción.
- Delegate control mejores practicas.
- Delegate control mas comunes.
- Ejemplo.
- Recomendaciones Generales.

## Introduccion.

```
En Active Directory tiene la capacidad delegar controles a usuario estándar o usuario privilegiado
de forma muy granular. En un entorno corporativo, un soporte técnico dedica tiempo improductivo a asistir 
a tickets relacionados con el restablecimiento de contraseñas, desbloquear usuarios, 
crear usuarios etc. Aunque son tareas simples, estas actividades consumen mucho tiempo.

La delegación de control (Delegate Control), ayuda al área de seguridad de la información 
a permitir que este personal de soporte técnico pueda cumplir con este tipo de tareas, 
sin comprometer la seguridad. Agregándole privilegio innecesario por desconocimiento.
Y al mismo tiempo erradicar esa mala práctica, donde se dan los accesos (Domain Admin u/o Administrador local).

```

## Delegate control mejores practicas

```
La delegación de permisos en Active Directory se realiza mediante unidades organizativas (OU Organization Unit), 
por lo que es fundamental tener un buen diseño de OU. El diseño de la unidad organizativa será diferente 
para cada organización, pero un diseño simple es poner todos los recursos similares en su propia unidad organizativa.
```

## Delegate control mas comunes.


|TIPO |TIPO DE PERMISO|
|---|---|
|User Account |Create,Move,Password Reset,Disable|
|Computers |Create,Move,Disable|
|Group| Create,Move,Disable|
|Organization Unit|Create,Move,Delete|

### EJEMPLO 1


### Recomendaciones Generales.

>Cuando hagamos un delegar control, favor NO utilizar grupos de AD por default. Ejemplo
No use: "Backup Operators" o "DHCP Administrator"
Estos grupos de AD tienen permisos especiales que pueden otorgar a los usuarios más privilegios de los necesarios.

