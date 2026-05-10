# Diagrama MER

El **Modelo Entidad–Relación (MER)** representa la estructura de la base de datos y las relaciones entre las entidades principales del sistema. Este documento sirve como referencia técnica para comprender la arquitectura de datos de GoalApp.

### **1. Visión General del Modelo**

El sistema se basa en una arquitectura relacional donde la integridad de los datos se garantiza mediante claves foráneas y restricciones de dominio.

**Entidades Principales:**
* Usuarios, Roles y Jugadores
* Ligas y Equipos
* Partidos, Eventos y Jornadas
* Convocatorias y Alineaciones
* Notificaciones e Invitaciones

### **2. Usuarios y Roles**

La gestión de identidades permite una flexibilidad total en la asignación de permisos.

*   **Usuarios $\leftrightarrow$ Roles**: Relación **N:N** mediante la tabla intermedia `usuario_rol`. Un usuario puede desempeñar múltiples funciones (ej. ser Coach y Administrador simultáneamente).
*   **Usuarios $\leftrightarrow$ Jugadores**: Relación **1:1**. Todo jugador debe tener una cuenta de usuario asociada, pero no todo usuario es necesariamente un jugador.

### **3. Ligas, Equipos y Jugadores**

La jerarquía organizativa asegura que la competición sea coherente.

*   **Ligas $\leftrightarrow$ Equipos**: Relación **1:N**. Cada equipo pertenece a una única liga.
*   **Equipos $\leftrightarrow$ Jugadores**: Relación **1:N**. Cada jugador está vinculado a un equipo.
*   **Equipos $\leftrightarrow$ Personal Técnico**: Cada equipo tiene un Entrenador y un Delegado asignados (Usuarios). Estos campos son **opcionales (nullable)** para permitir la creación de equipos antes de asignar la plantilla técnica.

### **4. Partidos y Eventos**

El núcleo operativo del sistema gestiona la ejecución de los encuentros.

*   **Equipos $\leftrightarrow$ Partidos**: Relación **N:N** representada por `id_equipo_local` e `id_equipo_visitante`. Ambos equipos deben pertenecer obligatoriamente a la misma liga.
*   **Ligas $\leftrightarrow$ Partidos**: Relación **1:N**. Los partidos se agrupan por la liga a la que pertenecen.
*   **Jornadas $\leftrightarrow$ Partidos**: Relación **1:N**. Los partidos se organizan cronológicamente en jornadas.
*   **Partidos $\leftrightarrow$ Eventos**: Relación **1:N**. Un partido registra múltiples eventos (goles, tarjetas, cambios, MVP).
*   **Jugadores $\leftrightarrow$ Eventos**: Relación **1:N**. Cada evento está vinculado al jugador que lo protagoniza.

### **5. Convocatorias y Alineaciones**

El proceso de preparación del partido se divide en dos etapas:

*   **Convocatorias**: Relación **1:N** entre Partido y Jugadores. Define la lista de disponibles para el encuentro.
*   **Alineaciones**: Relación **1:N** entre Partido y Jugadores. Define quiénes inician el partido y su posición (almacenada como `String` para flexibilidad táctica).

### **6. Notificaciones e Invitaciones**

El sistema de comunicación y acceso se gestiona mediante:

*   **Usuarios $\leftrightarrow$ Notificaciones**: Relación **1:N**. Cada alerta tiene un único destinatario.
*   **Ligas/Equipos $\leftrightarrow$ Invitaciones**: Relación para gestionar la entrada de nuevos usuarios mediante tokens y códigos específicos por rol.

### **7. Notas sobre la Implementación Técnica**

*   **No Unicidad de Nombre**: A diferencia de otras entidades, el nombre de la `Liga` **no es único**, permitiendo que diferentes administradores creen ligas con nombres similares.
*   **Auditoría**: Todas las tablas principales implementan los campos `created_at` y `updated_at` para trazabilidad completa.
*   **Eliminación de Módulos**: El antiguo sistema de formaciones tácticas (tablas `formaciones`, `posiciones`, etc.) ha sido eliminado en favor de un sistema de alineaciones más flexible.
