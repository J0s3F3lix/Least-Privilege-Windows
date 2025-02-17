# 🔐 Implementando Protección Tier 0

## 📌 Contenido
- [Introducción](#introducción)
- [¿Qué es Active Directory Tier Model?](#qué-es-active-directory-tier-model)
- [Principios del Active Directory Tier Model](#principios-del-active-directory-tier-model)
- [Protección de los Activos del Tier 0](#protección-de-los-activos-del-tier-0)
- [Requerimientos para Tier 0](#requerimientos-para-tier-0)
- [Implementación de Tier 0](#implementación-de-tier-0)
- [Recomendaciones Generales](#recomendaciones-generales)

---

## 📖 Introducción
Me apasiona la ciberseguridad en entornos Windows, especialmente en el ámbito corporativo. Uno de los temas que más me ha interesado es el **Active Directory Tier Model**. En este documento, presentaré un resumen detallado de este modelo, con un enfoque especial en la protección del **Tier 0**, el primer paso crítico en la seguridad de Active Directory.

---

## 🏛️ ¿Qué es Active Directory Tier Model?
El **Active Directory Tier Model** es una estructura que separa las autorizaciones de usuario en diferentes niveles, permitiendo que cada usuario acceda solo a los recursos dentro del marco de los permisos que se le otorgan.

📌 **Objetivo principal:** Proteger las cuentas administrativas y los activos críticos dentro de Active Directory.

📖 **Referencia:** [Securing Privileged Access - Microsoft Learn](https://learn.microsoft.com/en-us/security/privileged-access-workstations/privileged-access-access-model)

![Modelo de Niveles AD](https://www.piservices.fr/wp-content/uploads/2020/06/projet-tier-model-microsoft-scaled.jpg)

---

## 🔑 Principios del Active Directory Tier Model

1️⃣ **Las credenciales de una cuenta de administrador o de servicio de nivel 0 no deben exponerse a sistemas de nivel inferior.**
2️⃣ **Las credenciales de nivel inferior pueden usar los servicios de los niveles superiores, pero no al revés.**
3️⃣ **Cualquier sistema o cuenta de usuario que pueda administrar un nivel superior también debe ser miembro de ese nivel.**

📌 **Ejemplo de Segmentación:**
![Segmentación de Niveles](https://i0.wp.com/www.cozumpark.com/wp-content/uploads/2022/10/Modified-Microsofts-administrative-three-tier-Model-2.png?w=850&quality=80&ssl=1)

---

## 🏰 Protección de los Activos del Tier 0

El **Tier 0** engloba los activos que proporcionan control directo sobre la infraestructura de seguridad e identidad. 

🎯 **Ejemplos de activos en Tier 0:**
- Controladores de dominio (Domain Controllers).
- Servidores de certificación interna (CA Servers).
- Herramientas de gestión de identidad y acceso (IAM).
- File Servers críticos.

---

## ⚙️ Requerimientos para Tier 0
✔️ **RestrictedAdmin Required – Computer.**
✔️ **Restrict Workstation Logon.**
✔️ **Restrict Server Logon.**

---

## 🛠️ Implementación de Tier 0
Para limitar el uso de cuentas de nivel 0 a equipos de nivel 0, se deben seguir los siguientes pasos:

1️⃣ **Habilitar la protección de Kerberos (FAST)** en controladores de dominio y equipos Tier 0.
2️⃣ **Eliminar permisos ACL o Delegate** que otorguen permisos confidenciales en la raíz del dominio.
3️⃣ **Crear una estructura organizada en Active Directory:**
   - `Tier0 - Computer`
   - `Tier0 - Users`

⚠️ **Advertencia:** Las restricciones de autenticación no tienen soluciones alternativas. Si todos los administradores de dominio se agregan a usuarios protegidos sin pruebas previas, podrían bloquearse todas las cuentas con privilegios elevados.

---

## ✅ Recomendaciones Generales
Parte del contenido ha sido extraído y traducido de investigaciones especializadas en seguridad de Active Directory.

📖 **Referencias clave:**
- [Configurar cuentas protegidas - Microsoft Learn](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/how-to-configure-protected-accounts#create-a-user-account-audit-for-authentication-policy-with-adac)
- [Configuración de Tiering en AD - Petri IT Knowledgebase](https://petri.com/keep-active-directory-secure-using-privileged-access-workstations/)
- [Diseño de Active Directory Tiering - ÇözümPark](https://www.cozumpark.com/active-directory-tiering-model-tasarimi-bolum-1/)
- [Mitigación de Privilege Escalation - Ravenswood Technology](https://www.ravenswoodtechnology.com/how-to-mitigate-privilege-escalation-with-the-tiered-access-model-for-active-directory-security/)
- [Protección de Tier 0 - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/protecting-tier-0-the-modern-way/ba-p/4052851)

---

📌 **Autor:** José Félix *(Rookieヾ ⁿᵒᵛᵃᵗᵒ)*  
📌 **Repositorio:** [GitHub - Tier 0 Protection](#)  
