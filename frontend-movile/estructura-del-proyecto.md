# Estructura del Proyecto Frontend Móvil

La aplicación móvil sigue una arquitectura modular y escalable basada en el estándar de **expo-router** y una organización por dominios funcionales.

### 1. Organización de Directorios

La estructura de archivos está diseñada para separar la configuración de rutas de la lógica de negocio:

```
src/
├── app/             # Routing basado en archivos (Expo Router)
├── features/        # Lógica de negocio modular por dominio
├── shared/          # Componentes, estilos y utilidades compartidos
├── state/           # Gestión de estado global (Stores)
├── providers/       # Envoltorios de contexto y configuración global
└── mocks/           # Datos de prueba para desarrollo offline
```

### 2. El Sistema de Routing (`src/app/`)

Utiliza el patrón de **File-based Routing** de Expo, donde la estructura de carpetas define la URL de la aplicación:

- **`(tabs)/`**: Grupo de rutas para la navegación principal por pestañas.
- **`auth/`**: Rutas para login, registro y recuperación de cuenta.
- **`league/`**, **`matches/`**, **`statistics/`**: Rutas detalladas para cada entidad del sistema.

### 3. Organización de Features (`src/features/`)

Cada funcionalidad se encapsula en su propio módulo para evitar la interdependencia:

| Feature | Responsabilidad |
|----------|------------------|
| `calendar` | Gestión de fechas y programación de partidos. |
| `dashboard` | Orquestación de vistas según el rol del usuario. |
| `leagues` | Visualización y administración de ligas. |
| `matches` | Gestión de partidos en vivo y resultados. |
| `notifications` | Centro de alertas y notificaciones push. |
| `profile` | Gestión de datos del usuario y ajustes. |
| `public` | Vistas accesibles para usuarios no autenticados. |
| `statistics` | Análisis de rendimiento de jugadores y equipos. |
| `teams` | Gestión de plantillas y personal técnico. |
| `users` | Administración de perfiles y permisos. |

### 4. Anatomía de un Módulo de Feature

Cada feature contiene su propia infraestructura interna:
- `api/`: Llamadas específicas al backend.
- `components/`: UI exclusiva de esa funcionalidad.
- `hooks/`: Lógica de estado y efectos locales.
- `services/`: Procesamiento de datos y lógica de negocio.
- `types/`: Definiciones de TypeScript para el dominio.
