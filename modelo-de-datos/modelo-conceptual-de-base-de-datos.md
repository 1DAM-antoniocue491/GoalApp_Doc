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

***

#### roles

Tabla que almacena los diferentes roles que un usuario puede tener (Admin, Entrenador, Delegado, etc.).

***

#### usuario\_rol

Tabla intermedia que relaciona usuarios con roles, permitiendo que un usuario tenga múltiples roles.

***

#### jugadores

Almacena información específica de los jugadores, incluyendo la posición, dorsal y equipo al que pertenecen. Cada jugador corresponde a un usuario registrado.

***

#### ligas

Tabla que contiene las ligas disponibles en el sistema y la temporada correspondiente.

***

#### equipos

Almacena la información de los equipos, su liga, entrenador y delegado.

***

#### partidos

Registra los partidos programados o jugados entre equipos de la misma liga, con su estado y resultados.

***

#### eventos\_partido

Almacena los eventos ocurridos en un partido, como goles, tarjetas, cambios y MVP.

***

#### formaciones

Define las formaciones tácticas disponibles para los equipos.

***

#### posicion

Define las posiciones de cada formación (GK, CB, CM…).

***

#### formacion\_equipo

Relaciona formaciones asignadas a un equipo.

***

#### formacion\_partido

Define qué formación utiliza un equipo en un partido específico.

***

#### notificaciones

Almacena notificaciones enviadas a los usuarios.

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
