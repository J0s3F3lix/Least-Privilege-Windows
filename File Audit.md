
# Auditoría de Archivos y Carpetas

## Contenido

- [Introducción](#introducción)
- [Auditoría de archivos y carpetas](#auditoría-de-archivos-y-carpetas)
- [Paso práctico de implementación](#paso-práctico-de-implementación)
- [Recomendaciones](#recomendaciones)
- [Créditos](#créditos)

## Introducción

La auditoría de seguridad es una de las herramientas más eficaces para mantener la seguridad de una empresa. Uno de sus principales objetivos es garantizar el cumplimiento de normativas, detectar comportamientos anómalos y prevenir accesos no autorizados mediante el registro de actividad de los usuarios.

Los seguimientos de auditoría de acceso a archivos permiten a las organizaciones mejorar notablemente su tiempo de respuesta y la exactitud de la investigación.

> **Referencia**: [Auditoría de acceso a archivos en Windows](https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/scenario--file-access-auditing)

![Auditoría de acceso](https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/media/scenario--file-access-auditing/dynamicaccesscontrol_revguide_4.jpg)

## Auditoría de Archivos y Carpetas

Durante un tiempo, investigué cómo configurar la auditoría del sistema de archivos y carpetas en Windows sin instalar software de terceros. Tras muchas pruebas, diseñé un método para auditar carpetas críticas sin afectar todo el sistema.

### Solución propuesta

Se compone de dos archivos:

- **`DirectoryAudit.ps1`** → Script de PowerShell.
- **`PathDirectoryAudit.txt`** → Lista de carpetas críticas.

## Paso Práctico de Implementación

### Paso 1: Configurar Auditoría en AD
Se debe crear o modificar una política en Active Directory que habilite la auditoría de acceso a objetos.

```plaintext
Ubicación: Computer Configuration → Windows Settings → Security Settings → Local Policies → Audit Policy
Habilitar: "Audit Object Access" (Success & Failure)
```

### Paso 2: Crear `DirectoryAudit.ps1`

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

Write-Host "Política de auditoría aplicada correctamente."
```

### Paso 3: Crear `PathDirectoryAudit.txt`
Lista de directorios críticos:

```plaintext
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

### Paso 4: Ubicar los Archivos en SYSVOL
Los archivos deben almacenarse en:
```plaintext
C:\Windows\SYSVOL\laps.local\
```

### Paso 5: Configurar la GPO
Crear una política de grupo (GPO) para distribuir y ejecutar el script:

```plaintext
Computer Configuration → Policies → Windows Settings → Scripts → Startup → C:\Windows\audit\DirectoryAudit.ps1

Computer Configuration → Preferences → Windows Settings → Files →
    Source: \\laps.local\NETLOGON\audit\DirectoryAudit.ps1
    Destination: C:\Windows\audit\DirectoryAudit.ps1

Computer Configuration → Preferences → Windows Settings → Files →
    Source: \\laps.local\NETLOGON\audit\PathDirectoryAudit.txt
    Destination: C:\Windows\audit\PathDirectoryAudit.txt
```

## Recomendaciones
- Revisar periódicamente los registros de auditoría.
- No habilitar auditoría en todas las carpetas del sistema para evitar sobrecarga.
- Probar en un entorno de prueba antes de implementarlo en producción.

## Créditos
Este contenido fue elaborado por **José Félix (Rookieヾ ⁿᵒᵛᵃᵗᵒ)**.
