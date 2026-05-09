# Modelo de datos

El modelo de datos está compuesto por un conjunto de tablas que representan las entidades principales del sistema y sus relaciones. Cada tabla cumple un propósito específico dentro de la gestión de usuarios, equipos, ligas, partidos y estadísticas. A continuación se describen las tablas principales y su función dentro del sistema.

### **1. Usuarios y Roles**

#### **usuarios**

Tabla que almacena la información de todos los usuarios registrados en la aplicación.

Incluye:

* Datos personales básicos.
* Credenciales de acceso (con contraseña en hash).
* Información de auditoría.
* Estado del usuario (activo/inactivo).

Su función es servir como entidad base para todos los perfiles del sistema (jugadores, entrenadores, delegados, administradores).

<table><thead><tr><th width="116.6666259765625">Campo</th><th>Descripción</th><th>Tipo de dato</th><th>Obligatorio</th><th>Único</th></tr></thead><tbody><tr><td>id_usuario (PK)</td><td>Identificador único del usuario</td><td>INT</td><td>Sí</td><td>Sí</td></tr><tr><td>nombre</td><td>Nombre completo del usuario</td><td>VARCHAR(100)</td><td>Sí</td><td>No</td></tr><tr><td>email</td><td>Correo electrónico del usuario</td><td>VARCHAR(100)</td><td>Sí</td><td>Sí</td></tr><tr><td>contraseña_hash</td><td>Contraseña encriptada</td><td>VARCHAR(255)</td><td>Sí</td><td>No</td></tr><tr><td>genero</td><td>Género del usuario</td><td>VARCHAR (50)</td><td>No</td><td>No</td></tr><tr><td>telefono</td><td>Teléfono del usuario</td><td>VARCHAR(20)</td><td>No</td><td>No</td></tr><tr><td>fecha_nacimiento</td><td>Fecha de nacimento del usuario</td><td>DATE</td><td>No</td><td>No</td></tr><tr><td>imagen_url</td><td>Imagen</td><td>VARCHAR(255)</td><td>NO</td><td>No</td></tr><tr><td>created_at</td><td>Fecha de creación</td><td>TIMESTAMPTZ</td><td>Sí</td><td>No</td></tr><tr><td>updated_at</td><td>Fecha de actualización</td><td>TIMESTAMPTZ</td><td>Sí</td><td>No</td></tr></tbody></table>

#### **usuario sigue ligas**

| Campo               | Descripción           | Tipo de dato | Obligatorio | Único |
| ------------------- | --------------------- | ------------ | ----------- | ----- |
| id\_seguimiento(PK) | Identificador del rol | INT          | Sí          | Sí    |
| id\_usuario (FK)    | usuario asignado      | INT          | Sí          | No    |
| id\_liga            | Liga asignada         | INT          | Sí          | No    |
| created\_at         | Fecha de creación     | TIMESTAMPTZ  | Sí          | No    |

####

#### **roles**

Contiene los diferentes roles disponibles en el sistema, como:

* Administrador
* Entrenador
* Delegado de campo
* Jugador
* Usuario Registrado.
* Usuario sin registrar.

Los roles permiten controlar el acceso a funcionalidades específicas.

| Campo        | Descripción               | Tipo de dato | Obligatorio | Único |
| ------------ | ------------------------- | ------------ | ----------- | ----- |
| id\_rol (PK) | Identificador del rol     | INT          | Sí          | Sí    |
| nombre       | Nombre del rol            | VARCHAR(50)  | Sí          | Sí    |
| descripcion  | Breve descripción del rol | VARCHAR(255) | No          | No    |
| created\_at  | Fecha de creación         | TIMESTAMPTZ  | Sí          | No    |
| updated\_at  | Fecha de actualización    | TIMESTAMPTZ  | Sí          | No    |

#### **usuario\_rol**

Tabla intermedia que implementa la relación **N:N** entre usuarios y roles.

Permite:

* Asignar múltiples roles a un mismo usuario.
* Gestionar permisos de forma flexible.
* Escalar el sistema sin modificar la tabla de usuarios.

