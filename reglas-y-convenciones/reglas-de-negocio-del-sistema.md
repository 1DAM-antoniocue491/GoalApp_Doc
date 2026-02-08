# Reglas de negocio del sistema

Esta sección define las principales reglas de negocio que rigen el funcionamiento del sistema de gestión de ligas amateur de fútbol. Estas reglas garantizan coherencia en los datos, control de acceso por roles y consistencia en la gestión de ligas, equipos, partidos y estadísticas.

***

### 1. Gestión de usuarios, roles y control de acceso

El sistema implementa un control de acceso basado en roles (RBAC). Todas las acciones disponibles en la plataforma dependen del rol asignado al usuario dentro de cada liga.

* Todo usuario que desee utilizar el sistema debe registrarse.
* Los usuarios no autenticados únicamente podrán acceder a información pública.
* Los usuarios autenticados podrán acceder a funcionalidades en función de su rol.
* Un mismo usuario puede participar en varias ligas, y su rol puede variar en cada una de ellas.
* El acceso a las funcionalidades se define por el rol, no por el usuario en sí.

***

### 2. Asignación de roles dentro de una liga

La asignación de roles se realiza en función de la participación del usuario dentro de una liga y de las acciones administrativas realizadas.

* El creador de una liga adquiere automáticamente el rol de **Administrador** en dicha liga.
* Cuando un administrador asigna un entrenador a un equipo, el usuario adquiere el rol de **Entrenador** en esa liga.
* Cuando un administrador asigna un delegado de campo a un equipo, el usuario adquiere el rol de **Delegado de campo** en esa liga.
* Cuando un usuario es añadido como jugador a un equipo, adquiere el rol de **Jugador** en esa liga.

***

### 3. Gestión de ligas

Las ligas se gestionan mediante un ciclo de vida basado en estados, con el objetivo de garantizar consistencia y evitar modificaciones cuando la competición ya ha comenzado.

#### 3.1 Estados de la liga

Una liga puede encontrarse en uno de los siguientes estados:

* **CREADA**: la liga se encuentra creada y es editable.
* **CONFIGURACIÓN**: se añaden equipos y se completan datos previos al inicio.
* **EN COMPETICIÓN**: la liga está activa y se disputan partidos.
* **FINALIZADA**: la liga se encuentra cerrada y queda disponible únicamente en modo consulta.

#### 3.2 Reglas de transición

* Una liga debe tener al menos **dos equipos** registrados para poder pasar al estado **EN COMPETICIÓN**.
* Una vez iniciada la competición:
  * No se permite añadir ni eliminar equipos.
  * No se permite modificar reglas o configuraciones de la liga.
* Una liga solo puede finalizar cuando **todos los partidos estén finalizados**.

***

### 4. Gestión de equipos

Los equipos representan la unidad principal de participación en una liga.

* Un equipo pertenece a una única liga.
* Un equipo debe contar con:
  * **1 entrenador**
  * **1 delegado de campo**
* No es obligatorio asignar entrenador y delegado en el momento de creación, pero sí es obligatorio antes de que el equipo pueda disputar partidos.
* No se permite eliminar un equipo si tiene partidos programados o jugados.

#### 4.1 Restricciones de roles en equipos

* Un usuario no puede ser entrenador de dos equipos distintos dentro de la misma liga.
* Un jugador no puede pertenecer a más de un equipo dentro de la misma liga.

***

### 5. Gestión de jugadores

Los jugadores se gestionan como miembros activos de equipos dentro de una liga.

* Todo jugador debe estar asignado a:
  * Un equipo
  * Una liga
* Un usuario puede participar como jugador en varias ligas, siempre que sea en equipos distintos.
* No se permite registrar eventos de partido (goles, tarjetas o cambios) asociados a jugadores que no estén convocados.

***

### 6. Gestión de partidos

Los partidos constituyen los encuentros oficiales entre equipos dentro de una liga.

* Todo partido pertenece a una liga.
* Un partido siempre enfrenta a dos equipos distintos.
* No se permite modificar la fecha u hora del partido si el partido ya está en curso.
* El resultado final del partido se consolida únicamente cuando el partido pasa a estado finalizado.

#### 6.1 Estados del partido

Un partido puede encontrarse en uno de los siguientes estados:

* **PROGRAMADO**
* **EN CURSO**
* **FINALIZADO**

#### 6.2 Reglas de estado

* Mientras el partido está en estado **PROGRAMADO**, se permite modificar fecha y hora.
* Cuando el partido pasa a **EN CURSO**, se bloquea la edición de los equipos participantes.
* Cuando el partido pasa a **FINALIZADO**, se consolida el resultado y se recalculan clasificación y estadísticas.

***

### 7. Registro de eventos del partido

Los eventos representan acciones ocurridas durante el partido, como goles, tarjetas y cambios.

* Solo el **delegado de campo** puede registrar eventos.
* Todo evento debe incluir:
  * Tipo de evento
  * Minuto de juego
  * Jugador asociado
* No se permite registrar eventos si el partido no se encuentra en estado **EN CURSO**.
* Todo evento debe estar asociado a un jugador convocado para el partido.

#### 7.1 Reglas específicas

* Los goles afectan directamente al marcador del partido.
* Las tarjetas rojas impiden que el jugador continúe recibiendo eventos posteriores según las normas establecidas en la competición.

***

### 8. Clasificación de la liga

La clasificación de la liga se recalcula automáticamente en función de los resultados consolidados.

* La clasificación se recalcula al finalizar cada partido.
* Los puntos se asignan según el resultado:
  * Victoria: **3 puntos**
  * Empate: **1 punto**
  * Derrota: **0 puntos**
* Si se modifica un evento o un resultado, el sistema recalcula la clasificación afectada.

***

### 9. Estadísticas del sistema

Las estadísticas se generan exclusivamente a partir de los eventos registrados durante los partidos.

* No se permite la edición manual de estadísticas.
* Si se elimina o modifica un evento, las estadísticas se recalculan automáticamente.

#### 9.1 Tipos de estadísticas generadas

**Estadísticas de jugador**

* Goles
* Tarjetas
* Partidos jugados

**Estadísticas de equipo**

* Goles a favor
* Goles en contra
* Puntos
* Posición en la clasificación

***

### 10. Consulta y visibilidad de la información

La visibilidad de la información depende del rol del usuario y del estado de la competición.

* Los usuarios invitados únicamente pueden consultar información pública (clasificación y resultados).
* Los usuarios autenticados pueden acceder a información adicional en función de su rol.
* Los datos mostrados por el sistema deben mantenerse sincronizados con resultados y eventos.
