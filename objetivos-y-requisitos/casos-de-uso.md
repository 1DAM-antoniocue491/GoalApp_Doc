# Casos de uso

1. **Casos de usos.**

Con el objetivo de simplificar y representar de manera más clara y esquemática los distintos casos de uso de la aplicación, se muestra a continuación una distribución de las funcionalidades disponibles según el rol asignado a cada usuario. De esta forma, es posible identificar de manera visual qué acciones y permisos corresponden a cada tipo de usuario dentro del sistema.

<figure><img src="../.gitbook/assets/image (199).png" alt=""><figcaption></figcaption></figure>

2. **Gestión de Usuarios y Autentificación.**

**a. Asignar Rol en Liga**

* **Actor Principal:** Usuario no registrado
* **Actor Secundario:** Sistema
* **Descripciones:** Permite a una persona crear una cuenta en la aplicación para acceder a sus funcionalidades.
* **Precondiciones:**

\- El usuario no debe estar previamente registrado.

\- Debe proporcionar datos obligatorios válidos.

* **Postcondiciones:** El usuario queda registrado en el sistema con rol base “Usuario”.
* **Flujo principal:**

1. El usuario accede a la pantalla “Registrarse” desde la aplicación.
2. El sistema carga el formulario de registro y muestra los campos obligatorios.
3. El usuario introduce los datos requeridos:
4. Escribe su nombre.
5. Introduce un email válido.
6. Introduce una contraseña.
7. Repite la contraseña (si el formulario lo requiere).
8. El usuario marca la casilla de aceptación de términos y condiciones.
9. El usuario pulsa el botón “Confirmar registro”.
10. El sistema inicia el proceso de validación:
11. Verifica que todos los campos obligatorios estén completos.
12. Comprueba que el email tenga un formato válido.
13. Consulta la base de datos para verificar que el email no esté registrado.
14. Valida que la contraseña cumpla los criterios mínimos de seguridad.
15. Si todas las validaciones son correctas, el sistema procede a crear la cuenta:
16. Inserta el nuevo usuario en la base de datos.
17. Asigna automáticamente el rol base “Usuario”.
18. Genera un identificador único para el usuario.
19. Registra la fecha y hora de creación.
20. El sistema confirma la creación de la cuenta.
21. El sistema inicia sesión automáticamente o redirige a la pantalla de inicio de sesión (según diseño).
22. El usuario queda registrado y puede autenticarse en la aplicación.

* **Flujo Alternativo:**

&#x20;\- Email ya registrado.

\- Datos obligatorios incompletos.

\- Formato de email inválido.

* **Excepciones:**

\- Error en validación de contraseña.

\- Fallo en creación de cuenta.

* **Reglas de Negocio:**

\- El email debe ser único.

\- La contraseña debe cumplir criterios mínimos de seguridad.

\- El usuario se crea con rol básico sin privilegios administrativos.





<br>
