# Gestión de Estados en Frontend Móvil

 la aplicación móvil implementa un sistema de gestión de estado híbrido que optimiza el rendimiento y asegura la persistencia de la sesión.

### 1. Estado Global mediante Stores (`src/state/`)

En lugar de utilizar una sola librería masiva, la aplicación emplea **stores especializados** con un sistema de listeners para actualizar la UI de forma reactiva:

#### A. `sessionStore`
Gestiona la identidad del usuario y la seguridad.
- **Persistencia**: Sincronizado con `expo-secure-store`.
- **Responsabilidad**: Almacenar el token de acceso, el refresh token y los datos básicos del perfil.

#### B. `activeLeagueStore`
Controla el contexto de la liga que el usuario está operando.
- **Responsabilidad**: Almacenar la liga seleccionada y el rol activo del usuario (`Admin`, `Coach`, `Player`, `FieldDelegate`, `Observer`).
- **Uso**: Determina qué dashboard debe renderizar la aplicación y qué filtros aplicar a las peticiones API.

#### C. `uiStore`
Diseñado para gestionar estados efímeros de la interfaz (modales, alertas, temas). Actualmente se encuentra en fase de implementación o delegada a hooks locales.

### 2. Server State vs App State

La aplicación distingue claramente entre dos tipos de estado:

1. **Server State**: Datos que residen en el servidor (ej. resultados de un partido). Se gestionan mediante el `QueryProvider` (basado en TanStack Query) para manejar el caching y la revalidación automática.
2. **App State**: Datos locales de la aplicación (ej. la liga activa). Se gestionan mediante los stores mencionados anteriormente.

### 3. Flujo de Sincronización

El flujo de datos sigue este ciclo:
1. **Acción**: El usuario cambia de liga en la UI.
2. **Store**: El `activeLeagueStore` se actualiza con la nueva liga.
3. **Notificación**: Todos los componentes suscritos al store se re-renderizan automáticamente.
4. **API**: Las siguientes peticiones al backend incluyen el `id_liga` actualizado en los parámetros.

### 4. Providers de Contexto

Para la inyección de dependencias y el acceso global, se utiliza un `AuthProvider` que envuelve la aplicación, asegurando que la información de la sesión esté disponible en cualquier pantalla a través de hooks personalizados.