| Campo                 | Descripción                  | Tipo de dato | Obligatorio | Único |
| --------------------- | ---------------------------- | ------------ | ----------- | ----- |
| id\_usuario\_rol (PK) | Identificador de la relación | INT          | Sí          | Sí    |
| id\_usuario (FK)      | Usuario asignado             | INT          | Sí          | No    |
| id\_rol (FK)          | Rol asignado                 | INT          | Sí          | No    |
| id\_liga (FK)         | Liga asignada                | INT          | Sí          | No    |
| activo                | Liga activa                  | INT          | Sí          | No    |
| created\_at           | Fecha de creación            | TIMESTAMPTZ  | Sí          | No    |
| updated\_at           | Fecha de actualización       | TIMESTAMPTZ  | Sí          | No    |

### **2. Jugadores y Personal Técnico**

#### **jugadores**

Almacena información específica de los jugadores, vinculados directamente a un usuario.

Incluye:

* Posición en el campo.
* Dorsal.
* Equipo al que pertenece.
* Relación 1:1 con la tabla `usuarios`.

Esta tabla permite diferenciar a los jugadores del resto de perfiles del sistema.

| Campo            | Descripción                        | Tipo de dato | Obligatorio | Único |
| ---------------- | ---------------------------------- | ------------ | ----------- | ----- |
| id\_jugador (PK) | Identificador del jugador          | INT          | Sí          | Sí    |
| id\_usuario (FK) | Usuario asociado                   | INT          | Sí          | Sí    |
| id\_equipo (FK)  | Equipo al que pertenece            | INT          | Sí          | No    |
| posicion         | Posición del jugador               | VARCHAR(50)  | Sí          | No    |
| dorsal           | Número en la camiseta              | INT          | Sí          | No    |
| activo           | Indica si está activo en el equipo | BOOLEAN      | Sí          | No    |
| created\_at      | Fecha de creación                  | TIMESTAMPTZ  | Sí          | No    |
| updated\_at      | Fecha de actualización             | TIMESTAMPTZ  | Sí          | No    |

### **3. Ligas, Equipos y Temporadas**

#### **ligas**

Contiene las ligas disponibles en el sistema, junto con su temporada correspondiente.

Incluye:

* Nombre de la liga.
* Año o temporada.
* Configuración general.

| Campo              | Descripción                     | Tipo de dato | Obligatorio | Único |
| ------------------ | ------------------------------- | ------------ | ----------- | ----- |
| id\_liga (PK)      | Identificador de la liga        | INT          | Sí          | Sí    |
| nombre             | Nombre de la liga               | VARCHAR(100) | Sí          | Sí    |
| temporada          | Temporada correspondiente       | VARCHAR(20)  | Sí          | No    |
| categoria          | Categoria de la liga            | VARCHAR(50)  | No          | No    |
| activa             | Estado de la liga               | BOOLEAN      | Sí          | No    |
| cantidad\_partidos | Cantidad de partidos de la liga | INT          | No          | No    |
| duracion\_partido  | Duración de los partidos        | INT          | No          | No    |
| created\_at        | Fecha de creación               | TIMESTAMPTZ  | Sí          | No    |
| updated\_at        | Fecha de actualización          | TIMESTAMPTZ  | Sí          | No    |

#### configuración de la liga

| Campo                          | Descripción                       | Tipo de dato | Obligatorio | Único |
| ------------------------------ | --------------------------------- | ------------ | ----------- | ----- |
| id\_configuracion (PK)         | Identificador de la liga          | INT          | Sí          | Sí    |
| id\_liga                       | Liga asignada                     | INT          | Sí          | Sí    |
| hora\_partidos                 | Hora del partido                  | TIME         | Sí          | No    |
| min\_equipos                   | Mínimo de equipos                 | INT          | Sí          | No    |
| max\_equipos                   | Máximo de equipos                 | INT          | Sí          | No    |
| min\_convocados                | Mínimo de convocados              | INT          | Sí          | No    |
| max\_convocados                | Máximo de convocados              | INT          | Sí          | No    |
| min\_plantilla                 | Mínimo de jugadores en plantilla  | INT          | Sí          | No    |
| max\_plantilla                 | Máximo de jugadores en plantilla  | INT          | Sí          | No    |
| min\_juadores\_equipo          | Mínimo de jugadores en el equipo  | INT          | Sí          | No    |
| min\_jugadores\_entre\_equipos | Mínimo de jugadores entre equipos | INT          | Sí          | No    |
| minutos\_partido               | Mínutos de partidos               | INT          | Sí          | No    |
| max\_partidos                  | Máximo de partidos                | INT          | Sí          | No    |
| created\_at                    | Fecha de creación                 | TIMESTAMPTZ  | Sí          | No    |
| updated\_at                    | Fecha de actualización            | TIMESTAMPTZ  | Sí          | No    |

