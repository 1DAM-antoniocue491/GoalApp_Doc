# Estructura del Proyecto Frontend Web

La aplicación sigue una organización modular basada en el dominio funcional (**Feature-Based Architecture**), lo que permite que cada funcionalidad sea independiente y fácil de mantener.

### 1. Directorios Principales

```
src/
├── assets/          # Imágenes, fuentes y archivos estáticos
├── components/      # Componentes genéricos y reutilizables (UI Kit)
├── context/         # Contextos globales de estado
├── features/        # Lógica de negocio dividida por dominios (CORE)
├── hooks/          # Hooks personalizados globales
├── services/       # Configuración del cliente API (Axios)
├── types/          # Definiciones de interfaces globales
└── utils/          # Funciones auxiliares y helpers
```

### 2. Detalle de las Features (`src/features/`)

Cada carpeta dentro de `features/` es un módulo autónomo que contiene todo lo necesario para su funcionamiento:

| Feature | Responsabilidad |
|----------|------------------|
| `auth` | Login, registro, recuperación de password y gestión de sesión. |
| `calendario` | Visualización y gestión de fechas de partidos. |
| `league` | Administración de ligas y configuración de torneos. |
| `main` | Componentes comunes del layout y dashboard general. |
| `match` | Gestión de eventos, alineaciones y resultados de partidos. |
| `notificaciones` | Centro de alertas y notificaciones push. |
| `onboarding` | Flujo de creación y configuración inicial de la cuenta. |
| `statistic` | Procesamiento y visualización de datos de rendimiento. |
| `team` | Gestión de plantillas, equipos y personal técnico. |
| `users` | Administración de perfiles y gestión de usuarios del sistema. |

### 3. Anatomía de una Feature

Dentro de cada módulo de feature, se sigue la siguiente estructura interna:

```
feature-name/
├── components/   # Componentes específicos de la funcionalidad
├── pages/        # Vistas principales consumidas por el router
├── services/     # Definición de endpoints específicos de la feature
├── types/        # Tipos de TypeScript exclusivos del dominio
└── hooks/        # Lógica de estado local de la feature
```

### 4. Flujo de Navegación

El enrutamiento se centraliza en `App.tsx`, donde se definen las rutas públicas y las rutas protegidas por el `PrivateRoute`, conectando cada ruta con la `Page` correspondiente dentro de su respectiva `feature`.
