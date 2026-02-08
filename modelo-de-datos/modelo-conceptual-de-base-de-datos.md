# Modelo conceptual de Base de Datos

### 1. Introducción

El proyecto consiste en el desarrollo de una aplicación móvil multiplataforma (Android, iOS y Web) para la gestión de ligas amateur de fútbol.

El modelo de datos tiene como objetivo estructurar toda la información relevante del sistema de manera eficiente y segura, garantizando la integridad de los datos, el control de permisos de usuarios y la posibilidad de realizar consultas avanzadas para estadísticas, clasificaciones y notificaciones.

Esta base de datos servirá como núcleo de la aplicación, soportando la gestión de usuarios, equipos, ligas, partidos, eventos y alineaciones, y permitiendo futuras ampliaciones del sistema.

***

### 2. Alcance

#### Datos almacenados

El modelo de datos abarca:

* Usuarios y roles, con la posibilidad de asignar múltiples roles a un mismo usuario.
* Jugadores, entrenadores y delegados de campo.
* Equipos y ligas, incluyendo temporadas y detalles de cada equipo.
* Partidos y los eventos que ocurren en ellos (goles, tarjetas, cambios, MVP).
* Formaciones tácticas y alineaciones de cada partido.
* Notificaciones para los usuarios.
* Información de auditoría (`created_at`, `updated_at`) para seguimiento de cambios.

#### Datos no almacenados

* Contenido multimedia pesado, como fotos o vídeos de partidos.
* Mensajes privados entre usuarios.
* Historial completo de cambios de estadísticas (solo se almacena el valor final por partido, con posibilidad de extensión futura).

***

### 3. Modelo de Datos

El modelo de datos se compone de las siguientes tablas principales, con sus campos y explicaciones:

#### usuarios

Tabla que almacena información de todos los usuarios registrados en el sistema.

| Campo            | Descripción                     | Tipo de dato | Obligatorio | Único |
| ---------------- | ------------------------------- | ------------ | ----------- | ----- |
| id\_usuario (PK) | Identificador único del usuario | INT          | Sí          | Sí    |
| nombre           | Nombre completo del usuario     | VARCHAR(100) | Sí          | No    |
| email            | Correo electrónico del usuario  | VARCHAR(100) | Sí          | Sí    |
| contraseña\_hash | Contraseña encriptada           | VARCHAR(255) | Sí          | No    |
| created\_at      | Fecha de creación               | TIMESTAMP    | Sí          | No    |
| updated\_at      | Fecha de actualización          | TIMESTAMP    | Sí          | No    |

***

#### roles

Tabla que almacena los diferentes roles que un usuario puede tener (Admin, Entrenador, Delegado, etc.).

| Campo        | Descripción               | Tipo de dato | Obligatorio | Único |
| ------------ | ------------------------- | ------------ | ----------- | ----- |
| id\_rol (PK) | Identificador del rol     | INT          | Sí          | Sí    |
| nombre       | Nombre del rol            | VARCHAR(50)  | Sí          | Sí    |
| descripcion  | Breve descripción del rol | VARCHAR(255) | No          | No    |
| created\_at  | Fecha de creación         | TIMESTAMP    | Sí          | No    |
| updated\_at  | Fecha de actualización    | TIMESTAMP    | Sí          | No    |

***

#### usuario\_rol

Tabla intermedia que relaciona usuarios con roles, permitiendo que un usuario tenga múltiples roles.

| Campo                 | Descripción                  | Tipo de dato | Obligatorio | Único |
| --------------------- | ---------------------------- | ------------ | ----------- | ----- |
| id\_usuario\_rol (PK) | Identificador de la relación | INT          | Sí          | Sí    |
| id\_usuario (FK)      | Usuario asignado             | INT          | Sí          | No    |
| id\_rol (FK)          | Rol asignado                 | INT          | Sí          | No    |
| created\_at           | Fecha de creación            | TIMESTAMP    | Sí          | No    |
| updated\_at           | Fecha de actualización       | TIMESTAMP    | Sí          | No    |

***

#### jugadores

Almacena información específica de los jugadores, incluyendo la posición, dorsal y equipo al que pertenecen. Cada jugador corresponde a un usuario registrado.

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

***

#### ligas

Tabla que contiene las ligas disponibles en el sistema y la temporada correspondiente.

| Campo         | Descripción               | Tipo de dato | Obligatorio | Único |
| ------------- | ------------------------- | ------------ | ----------- | ----- |
| id\_liga (PK) | Identificador de la liga  | INT          | Sí          | Sí    |
| nombre        | Nombre de la liga         | VARCHAR(100) | Sí          | Sí    |
| temporada     | Temporada correspondiente | VARCHAR(20)  | Sí          | No    |
| created\_at   | Fecha de creación         | TIMESTAMP    | Sí          | No    |
| updated\_at   | Fecha de actualización    | TIMESTAMP    | Sí          | No    |

***

#### equipos

Almacena la información de los equipos, su liga, entrenador y delegado.

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

***

#### partidos

Registra los partidos programados o jugados entre equipos de la misma liga, con su estado y resultados.

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

***

#### eventos\_partido

Almacena los eventos ocurridos en un partido, como goles, tarjetas, cambios y MVP.

| Campo            | Descripción                                | Tipo de dato | Obligatorio | Único |
| ---------------- | ------------------------------------------ | ------------ | ----------- | ----- |
| id\_evento (PK)  | Identificador del evento                   | INT          | Sí          | Sí    |
| id\_partido (FK) | Partido asociado                           | INT          | Sí          | No    |
| id\_jugador (FK) | Jugador involucrado                        | INT          | Sí          | No    |
| tipo\_evento     | Tipo de evento (gol, tarjeta, cambio, MVP) | VARCHAR(50)  | Sí          | No    |
| minuto           | Minuto en que ocurrió                      | INT          | Sí          | No    |
| created\_at      | Fecha de creación                          | TIMESTAMP    | Sí          | No    |
| updated\_at      | Fecha de actualización                     | TIMESTAMP    | Sí          | No    |

