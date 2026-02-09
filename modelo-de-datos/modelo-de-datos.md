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

| Campo            | Descripción                     | Tipo de dato | Obligatorio | Único |
| ---------------- | ------------------------------- | ------------ | ----------- | ----- |
| id\_usuario (PK) | Identificador único del usuario | INT          | Sí          | Sí    |
| nombre           | Nombre completo del usuario     | VARCHAR(100) | Sí          | No    |
| email            | Correo electrónico del usuario  | VARCHAR(100) | Sí          | Sí    |
| contraseña\_hash | Contraseña encriptada           | VARCHAR(255) | Sí          | No    |
| created\_at      | Fecha de creación               | TIMESTAMP    | Sí          | No    |
| updated\_at      | Fecha de actualización          | TIMESTAMP    | Sí          | No    |

#### **roles**

Contiene los diferentes roles disponibles en el sistema, como:

* Administrador
* Entrenador
* Delegado
* Árbitro
* Usuario estándar

Los roles permiten controlar el acceso a funcionalidades específicas.

| Campo        | Descripción               | Tipo de dato | Obligatorio | Único |
| ------------ | ------------------------- | ------------ | ----------- | ----- |
| id\_rol (PK) | Identificador del rol     | INT          | Sí          | Sí    |
| nombre       | Nombre del rol            | VARCHAR(50)  | Sí          | Sí    |
| descripcion  | Breve descripción del rol | VARCHAR(255) | No          | No    |
| created\_at  | Fecha de creación         | TIMESTAMP    | Sí          | No    |
| updated\_at  | Fecha de actualización    | TIMESTAMP    | Sí          | No    |

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
| created\_at           | Fecha de creación            | TIMESTAMP    | Sí          | No    |
| updated\_at           | Fecha de actualización       | TIMESTAMP    | Sí          | No    |

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
| created\_at      | Fecha de creación                  | TIMESTAMP    | Sí          | No    |
| updated\_at      | Fecha de actualización             | TIMESTAMP    | Sí          | No    |

### **3. Ligas, Equipos y Temporadas**

#### **ligas**

Contiene las ligas disponibles en el sistema, junto con su temporada correspondiente.

Incluye:

* Nombre de la liga.
* Año o temporada.
* Configuración general.

| Campo         | Descripción               | Tipo de dato | Obligatorio | Único |
| ------------- | ------------------------- | ------------ | ----------- | ----- |
| id\_liga (PK) | Identificador de la liga  | INT          | Sí          | Sí    |
| nombre        | Nombre de la liga         | VARCHAR(100) | Sí          | Sí    |
| temporada     | Temporada correspondiente | VARCHAR(20)  | Sí          | No    |
| created\_at   | Fecha de creación         | TIMESTAMP    | Sí          | No    |
| updated\_at   | Fecha de actualización    | TIMESTAMP    | Sí          | No    |

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
| escudo              | URL o referencia al escudo del equipo | VARCHAR(255) | No          | No    |
| colores             | Colores representativos del equipo    | VARCHAR(50)  | No          | No    |
| id\_liga (FK)       | Liga a la que pertenece               | INT          | Sí          | No    |
| id\_entrenador (FK) | Usuario que actúa como entrenador     | INT          | Sí          | No    |
| id\_delegado (FK)   | Usuario que actúa como delegado       | INT          | Sí          | No    |
| created\_at         | Fecha de creación                     | TIMESTAMP    | Sí          | No    |
| updated\_at         | Fecha de actualización                | TIMESTAMP    | Sí          | No    |

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
| id\_equipo\_local (FK)     | Equipo local                   | INT          | Sí          | No    |
| id\_equipo\_visitante (FK) | Equipo visitante               | INT          | Sí          | No    |
| fecha                      | Fecha y hora del partido       | TIMESTAMP    | Sí          | No    |
| estado                     | Programado, jugado o cancelado | VARCHAR(50)  | Sí          | No    |
| goles\_local               | Goles del equipo local         | INT          | No          | No    |
| goles\_visitante           | Goles del equipo visitante     | INT          | No          | No    |
| created\_at                | Fecha de creación              | TIMESTAMP    | Sí          | No    |
| updated\_at                | Fecha de actualización         | TIMESTAMP    | Sí          | No    |

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

