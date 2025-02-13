## ¿Qué es Least Privilege?

El principio de privilegio mínimo (PoLP) es un concepto de seguridad de la información en el que se otorgan a los usuarios los niveles mínimos de acceso o permisos necesarios para realizar sus funciones laborales. También se considera una buena práctica de ciberseguridad y es un paso fundamental para proteger el acceso privilegiado a datos y activos de alto valor.

## ¿Por qué es importante el principio del mínimo privilegio (PoLP)?
Hoy en día, la mayoría de los ataques avanzados se basan en la explotación de credenciales privilegiadas. Al limitar los privilegios de superusuario y administrador, se reduce la superficie de ataque cibernético.
Dicho esto, me enfocaré en documentar diferentes procesos y técnicas que debemos implementar en un entorno corporativo para aplicar el principio de menor privilegio en ambientes Windows.

## Delegate Control Active Directory.

En Active Directory se tiene la capacidad de delegar controles a usuarios estándar o privilegiados de forma granular. En un entorno corporativo, el soporte técnico suele perder tiempo en atender tickets relacionados con el restablecimiento de contraseñas, el desbloqueo de usuarios y la creación de cuentas, entre otras tareas. Aunque estas actividades son simples, consumen mucho tiempo.

La delegación de control (Delegate Control) permite al área de seguridad de la información otorgar permisos específicos al personal de soporte técnico sin comprometer la seguridad. De esta manera, se evita la mala práctica de conceder accesos innecesarios, como la membresía en el grupo "Domain Admin" o privilegios de administrador local.

## Security (NTFS) VS Sharing (SMB).
Para muchos, la diferencia entre NTFS y SMB puede resultar confusa, por lo que es importante aclarar los conceptos de "Security vs. Sharing". Algo fundamental a tener en cuenta es que, al combinar ambos permisos, se genera un conjunto de reglas y, cuando se accede a los recursos desde la red, se aplica el permiso más restrictivo.


## Auditoría de archivos y carpetas.
Durante un tiempo investigué cómo configurar la auditoría del sistema de archivos y carpetas en Windows sin instalar soluciones de terceros. Después de muchas horas de análisis y con la intención de habilitar la auditoría solo en carpetas críticas, llegué a una conclusión: la mayoría de los procedimientos documentados en internet no diferenciaban entre carpetas críticas y el resto del sistema.
Como resultado, he desarrollado un script en PowerShell compuesto por dos archivos, que permite auditar únicamente las carpetas críticas sin afectar el rendimiento del sistema.


## ¿Qué es Active Directory Tier Model?
El modelo de niveles en Active Directory (Active Directory Tier Model) es una estructura en la que las autorizaciones de los usuarios están separadas por niveles de privilegio. Los usuarios solo pueden acceder a los recursos dentro del marco de permisos que se les han otorgado.

El beneficio más importante de este modelo es la protección de las cuentas administrativas del dominio o "cuentas confidenciales", reduciendo así el riesgo de accesos indebidos y ataques dirigidos contra usuarios con privilegios elevados.


## Creditos:
El contenido fue realizado por Jose Felix (Rookieヾ ⁿᵒᵛᵃᵗᵒ).
