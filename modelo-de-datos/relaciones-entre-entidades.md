# Relaciones entre entidades

El modelo de datos de GoalApp se basa en un conjunto de relaciones que garantizan la coherencia del sistema y permiten representar correctamente la estructura de ligas, equipos, usuarios y partidos.

### **1. Usuarios, Roles y Jugadores**

#### **Usuarios y Roles**

* **Tipo**: Relación **N:N**.
* **Implementación**: Mediante la tabla intermedia `usuario_rol`.
* **Lógica**: Un usuario puede tener múltiples roles (ej. Administrador y Coach). Esto permite un sistema de permisos granular.

#### **Usuarios y Jugadores**

* **Tipo**: Relación **1:1**.
* **Lógica**: Cada registro en la tabla `jugadores` debe estar vinculado a un único usuario. No todos los usuarios son jugadores, pero todo jugador es un usuario.

### **2. Ligas, Equipos y Jugadores**

#### **Ligas y Equipos**

* **Tipo**: Relación **1:N**.
* **Lógica**: Una liga contiene múltiples equipos. Cada equipo pertenece estrictamente a una sola liga.

#### **Equipos y Jugadores**

* **Tipo**: Relación **1:N**.
* **Lógica**: Un equipo tiene una plantilla de múltiples jugadores. Cada jugador pertenece a un solo equipo.

#### **Equipos y Personal Técnico**

* **Tipo**: Relación **1:1** (opcional).
* **Lógica**: Cada equipo puede tener asignado un Entrenador (`id_entrenador`) y un Delegado (`id_delegado`). Ambos campos son **nullable**, permitiendo que el equipo exista antes de asignar el personal.

### **3. Partidos y Eventos**

#### **Ligas y Jornadas y Partidos**

* **Tipo**: Relación **1:N**.
* **Lógica**: Los partidos se agrupan por Liga y por Jornada.

#### **Equipos y Partidos**

* **Tipo**: Relación **N:N** (representada por dos claves foráneas).
* **Lógica**: Un partido vincula un `equipo_local` y un `equipo_visitante`. Ambos deben pertenecer a la misma liga.

#### **Partidos y Eventos**

* **Tipo**: Relación **1:N**.
* **Lógica**: Un partido genera múltiples eventos (goles, tarjetas, etc.).

#### **Jugadores y Eventos**

* **Tipo**: Relación **1:N**.
* **Lógica**: Cada evento registra la acción de un jugador específico.

### **4. Convocatorias y Alineaciones**

#### **Partidos y Convocatorias**

* **Tipo**: Relación **1:N**.
* **Lógica**: Para cada partido se crea una lista de jugadores convocados.

#### **Partidos y Alineaciones**

* **Tipo**: Relación **1:N**.
* **Lógica**: Se define la alineación inicial del partido, asignando jugadores a posiciones específicas (almacenadas como texto).

### **5. Comunicación y Acceso**

#### **Usuarios y Notificaciones**

* **Tipo**: Relación **1:N**.
* **Lógica**: Un usuario recibe múltiples notificaciones; cada notificación pertenece a un solo usuario.

#### **Ligas/Equipos y Invitaciones**

* **Tipo**: Relación **1:N**.
* **Lógica**: Las invitaciones permiten vincular un nuevo usuario a una liga o equipo específico con un rol predefinido.

### **6. Auditoría y Consistencia**

Todas las entidades principales implementan el patrón de auditoría mediante los campos `created_at` y `updated_at`, asegurando la trazabilidad de los datos en todo el sistema.



<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>
