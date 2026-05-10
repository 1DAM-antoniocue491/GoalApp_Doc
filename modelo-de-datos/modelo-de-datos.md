# Modelo de Datos

El modelo de datos de GoalApp implementa una base de datos relacional en **PostgreSQL**, diseñada para garantizar la integridad referencial y la eficiencia en la consulta de estadísticas deportivas.

### **1. Usuarios y Roles**

#### **usuarios**
Almacena la identidad global de todas las personas que interactúan con la plataforma.
- **Campos Clave**: `id_usuario` (PK), `nombre`, `email` (Unique), `contraseña_hash`, `genero` (Enum), `imagen_url`.

#### **roles**
Define los niveles de acceso del sistema.
- **Roles implementados**: `admin`, `coach`, `delegate`, `player`, `viewer`.

#### **usuario_rol**
Tabla intermedia para la relación **N:N** entre usuarios y roles. Permite la asignación de múltiples permisos a un mismo usuario.

#### **usuario_sigue_ligas**
Gestiona la relación de seguimiento entre usuarios y ligas para la personalización del dashboard.

***

### **2. Jugadores y Personal Técnico**

#### **jugadores**
Especialización de la entidad usuario para el ámbito deportivo.
- **Campos Clave**: `id_jugador` (PK), `id_usuario` (FK 1:1), `id_equipo` (FK), `posicion`, `dorsal`, `es_capitan` (Boolean), `activo`.

***

### **3. Ligas y Equipos**

#### **ligas**
Entidad raíz de la competición.
- **Campos Clave**: `id_liga` (PK), `nombre` (No único), `temporada`, `activa` (Boolean), `logo_url`.

#### **configuracion_liga**
Almacena las reglas técnicas de cada competición.
- **Campos**: `min_equipos`, `max_equipos`, `min_convocados`, `max_convocados`, `minutos_partido`, `hora_partidos`.

#### **equipos**
Entidad que agrupa jugadores bajo una misma identidad competitiva.
- **Campos Clave**: `id_equipo` (PK), `nombre`, `escudo_url`, `id_liga` (FK), `id_entrenador` (FK, Nullable), `id_delegado` (FK, Nullable).

***

### **4. Partidos y Eventos**

#### **partidos**
El núcleo de la actividad del sistema.
- **Campos Clave**: `id_partido` (PK), `id_liga` (FK), `id_jornada` (FK), `id_equipo_local` (FK), `id_equipo_visitante` (FK), `fecha`, `estado` (Programado, Jugado, Cancelado), `goles_local`, `goles_visitante`.

#### **evento_partido**
Registro cronológico de lo ocurrido en el campo.
- **Campos Clave**: `id_evento` (PK), `id_partido` (FK), `id_jugador` (FK), `tipo_evento` (Gol, Tarjeta, Cambio, MVP), `minuto`.

#### **jornadas** (Nueva)
Organiza los partidos en bloques temporales o competitivos.
- **Campos**: `id_jornada` (PK), `numero_jornada`, `id_liga` (FK).

***

### **5. Gestión de Plantillas**

#### **convocatoria**
Lista de jugadores seleccionados para un partido específico.
- **Campos**: `id_convocatoria` (PK), `id_partiddo` (FK), `id_jugador` (FK).

#### **alineaciones**
Asignación de jugadores al inicio del encuentro.
- **Campos**: `id_alineacion` (PK), `id_partido` (FK), `id_jugador` (FK), `id_posicion` (String), `titular` (Boolean).

***

### **6. Otros Módulos**

#### **notificaciones**
Sincronización de alertas con el usuario.
- **Campos**: `id_notificacion` (PK), `id_usuario` (FK), `mensaje`, `leida` (Boolean).

#### **invitaciones**
Sistema de acceso controlado mediante códigos.
- **Campos**: `id_invitacion` (PK), `codigo` (Unique), `email`, `id_liga` (FK), `id_rol` (FK), `usada` (Boolean).

#### **token**
Gestión de seguridad para la recuperación de cuentas.
- **Campos**: `id_token` (PK), `id_usuario` (FK), `token`, `fecha_expiracion`.

#### **estado_jugador_partido**
Seguimiento del estado del jugador durante la ejecución de un encuentro.