***

#### formaciones

Define las formaciones tácticas disponibles para los equipos.

| Campo              | Descripción                        | Tipo de dato | Obligatorio | Único |
| ------------------ | ---------------------------------- | ------------ | ----------- | ----- |
| id\_formacion (PK) | Identificador de la formación      | INT          | Sí          | Sí    |
| nombre             | Nombre de la formación (ej. 4-3-3) | VARCHAR(20)  | Sí          | Sí    |
| created\_at        | Fecha de creación                  | TIMESTAMP    | Sí          | No    |
| updated\_at        | Fecha de actualización             | TIMESTAMP    | Sí          | No    |

***

#### posicion

Define las posiciones de cada formación (GK, CB, CM…).

| Campo              | Descripción                  | Tipo de dato | Obligatorio | Único |
| ------------------ | ---------------------------- | ------------ | ----------- | ----- |
| id\_posicion (PK)  | Identificador de la posición | INT          | Sí          | Sí    |
| id\_formacion (FK) | Formación a la que pertenece | INT          | Sí          | No    |
| nombre             | Nombre de la posición        | VARCHAR(50)  | Sí          | No    |
| created\_at        | Fecha de creación            | TIMESTAMP    | Sí          | No    |
| updated\_at        | Fecha de actualización       | TIMESTAMP    | Sí          | No    |

***

#### formacion\_equipo

Relaciona formaciones asignadas a un equipo.

| Campo                      | Descripción            | Tipo de dato | Obligatorio | Único |
| -------------------------- | ---------------------- | ------------ | ----------- | ----- |
| id\_formacion\_equipo (PK) | Identificador          | INT          | Sí          | Sí    |
| id\_equipo (FK)            | Equipo asociado        | INT          | Sí          | No    |
| id\_formacion (FK)         | Formación asignada     | INT          | Sí          | No    |
| created\_at                | Fecha de creación      | TIMESTAMP    | Sí          | No    |
| updated\_at                | Fecha de actualización | TIMESTAMP    | Sí          | No    |

***

#### formacion\_partido

Define qué formación utiliza un equipo en un partido específico.

| Campo                       | Descripción                   | Tipo de dato | Obligatorio | Único |
| --------------------------- | ----------------------------- | ------------ | ----------- | ----- |
| id\_formacion\_partido (PK) | Identificador                 | INT          | Sí          | Sí    |
| id\_partido (FK)            | Partido asociado              | INT          | Sí          | No    |
| id\_equipo (FK)             | Equipo que usará la formación | INT          | Sí          | No    |
| id\_formacion (FK)          | Formación utilizada           | INT          | Sí          | No    |
| created\_at                 | Fecha de creación             | TIMESTAMP    | Sí          | No    |
| updated\_at                 | Fecha de actualización        | TIMESTAMP    | Sí          | No    |

***

#### notificaciones

Almacena notificaciones enviadas a los usuarios.

| Campo                 | Descripción                         | Tipo de dato | Obligatorio | Único |
| --------------------- | ----------------------------------- | ------------ | ----------- | ----- |
| id\_notificacion (PK) | Identificador de la notificación    | INT          | Sí          | Sí    |
| id\_usuario (FK)      | Usuario receptor                    | INT          | Sí          | No    |
| mensaje               | Contenido de la notificación        | TEXT         | Sí          | No    |
| leida                 | Indica si la notificación fue leída | BOOLEAN      | Sí          | No    |
| created\_at           | Fecha de creación                   | TIMESTAMP    | Sí          | No    |
| updated\_at           | Fecha de actualización              | TIMESTAMP    | Sí          | No    |

***

### 4. Diagrama MER de las entidades

#### Roles y usuarios

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Partidos y ligas

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

***

### 5. Relaciones entre entidades

* Cada **usuario** puede tener varios **roles**, mediante la tabla `usuario_rol`.
* Cada **jugador** corresponde a un **usuario** registrado.
* Un **equipo** tiene varios **jugadores**, un **entrenador** y un **delegado**.
* Los **partidos** solo se pueden registrar entre equipos de la misma **liga**.
* Cada **partido** puede tener múltiples **eventos**, y cada **alineación** respeta la **formación** asignada por equipo.

***

### 6. Reglas de negocio

* Un jugador siempre es un usuario.
* Cada equipo tiene entrenador y delegado.
* Los partidos solo pueden registrarse entre equipos de la misma liga.
* Los eventos deben asociarse a un jugador válido y a un partido existente.
* Las alineaciones deben respetar la formación definida para cada partido.

***

### 7. Integridad y consistencia

* Uso de PK y FK en todas las relaciones críticas.
* Eliminaciones en cascada controladas (ej.: eliminar un partido elimina sus eventos y alineaciones asociadas).
* Validaciones `NOT NULL`, `UNIQUE` y `CHECK` para garantizar consistencia.
* Auditoría completa con `created_at` y `updated_at`.

***

### 8. Seguridad

* Contraseñas almacenadas en hash.
* Acceso a información sensible controlado por roles.
* Restricciones de integridad para evitar inconsistencias.

***

### 9. Escalabilidad y mejoras futuras

* Historial completo de estadísticas de jugadores.
* Integración con panel web administrativo.
* Consultas optimizadas para estadísticas y clasificaciones avanzadas.
* Soporte para múltiples temporadas, torneos y ligas simultáneas.
* Predicción de jugador de la jornada mediante IA.