#### **equipos**

Almacena la información de cada equipo registrado.

Incluye:

* Nombre del equipo.
* Liga a la que pertenece.
* Entrenador asignado.
* Delegado asignado.
* Relación con jugadores.

Cada equipo puede tener múltiples jugadores, pero solo un entrenador y un delegado.

| Campo               | Descripción                           | Tipo de dato | Obligatorio | Único |
| ------------------- | ------------------------------------- | ------------ | ----------- | ----- |
| id\_equipo (PK)     | Identificador del equipo              | INT          | Sí          | Sí    |
| nombre              | Nombre del equipo                     | VARCHAR(100) | Sí          | Sí    |
| ciudad              | Ciudad del equipo                     | VARCHAR(255) | No          | No    |
| escudo              | URL o referencia al escudo del equipo | VARCHAR(255) | No          | No    |
| colores             | Colores representativos del equipo    | VARCHAR(50)  | No          | No    |
| id\_liga (FK)       | Liga a la que pertenece               | INT          | Sí          | No    |
| id\_entrenador (FK) | Usuario que actúa como entrenador     | INT          | Sí          | No    |
| id\_delegado (FK)   | Usuario que actúa como delegado       | INT          | Sí          | No    |
| estadio             | Nombre del estadio                    | VARCHAR(255) | No          | No    |
| created\_at         | Fecha de creación                     | TIMESTAMPTZ  | Sí          | No    |
| updated\_at         | Fecha de actualización                | TIMESTAMPTZ  | Sí          | No    |

### **4. Partidos y Eventos**

#### **partidos**

Registra los partidos programados o jugados entre equipos de la misma liga.

Incluye:

* Fecha y hora.
* Equipos participantes.
* Estado del partido (pendiente, en juego, finalizado).
* Resultado final.
* Liga correspondiente.

Es una de las tablas centrales del sistema.

| Campo                      | Descripción                    | Tipo de dato | Obligatorio | Único |
| -------------------------- | ------------------------------ | ------------ | ----------- | ----- |
| id\_partido (PK)           | Identificador del partido      | INT          | Sí          | Sí    |
| id\_liga (FK)              | Liga del partido               | INT          | Sí          | No    |
| id\_jornada                | Jornada                        | INT          | Sí          | No    |
| id\_equipo\_local (FK)     | Equipo local                   | INT          | Sí          | No    |
| id\_equipo\_visitante (FK) | Equipo visitante               | INT          | Sí          | No    |
| fecha                      | Fecha y hora del partido       | TIMESTAMPTZ  | Sí          | No    |
| estado                     | Programado, jugado o cancelado | VARCHAR(50)  | Sí          | No    |
| goles\_local               | Goles del equipo local         | INT          | No          | No    |
| goles\_visitante           | Goles del equipo visitante     | INT          | No          | No    |
| created\_at                | Fecha de creación              | TIMESTAMPTZ  | Sí          | No    |
| updated\_at                | Fecha de actualización         | TIMESTAMPTZ  | Sí          | No    |

#### **evento\_partido**

Almacena los eventos ocurridos durante un partido.

Tipos de eventos:

* Gol
* Tarjeta amarilla
* Tarjeta roja
* Cambio
* MVP del partido

Incluye:

* Minuto del evento.
* Jugador involucrado.
* Equipo correspondiente.
* Relación con el partido.

