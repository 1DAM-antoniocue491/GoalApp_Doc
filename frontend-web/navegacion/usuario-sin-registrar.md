# Navegación de Usuarios No Registrados (Frontend Web)

Este documento describe la lógica de acceso y las restricciones de navegación aplicadas a los usuarios que no han iniciado sesión o no poseen una cuenta en la plataforma web de GoalApp.

## 1. Filosofía de Acceso
La aplicación implementa un modelo de **Acceso Restringido**, donde la gran mayoría de la funcionalidad está protegida. Los usuarios no registrados tienen una experiencia limitada diseñada exclusivamente para la conversión (registro) y la recuperación de credenciales.

## 2. Rutas Accesibles (Zonas Públicas)
Los usuarios no autenticados solo pueden acceder a las siguientes rutas:

### A. Dashboard Público (`/`)
Es la página de aterrizaje de la aplicación. Permite a los visitantes obtener una visión general del sistema sin necesidad de autenticarse. Es la única vista de "datos" de la plataforma accesible para el público general.

### B. Flujo de Autenticación y Registro
- **Login (`/login`)**: Acceso al formulario de inicio de sesión.
- **Registro (`/register`)**: Flujo de creación de nueva cuenta.

### C. Flujo de Recuperación de Contraseña
El sistema permite la navegación completa por el proceso de recuperación:
1. **Solicitud de Recuperación (`/forgot-password`)**: Formulario para enviar el correo electrónico.
2. **Confirmación de Envío (`/email-sent`)**: la página de aviso tras el envío del token.
3. **Restablecimiento de Contraseña (`/reset-password`)**: Formulario final para definir la nueva contraseña.

---

## 3. Mecanismo de Restricción (Auth Guards)

El control de acceso se gestiona a través del componente **`PrivateRoute`**, que actúa como un guardián de rutas.

### Lógica de Intercepción
Cuando un usuario intenta acceder a cualquier ruta fuera de las mencionadas anteriormente (ej. `/dashboard`, `/leagues`, `/calendar`), el componente `PrivateRoute` ejecuta la siguiente validación:

1. **Verificación de Estado**: Consulta el hook `useAuth()` para determinar si el usuario está autenticado (`isAuthenticated`).
2. **Estado de Inicialización**: Si el sistema aún está validando el token al cargar la página (`isInitializing`), se muestra un spinner de carga para evitar redirecciones erróneas.
3. **Redirección Forzosa**: Si `isAuthenticated` es `false`, el sistema intercepta la navegación y redirige al usuario inmediatamente a `/login`.

### Persistencia de la Intención de Navegación
Para mejorar la experiencia de usuario, el `PrivateRoute` guarda la ruta que el usuario intentaba visitar en el estado de la navegación. Una vez que el usuario se autentica con éxito, el sistema puede redirigirlo automáticamente a la página original en lugar de enviarlo siempre al dashboard principal.

## 4. Comparativa de Experiencia (No Registrado vs. Registrado)

| Elemento | Usuario No Registrado | Usuario Registrado |
| :--- | :--- | :--- |
| **URL Raíz (`/`)** | Ve el Dashboard Público | Ve el Dashboard Público (o es redirigido) |
| **Ruta `/dashboard`** | Bloqueada $\rightarrow$ Redirige a Login | Acceso Total (según Rol) |
| **Gestión de Ligas** | Bloqueada $\rightarrow$ Redirige a Login | Acceso Total |
| **Perfil / Ajustes** | Bloqueada $\rightarrow$ Redirige a Login | Acceso Total |
| **Recuperación de Contraseña**| Acceso Total | Acceso Total |
