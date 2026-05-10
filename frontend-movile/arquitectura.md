# Arquitectura Frontend Móvil

El frontend móvil de GoalApp es una aplicación de alto rendimiento desarrollada con un enfoque en la experiencia de usuario nativa y la robustez en la comunicación de datos.

### 1. Stack Tecnológico

La aplicación utiliza el ecosistema más moderno de desarrollo móvil con JavaScript/TypeScript:

*   **React Native 0.81.5**: Framework principal para la creación de la interfaz nativa.
*   **Expo SDK 54.0.33**: Entorno de desarrollo que facilita el acceso a APIs nativas y el despliegue rápido.
*   **Expo Router (~6.0.23)**: Sistema de navegación basado en archivos (*file-based routing*), lo que permite una estructura de rutas intuitiva y declarativa.
*   **NativeWind 5 / Tailwind CSS 4**: Implementación de estilos utilitarios para un diseño consistente y responsivo en iOS y Android.

### 2. Estructura de Navegación

La aplicación utiliza un sistema de rutas jerárquico gestionado en `src/app/`:

*   **Rutas Raíz**: Controlan el flujo inicial (Onboarding $\rightarrow$ Auth $\rightarrow$ App).
*   **Grupos de Rutas**: Utiliza grupos como `(tabs)` para separar la navegación principal de las vistas de detalle.
*   **Navegación por Tabs**: Implementa 5 pestañas principales: Inicio, Calendario, Añadir (Acciones Rápidas), Estadísticas y Perfil.

### 3. Patrón de Diseño: Modular por Dominios

Al igual que la versión web, la aplicación móvil sigue una arquitectura basada en dominios funcionales dentro de `src/features/`.

**Estructura de una Feature móvil:**
- `api/`: Definición de endpoints y llamadas al servicio.
- `components/`: Componentes de UI específicos del dominio.
- `hooks/`: Lógica de estado y efectos locales.
- `services/`: Lógica de negocio y procesamiento de datos.
- `types/`: Interfaces de TypeScript exclusivas del módulo.

**Módulos implementados:**
`calendar`, `dashboard`, `leagues`, `matches`, `notifications`, `profile`, `public`, `statistics`, `teams`, y `users`.

### 4. Gestión de Rendimiento

*   **Optimización de Listas**: Uso de componentes optimizados para el renderizado de grandes volúmenes de datos (estandarizado en React Native).
*   **Imágenes**: Gestión eficiente de carga de activos y logos de equipos.
*   **Interacciones**: Uso de animaciones nativas para transiciones fluidas entre pantallas.
