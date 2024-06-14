## Auditoría de archivos y carpetas
## Contenido

- Introducción.
- Auditoría de archivos y carpetas.
- Paso practico de implementacion.
- Recomendaciones.

## Introducción.

La auditoría de seguridad es una de las herramientas más eficaces para mantener la seguridad de una empresa.
Uno de los principales objetivos de las auditorías de seguridad es el cumplimiento de las normas.
Además, las auditorías de seguridad ayudan a detectar comportamientos anómalos, a identificar y mitigar brechas
en las directivas de seguridad y a impedir el comportamiento irresponsable mediante la creación de un registro
de la actividad del usuario que puede utilizarse para un análisis forense. Los requisitos de directiva de auditoría
generalmente se impulsan en 4 niveles principales, pero nos centraremos en el siguientes:

Seguridad de la información.

Los seguimientos de auditoría de acceso a archivos a menudo se utilizan para análisis forenses y detección de intrusión.
Poder obtener eventos concretos sobre el acceso a información de alto nivel permite a las organizaciones mejorar notablemente su
tiempo de respuesta y la exactitud de la investigación.

Link Referencia: https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/scenario--file-access-auditing

![image](https://learn.microsoft.com/es-es/windows-server/identity/solution-guides/media/scenario--file-access-auditing/dynamicaccesscontrol_revguide_4.jpg)

## Auditoría de archivos y carpetas.


Durante un tiempo estuve investigando cómo configurar la auditoría del sistema de archivos y carpetas en Windows sin instalar ninguna
solución de tercero y de carpetas críticas. luego de muchas horas de investigación y con una curiosidad que me invadía debido a deseaba
habilitar la auditoria, pero a carpeta críticas y no todas las carpetas de Windows. como muchos procesos en internet tenía documentados.

Mi conclusión fue la siguiente:
He construido un script de PowerShell que se compone de dos archivos.

**DirectoryAudit.ps1** y **PathDirectoryAudit.txt**

Ambos juntos podemos habilitar la auditoria de carpetas criticas sin la necesidad de un software de tercero.


## Paso practico de implementacion.

#### Paso#1 
Se debe tener o crear una politica en AD que habilite el  “Audit Object Access”, **“Success” and “Failure”**
```
Este parámetro de configuración lo podemos encontrar en::
“Computer Configuration” ➔ “Windows Settings” ➔ “Security Settings” ➔ “Local Policies” ➔ “Audit Policy”.
```
#### Paso#2
Crear el **DirectoryAudit.ps1** con el siguiente contenido.

```
$TargetFolders = Get-Content C:\FilesandDirectoryAudit.txt
$AuditUser = "Everyone"
$AuditRules = "CreateFiles,Delete,DeleteSubdirectoriesAndFiles"
$InheritType = "ContainerInherit,ObjectInherit"
$AuditType = "Success"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAuditRule($AuditUser,$AuditRules,$InheritType,"None",$AuditType)
foreach ($TargetFolder in $TargetFolders)
{
    $ACL = Get-Acl $TargetFolder
    $ACL.SetAuditRule($AccessRule)
    Write-Host "Processing >",$TargetFolder
    $ACL | Set-Acl $TargetFolder
}
Write-Host "Audit Policy File/Directory applied successfully."
```
#### Paso#3
Ahora crearemos el **PathDirectoryAudit.txt** con el siguiente contenido.

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
#### Paso#4
Colocar ambos archivo en la carpeta sysvol en mi laboratorio es **C:\Windows\SYSVOL\laps.local\**

#### Paso#5
Creamos una GPO que tome ambos archivo y lo coloque de manera local en cada servidor y luego la ejecute.

```
Computer Configuration ➔ Policies ➔ Windows Settings ➔ Scripts ➔ Startup ➔ C:\Windows\audit\DirectoryAudit.ps1

Computer Configuration ➔ Preferences ➔ Windows Settings ➔ Files ➔
    Source file: \\laps.local\\NETLOGON\audit\DirectoryAudit.ps1
    Destination file: C:\Windows\audit\DirectoryAudit.ps1
    
Computer Configuration ➔ Preferences ➔ Windows Settings ➔ Files ➔
    Source file: \\laps.local\\NETLOGON\audit\PathDirectoryAudit.txt
    Destination file: C:\Windows\audit\PathDirectoryAudit.txt
```


