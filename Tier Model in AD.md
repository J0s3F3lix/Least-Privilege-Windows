## Implementando Proteccion Tier 0 
### Contenido

- Introducción.
- ¿Qué es el modelo TIER?
- Los 3 Principio del TIER Model AD.
- Paso practico de implementacion.
- Recomendaciones.

## Introducción.

Debo decir que me apaciona la seguridad en Active Directory y uno de mis anelo siempre fue implementar Tier model en AD desde que lo escuche por primera en 2018 en una conferencia de seguridad, desde ese dia me enamore de este modelo, y por eso hare un resumen teorico practico de como asegurar el nivel 0 del model Tier en AD, el cual puedan implementar.

Tambien es bueno recodar que los ataques a Active Directory de los que se oye hablar hoy en día, independientemente de si se trata de ransomware o no, utilizan técnicas de robo de credenciales como factor clave para un compromiso exitoso. 

## ¿Qué es el modelo TIER?

El diseño del modelo de niveles es generalmente una estructura en la que las autorizaciones de usuario están separadas entre sí y los usuarios autorizados solo pueden acceder a los recursos de dominio dentro del marco de los permisos que se les otorgan. 
El nivel de seguridad más importante que aporta la estructura de niveles es proteger las cuentas de los administradores de dominio, que se denominan "cuentas confidenciales

Link Referencia: [Securing privileged access Enterprise access model - Privileged access | Microsoft Learn](https://learn.microsoft.com/en-us/security/privileged-access-workstations/privileged-access-access-model)

![image](https://www.piservices.fr/wp-content/uploads/2020/06/projet-tier-model-microsoft-scaled.jpg)

_Active Directory Tiered Administrative Model Control Restrictions (Image Credit: Microsoft)_
	
Tomando en cuenta lo ante dicho, en esta primera parte vamos a enfocanos en proteger el nivel 0 es el primer paso crítico hacia lo que debemo dar para la protección de Active Directory y la intencion mia es guiarle paso a paso en realizar este primer paso.

## Los 3 Principio del TIER Model AD:

Principio #1: Las credenciales de una cuenta de administrador o de servicio de nivel 0 no deben exponerse a sistemas de nivel inferior.

Principio #2: Las credenciales de nivel inferior pueden usar los servicios proporcionados por los niveles superiores, pero no al revés. 

Principio # 3: Cualquier sistema o cuenta de usuario que pueda administrar un nivel superior también debe ser miembro de ese nivel.

Ejemplo:
![image](https://i0.wp.com/www.cozumpark.com/wp-content/uploads/2022/10/Modified-Microsofts-administrative-three-tier-Model-2.png?w=850&quality=80&ssl=1)

_Active Directory Tiered Administrative Model Control Restrictions (Image Credit: Microsoft)_

## Protegiendo los activos del TIER 0

Para iniciar con los preparativos de proteccion utilizaremos un modelo de 3 niveles.

- **Nivel 0**: Activos que proporcionan control directo de la infraestructura de seguridad e identidad. El controlador de dominio es el activo mas critico del nivel 0. Pero tambien podemos tener en este nivel CA interno, herramientas de gestión de identidades y accesos (IAM) y hasta podermos llegar a tener un FileServer.

## Requerimientos para TIER 0

- RestrictedAdmin Required – Computer
- Restrict Workstation Logon
- Restrict Server Logon
## Implementacion TIER 0

Lo siguiente pasos son excenciales para limitar el uso de cuenta de nivel 0 (administradores y cuentas de servicio) a equipos de nivel 0.

Debemos de habilitar la proteccion de Kerberos (FAST) para controladores de dominio y todos los equipos del nivel 0.

No deben existir permisos a nivel de ACL o Delegate que tengan permisos confidenciales en el nivel raiz del dominio.

Crear una estructura en el AD de la siguiente manera:

Tier0 - Computer
Tier0 - Users

   
```
Advertencia!!!
Las restricciones de autenticación no tienen ninguna solución alternativa, lo que significa que los miembros de grupos con privilegios elevados, como el grupo Enterprise Admins o el grupo Domain Admins, están sujetos a las mismas restricciones que otros miembros del grupo Usuarios protegidos. Si todos los miembros de estos grupos se agregan al grupo Usuarios protegidos, es posible que se bloqueen todas esas cuentas. Nunca debe agregar todas las cuentas con privilegios elevados al grupo Usuarios protegidos hasta que haya probado exhaustivamente el impacto potencial.
```




### Recomendaciones Generales.

Parte del conenido de esta documentacion fue extraida y traducida al espanol de los siguientes investigadores, lo cuales me ayudaron en este viaje tan emocionante sobre la seguridad en Active Directory.

[Guidance about how to configure protected accounts | Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts#create-a-user-account-audit-for-authentication-policy-with-adac)
[Set Up Active Directory to Support Tiered Administration and Privileged Access Workstations - Petri IT Knowledgebase](https://petri.com/keep-active-directory-secure-using-privileged-access-workstations/)
[Active Directory Tiering Model Tasarımı Bölüm-1 - ÇözümPark (cozumpark.com)](https://www.cozumpark.com/active-directory-tiering-model-tasarimi-bolum-1/)
[How to Mitigate Privilege Escalation with the Tiered Access Model for Active Directory Security - Ravenswood Technology Group](https://www.ravenswoodtechnology.com/how-to-mitigate-privilege-escalation-with-the-tiered-access-model-for-active-directory-security/)
[Protecting Tier 0 the Modern Way - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/protecting-tier-0-the-modern-way/ba-p/4052851)

[Initially Isolate Tier 0 Assets with Group Policy to Start Administrative Tiering - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/initially-isolate-tier-0-assets-with-group-policy-to-start/ba-p/1184934)

[Microsoft Security Best Practices module: Privileged administration - Privileged access | Microsoft Learn](https://learn.microsoft.com/en-us/security/privileged-access-workstations/administration-videos-and-decks)

