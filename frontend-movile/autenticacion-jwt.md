# Autenticación JWT en Frontend Móvil

El sistema de autenticación móvil implementa medidas de seguridad reforzadas para la protección de tokens en dispositivos físicos.

### 1. Persistencia Segura (`expo-secure-store`)

A diferencia de la versión web que utiliza `localStorage`, la aplicación móvil utiliza **`expo-secure-store`** para almacenar la sesión. Esto garantiza que los tokens se guarden en el almacenamiento cifrado del sistema operativo:
- **iOS**: Keychain
- **Android**: EncryptedSharedPreferences

Se almacenan los siguientes datos en el `sessionStore.ts`:
- `access_token`
- `refresh_token`
- Objeto de perfil del `user`.

### 2. Flujo de Refresh Token y Concurrencia

Para evitar la pérdida de sesión y manejar múltiples peticiones simultáneas cuando el token expira, se ha implementado un sistema de **cola de suscriptores (`refreshSubscribers`)**:

1. **Detección**: Una petición API devuelve un error `401`.
2. **Bloqueo**: Se activa la bandera `isRefreshing = true`.
3. **Cola**: Todas las peticiones concurrentes que fallen mientras se renueva el token se añaden a una cola de espera.
4. **Renovación**: Se solicita un nuevo token al endpoint `/auth/refresh`.
5. **Resolución**: Una vez obtenido el nuevo token, se notifican a todos los suscriptores de la cola y se reintentan las peticiones originales.

### 3. Protección de Rutas y Roles

El acceso a las pantallas se controla mediante un `AuthProvider` y un `ProtectedRoute`.

- **Validación**: El sistema verifica el token al iniciar y en cada cambio de ruta crítica.
- **Sincronización de Roles**: El rol del usuario (`Admin`, `Coach`, `Player`, `FieldDelegate`, `Observer`) se recupera del token y se almacena en el estado global para adaptar la interfaz de usuario en tiempo real.