| Campo                | Descripción                                | Tipo de dato | Obligatorio | Único |
| -------------------- | ------------------------------------------ | ------------ | ----------- | ----- |
| id\_convocatoria(PK) | Identificador del evento                   | INT          | Sí          | Sí    |
| id\_partido (FK)     | Partido asociado                           | INT          | Sí          | No    |
| id\_jugador (FK)     | Jugador involucrado                        | INT          | Sí          | No    |
| tipo\_evento         | Tipo de evento (gol, tarjeta, cambio, MVP) | VARCHAR(50)  | Sí          | No    |
| minuto               | Minuto en que ocurrió                      | INT          | Sí          | No    |
| created\_at          | Fecha de creación                          | TIMESTAMPTZ  | Sí          | No    |
| updated\_at          | Fecha de actualización                     | TIMESTAMPTZ  | Sí          | No    |

### **5. Convocatoria y Alineaciones**

#### **convocatoria**

Define la alineaciónes del partido para los equipos.

| Campo               | Descripción                   | Tipo de dato | Obligatorio | Único |
| ------------------- | ----------------------------- | ------------ | ----------- | ----- |
| id\_alineacion (PK) | Identificador de la formación | INT          | Sí          | Sí    |
| id\_partido (FK)    | Partido asignado              | INT          | Sí          | Sí    |
| id\_jugador (FK)    | Jugador asignado              | INT          | Sí          | No    |
| es\_titular         | Estado jugador                | BOOLEAN      | Sí          | No    |
| created\_at         | Fecha de creación             | TIMESTAMPTZ  | Sí          | No    |

#### **alineaciones**

Define la alineaciónes del partido para los equipos.

| Campo               | Descripción                   | Tipo de dato | Obligatorio | Único |
| ------------------- | ----------------------------- | ------------ | ----------- | ----- |
| id\_alineacion (PK) | Identificador de la formación | INT          | Sí          | Sí    |
| id\_partido (FK)    | Partido asignado              | INT          | Sí          | Sí    |
| id\_jugador (FK)    | Jugador asignado              | INT          | Sí          | No    |
| titular             | Estado jugador                | BOOLEAN      | Sí          | No    |
| created\_at         | Fecha de creación             | TIMESTAMPTZ  | Sí          | No    |
| updated\_at         | Fecha de actualización        | TIMESTAMP    | Sí          | No    |

#### **6. Notificaciones**

#### **notificaciones**

Almacena las notificaciones enviadas a los usuarios dentro de la aplicación.

Incluye:

* Usuario destinatario.
* Tipo de notificación.
* Contenido.
* Estado (leída/no leída).
* Fecha de envío.

| Campo                 | Descripción                         | Tipo de dato | Obligatorio | Único |
| --------------------- | ----------------------------------- | ------------ | ----------- | ----- |
| id\_notificacion (PK) | Identificador de la notificación    | INT          | Sí          | Sí    |
| id\_usuario (FK)      | Usuario receptor                    | INT          | Sí          | No    |
| mensaje               | Contenido de la notificación        | TEXT         | Sí          | No    |
| leida                 | Indica si la notificación fue leída | BOOLEAN      | Sí          | No    |
| created\_at           | Fecha de creación                   | TIMESTAMPTZ  | Sí          | No    |
| updated\_at           | Fecha de actualización              | TIMESTAMPTZ  | Sí          | No    |

### **7. Recuperación de contraseña.**

#### token

| Campo             | Descripción                      | Tipo de dato | Obligatorio | Único |
| ----------------- | -------------------------------- | ------------ | ----------- | ----- |
| id\_token (PK)    | Identificador de la notificación | INT          | Sí          | Sí    |
| id\_usuario (FK)  | Usuario receptor                 | INT          | Sí          | No    |
| token             | token                            | VARCHAR(255) | Sí          | Sí    |
| fecha\_expiración | Fecha en caducar                 | TIMESTAMPTZ  | Sí          | No    |
| usado             | Estado                           | BOOLEAN      | Sí          | No    |
| created\_at       | Fecha de creación                | TIMESTAMPTZ  | Sí          | No    |

### **8. Invitar a un usuario.**

Define las invitaciónes de un usuario a una liga:



### **7. Auditoría**

Todas las tablas principales incluyen:

* **created\_at**
* **updated\_at**

Estos campos permiten:

* Registrar cuándo se creó un registro.
* Registrar cuándo se modificó.
* Facilitar trazabilidad y depuración.
