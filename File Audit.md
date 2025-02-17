# 📂 Auditoría de Archivos y Carpetas

## 📌 Contenido
- [Introducción](#introducción)
- [Importancia de la Auditoría](#importancia-de-la-auditoría)
- [Implementación Práctica](#implementación-práctica)
- [Recomendaciones Finales](#recomendaciones-finales)
- [Créditos](#créditos)

---

## 📖 Introducción
La auditoría de seguridad es una de las herramientas más eficaces para mantener la integridad y protección de los sistemas de una empresa. Su principal objetivo es garantizar el cumplimiento normativo y detectar comportamientos anómalos que puedan comprometer la seguridad de la información.

Al implementar un sistema de auditoría, las organizaciones pueden:
- Identificar y mitigar brechas en sus directivas de seguridad.
- Impedir acciones irresponsables mediante registros detallados de actividad.
- Mejorar el tiempo de respuesta ante incidentes.

📌 **Referencia:** [Microsoft Docs - File Access Auditing](https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/scenario--file-access-auditing)

![Auditoría de Archivos](https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/media/scenario--file-access-auditing/dynamicaccesscontrol_revguide_4.jpg)

---

## 🔍 Importancia de la Auditoría

Los seguimientos de auditoría de acceso a archivos permiten realizar análisis forenses y detectar intrusiones de manera efectiva. Contar con eventos detallados sobre accesos no autorizados ayuda a reforzar la seguridad en entornos empresariales.

### 🎯 Beneficios clave:
✔️ Detección temprana de accesos sospechosos.  
✔️ Registro detallado para análisis forense.  
✔️ Mayor control sobre la información sensible.  
✔️ Cumplimiento de normativas de seguridad.  

---

## ⚙️ Implementación Práctica

A continuación, se detalla un método eficiente para habilitar la auditoría de archivos y carpetas críticas en Windows sin necesidad de software de terceros.

### 🛠️ **Paso 1: Configurar la Política de Auditoría en Active Directory**

Se debe habilitar la opción **“Audit Object Access”** con las configuraciones **“Success” y “Failure”** en la siguiente ruta:
```
Computer Configuration ➔ Windows Settings ➔ Security Settings ➔ Local Policies ➔ Audit Policy
```

### 📝 **Paso 2: Crear el script `DirectoryAudit.ps1`**
Este script en PowerShell permite establecer reglas de auditoría sobre las carpetas críticas:

```powershell
$TargetFolders = Get-Content C:\FilesandDirectoryAudit.txt
$AuditUser = "Everyone"
$AuditRules = "CreateFiles,Delete,DeleteSubdirectoriesAndFiles"
$InheritType = "ContainerInherit,ObjectInherit"
$AuditType = "Success"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAuditRule($AuditUser,$AuditRules,$InheritType,"None",$AuditType)

foreach ($TargetFolder in $TargetFolders) {
    $ACL = Get-Acl $TargetFolder
    $ACL.SetAuditRule($AccessRule)
    Write-Host "Procesando >", $TargetFolder
    $ACL | Set-Acl $TargetFolder
}

Write-Host "Política de auditoría aplicada con éxito."
```

### 📂 **Paso 3: Crear el archivo `PathDirectoryAudit.txt`**
Este archivo debe contener las rutas de las carpetas a auditar:

```
C:\Windows\AppPatch\Custom
C:\Windows\system32\Drivers
C:\Windows\System32\drivers\etc
C:\Windows\system32\GroupPolicy\Machine\Scripts
C:\Windows\system32\GroupPolicy\User\Scripts
C:\Windows\system32\Tasks
C:\Windows\system32\Wbem
C:\Windows\SysWOW64\Drivers
C:\Windows\SysWOW64\Tasks
C:\Windows\SysWOW64\Wbem
C:\Windows\SysWOW64\WindowsPowerShell
C:\Windows\Tasks
```

### 🔧 **Paso 4: Implementación con GPO**
Los archivos `DirectoryAudit.ps1` y `PathDirectoryAudit.txt` deben ser almacenados en `C:\Windows\SYSVOL\laps.local\`.

A continuación, configuramos una **GPO** para distribuir y ejecutar el script en todos los servidores:
```
Computer Configuration ➔ Policies ➔ Windows Settings ➔ Scripts ➔ Startup ➔ C:\Windows\audit\DirectoryAudit.ps1

Computer Configuration ➔ Preferences ➔ Windows Settings ➔ Files ➔
    Source file: \\laps.local\\NETLOGON\audit\DirectoryAudit.ps1
    Destination file: C:\Windows\audit\DirectoryAudit.ps1

Computer Configuration ➔ Preferences ➔ Windows Settings ➔ Files ➔
    Source file: \\laps.local\\NETLOGON\audit\PathDirectoryAudit.txt
    Destination file: C:\Windows\audit\PathDirectoryAudit.txt
```

---

## ✅ Recomendaciones Finales
✔️ **Evita auditar carpetas del sistema innecesarias** para reducir el impacto en el rendimiento.  
✔️ **Revisa periódicamente los logs** para detectar accesos inusuales.  
✔️ **Integra soluciones de SIEM** para correlacionar eventos de auditoría.  
✔️ **Restringe el acceso a los registros** solo a personal autorizado.  

---

## 👨‍💻 Créditos
📌 **Autor:** José Félix *(Rookieヾ ⁿᵒᵛᵃᵗᵒ)*  
📌 **Repositorio:** [GitHub - File Audit](#)  
