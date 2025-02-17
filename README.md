# 🔐 Principio de Privilegio Mínimo (PoLP)

## 📌 Contenido
- [Introducción](#introducción)
- [Importancia del Privilegio Mínimo](#importancia-del-privilegio-mínimo)
- [Delegate Control en Active Directory](#delegate-control-en-active-directory)
- [Security (NTFS) vs. Sharing (SMB)](#security-ntfs-vs-sharing-smb)
- [Auditoría de Archivos y Carpetas](#auditoría-de-archivos-y-carpetas)
- [Active Directory Tier Model](#active-directory-tier-model)
- [Créditos](#créditos)

---

## 📖 Introducción
El **Principio de Privilegio Mínimo (PoLP)** es una estrategia de seguridad que otorga a los usuarios solo los permisos estrictamente necesarios para realizar sus funciones laborales. Aplicar este principio ayuda a minimizar riesgos de seguridad y proteger activos críticos dentro de un entorno corporativo.

---

## ⚠️ Importancia del Privilegio Mínimo
La mayoría de los ataques cibernéticos explotan **credenciales privilegiadas**. Reduciendo los privilegios administrativos y de superusuario, se limita la superficie de ataque y se mejora la seguridad organizacional.

Beneficios clave:
✔️ Minimiza el riesgo de accesos no autorizados.  
✔️ Reduce el impacto de malware y ataques internos.  
✔️ Mejora el cumplimiento de normativas de seguridad.  
✔️ Aumenta la trazabilidad y control de accesos.  

---

## 🔑 Delegate Control en Active Directory

Active Directory permite delegar permisos específicos a usuarios estándar o privilegiados, evitando la mala práctica de asignar accesos innecesarios.

🎯 **Casos de uso:**
- Delegación de restablecimiento de contraseñas sin acceso administrativo total.
- Permitir la creación y gestión de cuentas dentro de unidades organizativas específicas.
- Asignación de permisos segmentados para soporte técnico sin otorgar roles elevados.

✅ **Mejor práctica:** Evitar el uso indiscriminado del grupo **Domain Admins** y aplicar el principio de privilegio mínimo.

---

## 🔐 Security (NTFS) vs. Sharing (SMB)
### 📜 Diferencias clave:
- **NTFS (Security):** Permisos aplicados a archivos y carpetas locales.
- **SMB (Sharing):** Permisos de acceso a recursos compartidos en red.

📌 **Regla importante:** Cuando se combinan, **se aplicará el permiso más restrictivo** al acceder a través de la red.

🔎 **Ejemplo:**
```
Security NTFS = Read
Sharing SMB = Change
```
Resultado: Solo se otorgará acceso de **lectura**, ya que NTFS es más restrictivo.

📖 [Leer más sobre Security vs. Sharing](./Security_vs_Sharing.md)

---

## 📂 Auditoría de Archivos y Carpetas

Realizar auditorías de acceso a archivos y carpetas críticas ayuda a detectar accesos sospechosos y a cumplir con normativas de seguridad.

🛠️ **Pasos recomendados:**
1️⃣ Habilitar la auditoría de acceso a objetos en Active Directory.  
2️⃣ Usar scripts de PowerShell para configurar auditoría específica.  
3️⃣ Implementar GPOs para desplegar políticas de auditoría en servidores.  

📖 [Leer más sobre Auditoría de Archivos](./File_Audit.md)

---

## 🏛️ Active Directory Tier Model
El **modelo de niveles en Active Directory** segmenta los permisos administrativos en diferentes capas para reducir riesgos.

📌 **Niveles de acceso:**
- **Tier 0:** Administración de dominio y controladores de AD.
- **Tier 1:** Administración de servidores y aplicaciones.
- **Tier 2:** Administración de estaciones de trabajo y usuarios finales.

✅ **Mejor práctica:** Aplicar segmentación estricta y evitar el uso de cuentas con privilegios elevados en múltiples niveles.

---

## 👨‍💻 Créditos
📌 **Autor:** José Félix *(Rookieヾ ⁿᵒᵛᵃᵗᵒ)*  
📌 **Repositorio:** [GitHub - Least Privilege](#)  
