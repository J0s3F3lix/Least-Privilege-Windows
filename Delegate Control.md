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

Iniciaremos creando nuestro primer grupo llamado "AD.Delegate_Account"

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWj0qPhdQvqBHEjaWX3TerTlQVoEaGKzXyOUAZVTMDwItw56UY04wVymvKdD-YFNjSqGAK2qswJE4z1p_olSL8SF11gp77fCeYwSoMCkiAiDgSxeAhY-1Zc7IWouhMBAB2MHnTr_K7Fxa5/s1600/Delegate1.jpg)

>Dicho grupo lo utilizaremos para dar privilegio a Crear, Mover y Elimiar usuarios en AD.

>Luego de crear el grupo hacemos clic derecho en lab.local(este caso es mi dominio de prueba)
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

### Recomendaciones Generales.

>Cuando hagamos un delegar control, favor NO utilizar grupos de AD por default. Ejemplo
No use: "Backup Operators" o "DHCP Administrator"
Estos grupos de AD tienen permisos especiales que pueden otorgar a los usuarios más privilegios de los necesarios.

