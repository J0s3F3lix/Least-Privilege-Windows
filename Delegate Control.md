# Delegate Control en Active Directory

## Índice
- [Introducción](#introducción)
- [Mejores Prácticas](#mejores-prácticas)
- [Delegaciones Comunes](#delegaciones-comunes)
- [Ejemplo de Configuración](#ejemplo-de-configuración)
- [Recomendaciones Generales](#recomendaciones-generales)
- [Créditos](#créditos)

---

## Introducción

Active Directory permite delegar controles a usuarios estándar o privilegiados de manera granular. En entornos corporativos, el soporte técnico invierte una cantidad considerable de tiempo en tareas repetitivas como:

- Restablecimiento de contraseñas
- Desbloqueo de cuentas
- Creación de usuarios

Si bien estas tareas son simples, consumen tiempo y pueden generar riesgos de seguridad si no se gestionan correctamente. La delegación de control permite asignar estos permisos al personal adecuado sin comprometer la seguridad, evitando otorgar privilegios innecesarios, como el acceso de **Domain Admin** o **Administrador local**.

---

## Mejores Prácticas

La delegación de permisos en Active Directory se realiza mediante **Unidades Organizativas (OU - Organizational Units)**. Un buen diseño de OU es fundamental para garantizar una administración eficiente y segura. Aunque la estructura puede variar según la organización, una recomendación general es agrupar los recursos similares dentro de su propia OU.

---

## Delegaciones Comunes

| **Tipo**          | **Permisos Delegados** |
|------------------|----------------------|
| **User Account**  | Create, Move, Password Reset, Disable |
| **Computers**     | Create, Move, Disable |
| **Groups**       | Create, Move, Disable |
| **Organizational Unit** | Create, Move, Delete |


---

## Ejemplo de Configuración

### 1️⃣ Crear un Grupo de Delegación

Crearemos un grupo llamado **`AD.Delegate_Account`** con la siguiente descripción:


![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWj0qPhdQvqBHEjaWX3TerTlQVoEaGKzXyOUAZVTMDwItw56UY04wVymvKdD-YFNjSqGAK2qswJE4z1p_olSL8SF11gp77fCeYwSoMCkiAiDgSxeAhY-1Zc7IWouhMBAB2MHnTr_K7Fxa5/s1600/Delegate1.jpg)


### 2️⃣ Delegar Permisos en Active Directory

Luego de crear el grupo, seguimos estos pasos:
1. Hacer clic derecho en la raíz de Active Directory (ejemplo: `lab.local`).
2. Seleccionar la opción **Delegate Control**.
3. Seguir las instrucciones del asistente de delegación.

#### 📸 Capturas del Proceso
![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjk_4MzzM-8odrUOjv7LK1SzG0alH9x8eQS4T0DEIBPPuH5BkgADdaCa9Wjj53VEjR9PpITm4GaeOdVyna1Gw8p6L3KqKVzMu8FhOim78HC2xUm-L3ho5vzoH7tdhBH2c0-iuG4uo7248qX/s1600/Delegate.png)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEGr2U1BXPLzYV2OBoQxXDqrUmWyUk8DJaUYeMBL6m6j1MtikQlZ3bWabC1tPLNTq2Y2ziiMAIVReasfS6VZrlZ0yvNTO9XEynAgR1Q2NKvSCNosb_3TbbqLXtWwVE6kdjrkZyRYCdD9el/s1600/Delegate2.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipunJYzpXQz5_StgHjk-4MPI52egil078nkU9AKYp3_ZVhmbf5FdMcruCNYVBROT9eW4hLXSCmlOPEovUAyMTeitZdvT6n0RB4aHHTZSQCJVk2C1HS3_snjwyzRsttj7fXBQSh8h60BquR/s1600/Delegate3.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjzL94enTQTW8DFWB8gtRSIA_1Nqftd8QnAKQNW1JaycPuUCcOtIdaoq_F2HVPD-V3mcIdpFR9r0o18xYzikyCoh3SrNsTGp0fucRBf43KgSyDjhkxbZQvrvsGXlnDXdkIzYgNXdq-v3poG/s1600/Delegate4.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEha2K1xUwii72mMkvpj4P8tj-8NxNlIdctsBDnt2T0o5A91lU8o9vu5W5bd_f3KOzQTs7_HOixau7rtWMadcQDITIgsNdUdlAj-Oii5Pjr8CNlQbyR39UsTHu8PyHA1hPPArnqxOw0WbvWf/s1600/Delegate5.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh5R9XBDM5mm7zTPGBdN00UY7wdqSAjf9u5vT1KP6sSENNjSaAnqZCFfz9prMcKkwyxNVSKifmNqgXX6cYoLlAK5kuZZwcAl5GH7yHkHJCuB8pOkQRq9RVUVbkoYQ6MKCgMOKWDB5BXVOui/s1600/Delegate6.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEif44Ewcfo__d8gSZ1I-ia5duVNbsFJMmkl9H87WCy2w3M9yBtJyuE7iv1tJLYeUFyxx10ZjujZZpJpguuikaU7tNdrxe8Dbg67Jzt5KJ6d1accDD4fIkubbJ3_AwODX1UFELDIx5M0Fcdk/s1600/Delegate7.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjhqyHpC_IRrQ5pT5mDGVCDP8H5X5fezXR0ykko1DPPx_puF0PmwgiUWm6pnT_qVU5ukmVxvuJLGh0AsibACZeB1FEQstgHx-Txe1XhOTOZ-AKtb_3A79pTaDYSi6VtWnHT93N9PpUN-Sek/s1600/Delegate8.jpg)

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiiD-4X-Zcx57Jlrdg48oheR9H_ZMR6xqlT4AJsA4vJdF8sHGKFt4WUhdd_-L4qHd6pdoTKFcwQ-n1abOe5V-Jc6Zejmonr0LlxwL4_N_8-tXLotcMRKodYZ9nzHBlpU_i84BdmG7r6yVWP/s1600/Delegate9.jpg)

Listo, con estos simples pasos, tenemos nuestro primer delegate.

## Recomendaciones Generales

✅ **No usar grupos predeterminados de Active Directory** para delegar control. 

🚫 *Evitar grupos como:* `Backup Operators`, `DHCP Administrator`.

Estos grupos tienen permisos especiales que pueden otorgar más privilegios de los necesarios a los usuarios.

---

## Créditos

📌 **Autor:** Jose Félix *(Rookieヾ ⁿᵒᵛᵃᵗᵒ)*

