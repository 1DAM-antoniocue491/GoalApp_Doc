# Modelo de datos

El modelo de datos está compuesto por un conjunto de tablas que representan las entidades principales del sistema y sus relaciones. Cada tabla cumple un propósito específico dentro de la gestión de usuarios, equipos, ligas, partidos y estadísticas. A continuación se describen las tablas principales y su función dentro del sistema.

### **2.1 Usuarios y Roles**

#### **usuarios**

Tabla que almacena la información de todos los usuarios registrados en la aplicación.

Incluye:

* Datos personales básicos.
* Credenciales de acceso (con contraseña en hash).
* Información de auditoría.
* Estado del usuario (activo/inactivo).

Su función es servir como entidad base para todos los perfiles del sistema (jugadores, entrenadores, delegados, administradores).

<table data-full-width="true"><thead><tr><th>Campo</th><th>Tipo</th><th>PK</th><th>FK</th><th>Restricciones</th><th>Descripción</th></tr></thead><tbody><tr><td>id_usuario</td><td>INT</td><td>✔</td><td></td><td>NOT NULL, UNIQUE</td><td>Identificador del usuario</td></tr><tr><td>nombre</td><td>VARCHAR(100)</td><td></td><td></td><td>NOT NULL</td><td>Nombre del usuario</td></tr><tr><td>email</td><td>VARCHAR(100)</td><td></td><td></td><td>NOT NULL, UNIQUE</td><td>Correo electrónico</td></tr><tr><td>contraseña_hash</td><td>VARCHAR(255)</td><td></td><td></td><td>NOT NULL</td><td>Contraseña en hash</td></tr><tr><td>created_at</td><td>TIMESTAMP</td><td></td><td></td><td>NOT NULL</td><td>Fecha de creación</td></tr><tr><td>updated_at</td><td>TIMESTAMP</td><td></td><td></td><td>NOT NULL</td><td>Fecha de actualización</td></tr></tbody></table>

#### **roles**

Contiene los diferentes roles disponibles en el sistema, como:

* Administrador
* Entrenador
* Delegado
* Árbitro
* Usuario estándar

Los roles permiten controlar el acceso a funcionalidades específicas.

#### **usuario\_rol**

Tabla intermedia que implementa la relación **N:N** entre usuarios y roles.

Permite:

* Asignar múltiples roles a un mismo usuario.
* Gestionar permisos de forma flexible.
* Escalar el sistema sin modificar la tabla de usuarios.

### **2.2 Jugadores y Personal Técnico**

#### **jugadores**

Almacena información específica de los jugadores, vinculados directamente a un usuario.

Incluye:

* Posición en el campo.
* Dorsal.
* Equipo al que pertenece.
* Relación 1:1 con la tabla `usuarios`.

Esta tabla permite diferenciar a los jugadores del resto de perfiles del sistema.

### **2.3 Ligas, Equipos y Temporadas**

#### **ligas**

Contiene las ligas disponibles en el sistema, junto con su temporada correspondiente.

Incluye:

* Nombre de la liga.
* Año o temporada.
* Configuración general.

#### **equipos**

Almacena la información de cada equipo registrado.

Incluye:

* Nombre del equipo.
* Liga a la que pertenece.
* Entrenador asignado.
* Delegado asignado.
* Relación con jugadores.

Cada equipo puede tener múltiples jugadores, pero solo un entrenador y un delegado.

### **2.4 Partidos y Eventos**

#### **partidos**

Registra los partidos programados o jugados entre equipos de la misma liga.

Incluye:

* Fecha y hora.
* Equipos participantes.
* Estado del partido (pendiente, en juego, finalizado).
* Resultado final.
* Liga correspondiente.

Es una de las tablas centrales del sistema.

#### **eventos\_partido**

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

### **2.5 Formaciones y Alineaciones**

#### **formaciones**

Define las formaciones tácticas disponibles para los equipos.

Ejemplos:

* 4-3-3
* 4-4-2
* 3-5-2

Incluye:

* Nombre o código de la formación.
* Número de jugadores por línea.

#### **posicion**

Define las posiciones dentro de una formación.

Ejemplos:

* GK (portero)
* CB (central)
* CM (centrocampista)
* ST (delantero)

Cada posición está asociada a una formación.

#### **formacion\_equipo**

Relaciona las formaciones disponibles para un equipo.

Permite:

* Registrar qué formaciones puede utilizar un equipo.
* Preparar alineaciones previas a los partidos.

#### **formacion\_partido**

Define la formación utilizada por un equipo en un partido específico.

Incluye:

* Equipo.
* Partido.
* Formación seleccionada.
* Alineación asociada.

### **2.6 Notificaciones**

#### **notificaciones**

Almacena las notificaciones enviadas a los usuarios dentro de la aplicación.

Incluye:

* Usuario destinatario.
* Tipo de notificación.
* Contenido.
* Estado (leída/no leída).
* Fecha de envío.

### **2.7 Auditoría**

Todas las tablas principales incluyen:

* **created\_at**
* **updated\_at**

Estos campos permiten:

* Registrar cuándo se creó un registro.
* Registrar cuándo se modificó.
* Facilitar trazabilidad y depuración.
