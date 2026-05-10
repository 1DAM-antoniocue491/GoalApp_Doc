# Autenticación JWT en Frontend Web

El sistema de autenticación implementa un flujo seguro basado en tokens JWT, gestionando la sesión de forma global y persistente.

### 1. Gestión de la Sesión (`AuthContext`)

La sesión del usuario se centraliza en el `AuthContext` (ubicado en `src/features/auth/hooks/useAuth.tsx`), que proporciona los siguientes estados:
- `user`: Objeto con la información del usuario autenticado.
- `token`: El token de acceso actual.
- `isLoading`: Estado de carga durante la validación del token al iniciar la app.
- `isInitializing`: Indica si el sistema está recuperando la sesión desde el almacenamiento.

### 2. Persistencia de Tokens

Para mantener la sesión entre recargas de página, el sistema utiliza `localStorage` con las siguientes claves:
- `AUTH_TOKEN_KEY`: Almacena el access token.
- `AUTH_REFRESH_TOKEN_KEY`: Almacena el refresh token.

### 3. Flujo de Refresh Token (Auto-renovación)

El sistema implementa un mecanismo de renovación automática para evitar que el usuario tenga que iniciar sesión constantemente:

1. **Verificación**: Al cargar la aplicación, `loadUser` verifica si el token actual está próximo a expirar (`isTokenExpiringSoon`).
2. **Renovación**: Si el token ha expirado o está por expirar, se dispara la función `refreshToken()`.
3. **Intercepción**: Si una petición API devuelve un error `401 (Unauthorized)`, el interceptor de Axios pausa las peticiones, solicita un nuevo token y reintenta las llamadas fallidas automáticamente.

### 4. Protección de Rutas (`PrivateRoute`)

El acceso a las funcionalidades del sistema está protegido mediante el componente `PrivateRoute.tsx`.

- **Lógica**: Si un usuario intenta acceder a una ruta protegida sin un token válido en el contexto, es redirigido automáticamente a la página de `/login`.
- **Onboarding**: El sistema verifica si el usuario ha completado el flujo de onboarding antes de permitirle entrar al `/dashboard`.

### 5. Flujo de Salida (Logout)

El proceso de cierre de sesión limpia completamente el estado:
1. Eliminación de tokens en `localStorage`.
2. Reset del estado del `AuthContext` (`user = null`).
3. Redirección inmediata a la página de login.
