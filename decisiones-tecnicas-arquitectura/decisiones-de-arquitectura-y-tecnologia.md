# Decisiones de Arquitectura y Tecnología

### Arquitectura general

**Decisión:** Arquitectura cliente–servidor con API REST\
**Justificación:**

* Separación clara entre frontend y backend.
* Permite reutilizar la API para móvil y web.
* Facilita trabajo en equipo, escalabilidad y seguridad.
* El frontend no accede directamente a la base de datos.

### Frontend

**Tecnología:** React Native + Expo\
**Decisión:** Una única base de código para Android, iOS y Web\
**Justificación:**

* Desarrollo más rápido y menor coste de mantenimiento.
* Componentes reutilizables.
* Adecuado para proyectos académicos y reales.

### Backend / API

**Tecnología:** Python + FastAPI\
**Decisión:** Centralizar toda la lógica de negocio en el backend\
**Justificación:**

* Seguridad (roles y permisos).
* Validaciones y control de acceso consistentes.
* Facilita pruebas y mantenimiento.

### Base de datos

**Tecnología:** MySQL (relacional)\
**Decisión:** Modelo relacional normalizado\
**Justificación:**

* Relaciones claras (usuarios, equipos, partidos…).
* Integridad referencial.
* Fácil de justificar académicamente.
* Adecuado para datos estructurados.

### Modelo de usuarios y roles

**Decisión:** Sistema desacoplado con tablas `usuarios`, `roles`, `usuarios_roles`\
**Justificación:**

* Un usuario puede tener varios roles.
* Mayor flexibilidad y escalabilidad.
* Control de permisos limpio.\
  **Roles definidos:** Administrador, Entrenador, Delegado de campo, Jugador, Espectador

### Gestión de partidos y eventos

**Decisión:** Registrar sucesos del partido mediante eventos (`partidos`, `eventos_partido`)\
**Justificación:**

* Permite registrar goles, tarjetas, cambios.
* Facilita estadísticas automáticas y historial completo.
* Representación realista del mundo deportivo.

### Gestión táctica (formaciones)

**Decisión:** Modelar formaciones como entidades propias (`formaciones`, `posiciones_formacion`, `formaciones_equipo`, `formaciones_partido`)\
**Justificación:**

* Reutilización de esquemas tácticos.
* Visualización gráfica en la app.
* Asignación real de jugadores a posiciones.
* Diferencial frente a otros proyectos.

### Seguridad y permisos

**Decisión:** Control de acceso basado en autenticación y autorización por rol\
**Justificación:**

* Evita accesos indebidos.
* Cada usuario ve y edita solo lo que le corresponde.
* Facilita mantenimiento y auditoría.

### Organización del desarrollo

**Decisión:** Desarrollo incremental basado en MVP\
**Justificación:**

* Garantiza una versión funcional mínima.
* Reduce riesgos y permite ampliaciones progresivas.
* Facilita entregas parciales aunque falte tiempo.