| Campo            | Descripción                                | Tipo de dato | Obligatorio | Único |
| ---------------- | ------------------------------------------ | ------------ | ----------- | ----- |
| id\_evento (PK)  | Identificador del evento                   | INT          | Sí          | Sí    |
| id\_partido (FK) | Partido asociado                           | INT          | Sí          | No    |
| id\_jugador (FK) | Jugador involucrado                        | INT          | Sí          | No    |
| tipo\_evento     | Tipo de evento (gol, tarjeta, cambio, MVP) | VARCHAR(50)  | Sí          | No    |
| minuto           | Minuto en que ocurrió                      | INT          | Sí          | No    |
| created\_at      | Fecha de creación                          | TIMESTAMP    | Sí          | No    |
| updated\_at      | Fecha de actualización                     | TIMESTAMP    | Sí          | No    |

### **5. Formaciones y Alineaciones**

#### **formaciones**

Define las formaciones tácticas disponibles para los equipos.

{% hint style="success" %}


**Ejemplos:**

* 4-3-3
* 4-4-2
* 3-5-2
{% endhint %}

Incluye:

* Nombre o código de la formación.
* Número de jugadores por línea.

| Campo              | Descripción                        | Tipo de dato | Obligatorio | Único |
| ------------------ | ---------------------------------- | ------------ | ----------- | ----- |
| id\_formacion (PK) | Identificador de la formación      | INT          | Sí          | Sí    |
| nombre             | Nombre de la formación (ej. 4-3-3) | VARCHAR(20)  | Sí          | Sí    |
| created\_at        | Fecha de creación                  | TIMESTAMP    | Sí          | No    |
| updated\_at        | Fecha de actualización             | TIMESTAMP    | Sí          | No    |

#### **posicion**

Define las posiciones dentro de una formación.

{% hint style="success" %}


**Ejemplos:**

* GK (portero)
* CB (central)
* CM (centrocampista)
* ST (delantero)
{% endhint %}

Cada posición está asociada a una formación.

| Campo              | Descripción                  | Tipo de dato | Obligatorio | Único |
| ------------------ | ---------------------------- | ------------ | ----------- | ----- |
| id\_posicion (PK)  | Identificador de la posición | INT          | Sí          | Sí    |
| id\_formacion (FK) | Formación a la que pertenece | INT          | Sí          | No    |
| nombre             | Nombre de la posición        | VARCHAR(50)  | Sí          | No    |
| created\_at        | Fecha de creación            | TIMESTAMP    | Sí          | No    |
| updated\_at        | Fecha de actualización       | TIMESTAMP    | Sí          | No    |

#### **formacion\_equipo**

Relaciona las formaciones disponibles para un equipo.

Permite:

* Registrar qué formaciones puede utilizar un equipo.
* Preparar alineaciones previas a los partidos.

| Campo                      | Descripción            | Tipo de dato | Obligatorio | Único |
| -------------------------- | ---------------------- | ------------ | ----------- | ----- |
| id\_formacion\_equipo (PK) | Identificador          | INT          | Sí          | Sí    |
| id\_equipo (FK)            | Equipo asociado        | INT          | Sí          | No    |
| id\_formacion (FK)         | Formación asignada     | INT          | Sí          | No    |
| created\_at                | Fecha de creación      | TIMESTAMP    | Sí          | No    |
| updated\_at                | Fecha de actualización | TIMESTAMP    | Sí          | No    |

#### **formacion\_partido**

Define la formación utilizada por un equipo en un partido específico.

Incluye:

* Equipo.
* Partido.
* Formación seleccionada.
* Alineación asociada.

| Campo                       | Descripción                   | Tipo de dato | Obligatorio | Único |
| --------------------------- | ----------------------------- | ------------ | ----------- | ----- |
| id\_formacion\_partido (PK) | Identificador                 | INT          | Sí          | Sí    |
| id\_partido (FK)            | Partido asociado              | INT          | Sí          | No    |
| id\_equipo (FK)             | Equipo que usará la formación | INT          | Sí          | No    |
| id\_formacion (FK)          | Formación utilizada           | INT          | Sí          | No    |
| created\_at                 | Fecha de creación             | TIMESTAMP    | Sí          | No    |
| updated\_at                 | Fecha de actualización        | TIMESTAMP    | Sí          | No    |

### **6. Notificaciones**

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
| created\_at           | Fecha de creación                   | TIMESTAMP    | Sí          | No    |
| updated\_at           | Fecha de actualización              | TIMESTAMP    | Sí          | No    |

### **7. Auditoría**

Todas las tablas principales incluyen:

* **created\_at**
* **updated\_at**

Estos campos permiten:

* Registrar cuándo se creó un registro.
* Registrar cuándo se modificó.
* Facilitar trazabilidad y depuración.
