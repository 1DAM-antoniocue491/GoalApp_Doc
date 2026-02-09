# Equipos y Jugadores

Esta sección define las reglas de negocio relacionadas con la gestión de equipos y jugadores dentro de una liga. Su objetivo es garantizar que la estructura de los equipos sea coherente, que los roles estén correctamente asignados y que los jugadores participen de forma válida en la competición.

## **1. Gestión de Equipos**

Los equipos representan la unidad principal de participación dentro de una liga. Cada equipo debe cumplir una serie de requisitos para poder competir oficialmente.

### **Reglas generales de los equipos**

* Un equipo pertenece **a una única liga**.
* Una liga puede tener múltiples equipos.
* Un equipo debe contar con:
  * **1 entrenador**
  * **1 delegado de campo**
* No es obligatorio asignar entrenador y delegado al crear el equipo, pero **sí antes de disputar partidos**.
* No se permite eliminar un equipo si:
  * Tiene partidos programados, o
  * Tiene partidos jugados.

### **Restricciones de roles dentro de los equipos**

Para garantizar coherencia y evitar conflictos de gestión:

* Un usuario **no puede ser entrenador de dos equipos distintos dentro de la misma liga**.
* Un jugador **no puede pertenecer a más de un equipo dentro de la misma liga**.
* Un usuario puede tener roles distintos en ligas diferentes, pero **no roles incompatibles dentro de la misma liga**.

### **Asignación de roles en equipos**

La asignación de roles dentro de un equipo afecta directamente a los roles RBAC del usuario en la liga:

* Al asignar un **entrenador**, el usuario obtiene el rol de **Entrenador** en esa liga.
* Al asignar un **delegado de campo**, el usuario obtiene el rol de **Delegado de campo** en esa liga.
* Al añadir un **jugador** al equipo, el usuario obtiene el rol de **Jugador** en esa liga.

Estas asignaciones son automáticas y no requieren intervención manual adicional.

## **2. Gestión de Jugadores**

Los jugadores son miembros activos de los equipos y participan directamente en los partidos y estadísticas de la liga.

### **Reglas generales de los jugadores**

* Todo jugador debe estar asignado a:
  * Un equipo
  * Una liga
* Un usuario puede ser jugador en varias ligas, siempre que pertenezca a equipos distintos.
* Un jugador debe estar **activo** para poder participar en partidos.

### **Restricciones de participación**

Para garantizar la validez de los eventos y estadísticas:

* No se permite registrar eventos de partido (goles, tarjetas, cambios) asociados a jugadores que **no estén convocados**.
* Un jugador solo puede recibir eventos si pertenece a uno de los equipos del partido.
* Un jugador expulsado (tarjeta roja) no puede recibir eventos posteriores que contradigan las reglas de la competición.

### **Relación entre jugadores y roles**

* Todo jugador corresponde a un usuario registrado.
* Al añadirse a un equipo, el usuario obtiene automáticamente el rol de **Jugador** en esa liga.
* Un jugador puede tener otros roles simultáneamente (por ejemplo, Delegado), siempre que no contradigan las reglas de la liga.
