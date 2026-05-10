# Gestión de Estados en Frontend Web

GoalApp utiliza una combinación de **React Context API** para estados globales y **Hooks locales** para estados efímeros, asegurando un flujo de datos eficiente y predecible.

### 1. Contextos Globales

Para evitar el "prop drilling" y compartir información entre múltiples features, se han implementado tres contextos principales en `src/context/`:

#### A. AuthContext (`AuthContext.tsx`)
Es el corazón de la aplicación. Gestiona la identidad del usuario y la seguridad.
- **Estado**: Almacena el usuario autenticado, el token JWT y el estado de carga inicial.
- **Acciones**: `login()`, `logout()`, `refreshToken()`.
- **Uso**: Control de acceso en rutas y personalización de la interfaz según el rol.

#### B. SelectedLeagueContext (`SelectedLeagueContext.tsx`)
Permite que la aplicación "recuerde" qué liga está visualizando el usuario en cualquier momento.
- **Estado**: ID y datos básicos de la liga seleccionada actualmente.
- **Acciones**: `setSelectedLeague(league)`.
- **Uso**: Filtra automáticamente los datos de partidos, equipos y estadísticas en toda la app.

#### C. ToastContext (`ToastContext.tsx`)
Gestiona el sistema de notificaciones efímeras (mensajes de éxito, error o advertencia).
- **Estado**: Cola de notificaciones activas.
- **Acciones**: `showToast(message, type)`.
- **Uso**: Feedback inmediato tras acciones del usuario (ej. "Equipo creado con éxito").

### 2. Gestión de Estado Local

Para estados que no necesitan ser globales, se utilizan los siguientes patrones:

*   **`useState`**: Para estados simples de componentes (ej. si un modal está abierto).
*   **`useReducer`**: Para lógicas de estado más complejas dentro de una feature.
*   **Custom Hooks**: Para encapsular la lógica de fetching y transformación de datos, separándola de la vista.

### 3. Sincronización con el Backend

El estado global se sincroniza con la API mediante el siguiente flujo:
1. El componente dispara una acción en el `service`.
2. El `service` realiza la petición HTTP.
3. La respuesta actualiza el estado en el `Context` correspondiente.
4. React dispara el re-renderizado de todos los componentes que consumen ese contexto.

### 4. Persistencia de Estado

El estado de autenticación se persiste en `localStorage` para evitar que el usuario pierda la sesión al recargar la página, mientras que el estado de la liga seleccionada es efímero y se reinicia al cerrar la pestaña.
