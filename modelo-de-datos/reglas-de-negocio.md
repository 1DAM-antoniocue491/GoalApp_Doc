# Reglas de negocio

Esta sección define las reglas de negocio que rigen el funcionamiento del sistema de gestión de ligas amateur de fútbol. Su objetivo es garantizar coherencia en los datos, control de acceso basado en roles, consistencia en la gestión de ligas, equipos, partidos y estadísticas, y un comportamiento uniforme en toda la plataforma.

Las reglas se agrupan por áreas funcionales para facilitar su comprensión.

## **1. Gestión de Usuarios, Roles y Control de Acceso**

#### **Control de acceso basado en roles (RBAC)**

* El sistema utiliza un modelo RBAC: las acciones permitidas dependen del **rol del usuario dentro de cada liga**.
* Un usuario puede tener **roles distintos en ligas distintas**.
* El acceso se define por el **rol**, no por el usuario en sí.

#### **Autenticación y visibilidad**

* Todo usuario debe registrarse para utilizar el sistema.
* Usuarios no autenticados solo pueden acceder a información pública.
* Usuarios autenticados acceden a funcionalidades según su rol.

#### **Asignación de roles**

Los roles se asignan automáticamente según la participación del usuario en una liga:

* El creador de una liga obtiene el rol **Administrador** en esa liga.
* Al asignar un entrenador a un equipo, el usuario obtiene el rol **Entrenador** en esa liga.
* Al asignar un delegado, obtiene el rol **Delegado de campo**.
* Al añadir un jugador a un equipo, obtiene el rol **Jugador** en esa liga.

#### **Relación con el modelo de datos**

* Un usuario puede tener múltiples roles (tabla `usuario_rol`).
* Un jugador siempre corresponde a un usuario registrado (relación 1:1).

## **2. Gestión de Ligas**

#### **Estados de la liga**

Una liga puede estar en uno de los siguientes estados:

* **CREADA**: editable.
* **CONFIGURACIÓN**: se añaden equipos y datos previos.
* **EN COMPETICIÓN**: partidos activos.
* **FINALIZADA**: solo consulta.

#### **Reglas de transición**

* Una liga debe tener **al menos dos equipos** para pasar a EN COMPETICIÓN.
* Una vez iniciada la competición:
  * No se pueden añadir ni eliminar equipos.
  * No se pueden modificar reglas o configuraciones.
* Una liga solo puede finalizar cuando **todos los partidos estén finalizados**.

#### **Relación con el modelo de datos**

* Los equipos pertenecen a una única liga.
* Los partidos solo pueden registrarse entre equipos de la misma liga.

## **3. Gestión de Equipos**

#### **Estructura del equipo**

Un equipo debe tener:

* 1 entrenador
* 1 delegado de campo

No es obligatorio asignarlos al crear el equipo, pero **sí antes de disputar partidos**.

#### **Restricciones**

* Un usuario **no puede ser entrenador de dos equipos** en la misma liga.
* Un jugador **no puede pertenecer a más de un equipo** en la misma liga.
* No se puede eliminar un equipo si tiene partidos programados o jugados.

#### **Relación con el modelo de datos**

* Un equipo pertenece a una única liga.
* Un equipo tiene múltiples jugadores.
* Entrenador y delegado son usuarios con roles específicos.

## **4. Gestión de Jugadores**

#### **Reglas generales**

* Todo jugador debe estar asignado a:
  * Un equipo
  * Una liga
* Un usuario puede ser jugador en varias ligas, siempre en equipos distintos.

#### **Restricciones en partidos**

* No se pueden registrar eventos asociados a jugadores **no convocados**.
* Un jugador debe pertenecer a uno de los equipos del partido para generar eventos.

#### **Relación con el modelo de datos**

* Cada jugador corresponde a un usuario.
* Cada jugador pertenece a un equipo.

## **5. Gestión de Partidos**

#### **Reglas generales**

* Todo partido pertenece a una liga.
* Un partido enfrenta siempre a **dos equipos distintos**.
* Ambos equipos deben pertenecer a la **misma liga**.

#### **Estados del partido**

* Pendiente
* En juego
* Finalizado

Las transiciones deben ser coherentes con el flujo de competición.

#### **Eventos del partido**

* Cada evento debe asociarse a:
  * Un partido existente
  * Un jugador válido
  * Un equipo participante

Tipos permitidos:

* Gol
* Tarjeta amarilla
* Tarjeta roja
* Cambio
* MVP

## **6. Formaciones y Alineaciones**

#### **Reglas de uso**

* Un equipo solo puede usar formaciones que tenga asignadas (`formacion_equipo`).
* En cada partido, el equipo debe seleccionar una formación (`formacion_partido`).
* La alineación debe respetar:
  * El número de jugadores de la formación.
  * Las posiciones definidas en la formación.

#### **Restricciones**

* No se permite registrar alineaciones sin formación asignada.
* Las posiciones deben coincidir con las definidas en la tabla `posicion`.

## **7. Notificaciones**

#### **Reglas generales**

* Toda notificación debe tener un usuario destinatario válido.
* No se envían notificaciones a usuarios eliminados o inactivos.
* Las notificaciones registran estado (leída/no leída) y fecha de envío.

## **8. Auditoría e Integridad**

#### **Auditoría**

* Todas las tablas principales incluyen:
  * `created_at`
  * `updated_at`

#### **Integridad referencial**

* Eliminación en cascada para:
  * Eventos de un partido eliminado.
  * Alineaciones asociadas a una formación de partido.
* Restricciones NOT NULL, UNIQUE y CHECK para garantizar consistencia.

## **9. Resumen de Reglas Críticas**

* El acceso depende del rol del usuario en cada liga.
* Un jugador siempre es un usuario.
* Un usuario puede tener roles distintos en distintas ligas.
* Los equipos deben tener entrenador y delegado antes de competir.
* Los partidos solo se registran entre equipos de la misma liga.
* Los eventos deben asociarse a jugadores válidos y convocados.
* Las alineaciones deben respetar la formación asignada.
* Las ligas siguen un ciclo de vida con restricciones estrictas.
