# Arquitectura Frontend Web

El frontend de GoalApp es una aplicación moderna desarrollada con un enfoque de **estabilidad, tipado fuerte y alta escalabilidad**.

### 1. Stack Tecnológico

La aplicación utiliza las versiones más recientes y estables de las siguientes tecnologías:

*   **React 19.2.0**: Librería principal para la construcción de la interfaz de usuario.
*   **Vite 7.3.1**: Herramienta de build ultra-rápida y servidor de desarrollo.
*   **TypeScript 5.9.3**: Tipado estático para reducir errores en tiempo de ejecución y mejorar la mantenibilidad.
*   **Tailwind CSS 4.2.1**: Framework de CSS utilitario para un diseño rápido y consistente, utilizando el nuevo plugin `@tailwindcss/vite`.

### 2. Patrón de Diseño: Feature-Based Architecture

A diferencia de las arquitecturas tradicionales organizadas por tipo de archivo (todos los componentes juntos, todas las páginas juntas), GoalApp implementa una **Arquitectura Basada en Features**.

Este enfoque agrupa el código por dominio funcional, facilitando la localización de archivos y reduciendo la complejidad cognitiva.

**Estructura de un módulo de Feature:**
Cada feature en `src/features/[feature-name]/` contiene:
- `components/`: Componentes específicos de esa funcionalidad.
- `pages/`: Vistas principales de la feature.
- `services/`: Llamadas a la API relacionadas con el dominio.
- `types/`: Definiciones de interfaces y tipos de TypeScript.
- `hooks/`: Lógica de estado y efectos compartida dentro de la feature.

**Módulos implementados:**
`auth`, `calendario`, `league`, `main`, `match`, `notificaciones`, `onboarding`, `statistic`, `team`, y `users`.

### 3. Flujo de Datos y Renderizado

La aplicación sigue un flujo unidireccional de datos:
1. **API Service**: El servicio de la feature solicita datos al backend.
2. **Context/State**: Los datos se almacenan en el contexto correspondiente (ej. `SelectedLeagueContext`).
3. **Component**: Los componentes consumen el estado y renderizan la UI.

### 4. Optimización y Rendimiento

*   **Lazy Loading**: Las rutas principales están optimizadas para cargar solo el código necesario para la vista actual.
*   **SFC (Stateless Functional Components)**: Priorización de componentes funcionales y hooks para un renderizado eficiente.
*   **Caché de API**: Implementación de interceptores para evitar peticiones redundantes.
