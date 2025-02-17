# 🔐 Security (NTFS) vs. Sharing (SMB)

## 📌 Contenido
- [Introducción](#introducción)
- [Permisos NTFS (Security)](#permisos-ntfs-security)
- [Permisos SMB (Sharing)](#permisos-smb-sharing)
- [Ejemplos Prácticos](#ejemplos-prácticos)
- [Créditos](#créditos)

---

## 📖 Introducción
Al administrar permisos en Windows, es común confundir los permisos de seguridad de **NTFS (Security)** con los permisos de compartición de **SMB (Sharing)**. Es fundamental entender que al combinar ambos, se aplicará **el permiso más restrictivo** cuando se accede a los recursos compartidos en la red.

Este documento tiene como objetivo aclarar las diferencias y ayudar a comprender cómo funcionan ambos modelos de permisos.

---

## 🔒 Permisos NTFS (Security)
Los permisos NTFS controlan el acceso a archivos y carpetas en sistemas de archivos formateados con NTFS, ya sea en acceso local o remoto. Estos permisos son más detallados y ofrecen un mayor control.

### 📜 Lista de Permisos NTFS:
```plaintext
Full Control = Acceso total, incluyendo administración de permisos.
Modify = Permite modificar archivos y carpetas.
Read & Execute = Permite leer y ejecutar archivos.
List Folder Contents = Solo permite listar los contenidos de la carpeta.
Read = Solo permite leer el contenido de archivos y carpetas.
Write = Permite escribir y modificar archivos, pero no eliminarlos.
Special Permissions = Permisos personalizados específicos.
```

---

## 🌐 Permisos SMB (Sharing)
Los permisos de compartición (SMB) determinan el acceso a carpetas compartidas en una red. Estos permisos son menos granulares y solo controlan el acceso al recurso compartido.

### 📜 Lista de Permisos SMB:
```plaintext
Full Control = Acceso total a la carpeta compartida.
Change = Permite modificar archivos y carpetas dentro del recurso compartido.
Read = Solo permite leer archivos dentro de la carpeta compartida.
```

---

## 🧩 Ejemplos Prácticos

### 🔹 **Ejemplo 1**
> **Configuración:**
```
Security NTFS = Read
Sharing SMB = Change
```
**Resultado:** El usuario tendrá acceso de **solo lectura**, ya que NTFS es más restrictivo.

### 🔹 **Ejemplo 2**
> **Configuración:**
```
Security NTFS = Full Control
Sharing SMB = Change
```
**Resultado:** El usuario tendrá acceso de **cambio/modificación**, ya que Sharing SMB es más restrictivo.

📌 **Regla General:** **Siempre se aplicará el permiso más restrictivo** cuando se acceda al recurso desde la red.

---

## 👨‍💻 Créditos
📌 **Autores:** José Félix *(Rookieヾ ⁿᵒᵛᵃᵗᵒ)* y Dayner Rolando Félix  
📌 **Repositorio:** [GitHub - Security vs Sharing](#)  
