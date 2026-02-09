# Relaciones entre entidades

El modelo de datos se basa en un conjunto de relaciones que garantizan la coherencia del sistema y permiten representar correctamente la estructura de ligas, equipos, usuarios y partidos. A continuación se describen las relaciones principales entre las entidades, así como su impacto en la lógica del sistema.

### **1. Usuarios, Roles y Jugadores**

#### **Usuarios ↔ Roles**

> Relación **N:N** mediante la tabla intermedia `usuario_rol`.
>
> Un usuario puede tener múltiples roles (por ejemplo, Entrenador y Delegado).
>
> Un rol puede asignarse a múltiples usuarios.

Esta estructura permite un sistema flexible de permisos y control de acceso.

#### **Usuarios ↔ Jugadores**

> Relación **1:1** entre `usuarios` y `jugadores`.
>
> Cada jugador corresponde a un usuario registrado.
>
> No todos los usuarios son jugadores, pero todos los jugadores son usuarios.

Esto permite que un jugador pueda iniciar sesión, recibir notificaciones y tener un perfil completo.

### **2. Ligas, Equipos y Jugadores**

#### **Ligas ↔ Equipos**

> Relación **1:N**.
>
> Una liga puede tener múltiples equipos.
>
> Cada equipo pertenece a una única liga.

Esto garantiza que los partidos solo se programen dentro de la misma liga.

#### **Equipos ↔ Jugadores**

> Relación **1:N**.
>
> Un equipo puede tener muchos jugadores.
>
> Cada jugador pertenece a un único equipo.

#### **Equipos ↔ Entrenador / Delegado**

> Relación **1:1** con `usuarios` para cada rol.
>
> Cada equipo tiene:
>
> * Un entrenador asignado.
> * Un delegado asignado.

Ambos son usuarios del sistema, pero no necesariamente jugadores.

### **3. Partidos y Eventos**

#### **Equipos ↔ Partidos**

> Relación **N:N**, representada mediante dos FK en `partidos`:
>
> * equipo\_local
> * equipo\_visitante
>
> Ambos equipos deben pertenecer a la misma liga.

#### **Partidos ↔ Eventos**

> Relación **1:N**.
>
> Un partido puede tener múltiples eventos.
>
> Cada evento está asociado a un jugador y a un equipo.

#### **Jugadores ↔ Eventos**

> Relación **1:N**.
>
> Un jugador puede generar múltiples eventos (goles, tarjetas, cambios).
>
> Cada evento debe estar vinculado a un jugador válido.

### **4. Formaciones y Alineaciones**

#### **Formaciones ↔ Posiciones**

> Relación **1:N**.
>
> Una formación define varias posiciones (GK, CB, CM, etc.).

#### **Equipos ↔ Formaciones**

> Relación **N:N** mediante `formacion_equipo`.
>
> Un equipo puede tener varias formaciones disponibles.
>
> Una formación puede ser utilizada por varios equipos.

#### **Partidos ↔ Formaciones**

> Relación **N:N** mediante `formacion_partido`.
>
> Cada equipo selecciona una formación para cada partido.
>
> La alineación debe respetar la formación asignada.

### **5. Notificaciones**

#### **Usuarios ↔ Notificaciones**

> Relación **1:N**.
>
> Un usuario puede recibir múltiples notificaciones.
>
> Cada notificación tiene un único destinatario.

### **6. Auditoría y Consistencia**

Todas las tablas principales incluyen campos de auditoría:

* `created_at`
* `updated_at`

Estas relaciones permiten:

* Trazabilidad de cambios.
* Control de integridad.
* Depuración eficiente.

### **7. Resumen General de Relaciones**

* **Usuarios** se relacionan con **roles**, **jugadores** y **notificaciones**.
* **Jugadores** se relacionan con **equipos**, **partidos** (a través de eventos) y **formaciones** (a través de alineaciones).
* **Equipos** se relacionan con **ligas**, **jugadores**, **entrenadores**, **delegados** y **partidos**.
* **Partidos** se relacionan con **equipos**, **eventos** y **formaciones**.
* **Formaciones** se relacionan con **posiciones**, **equipos** y **partidos**.
