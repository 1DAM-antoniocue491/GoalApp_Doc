# Consulta y Visibilidad de la Información

Esta sección define las reglas de negocio relacionadas con la visibilidad de la información dentro del sistema y cómo esta visibilidad depende del rol del usuario y del estado de la competición. El objetivo es garantizar que cada usuario acceda únicamente a la información que le corresponde, manteniendo la coherencia, la privacidad y la integridad de los datos.

## **1. Principios generales de visibilidad**

La visibilidad de la información en el sistema depende de tres factores:

1. **El rol del usuario dentro de la liga**
2. **El estado de la liga o del partido**
3. **El nivel de autenticación del usuario**

El sistema garantiza que los datos mostrados estén siempre sincronizados con los resultados, eventos y estadísticas generadas.

## **2. Visibilidad según el tipo de usuario**

### **Usuarios no autenticados (invitados)**

Los usuarios no autenticados solo pueden acceder a información pública:

* Clasificación de la liga
* Resultados de partidos finalizados
* Información básica de equipos (nombre, escudo, colores)
* Calendario de partidos

No pueden acceder a:

* Estadísticas detalladas
* Información interna de equipos
* Convocatorias
* Eventos en tiempo real
* Gestión de equipos o ligas

### **Usuarios autenticados**

Los usuarios autenticados pueden acceder a información adicional según su rol dentro de cada liga.

#### **Jugador**

Puede ver:

* Información de su equipo
* Convocatorias
* Estadísticas personales
* Estadísticas de su equipo
* Calendario y resultados de la liga

No puede ver:

* Gestión de equipos
* Gestión de roles
* Configuración de la liga

#### **Entrenador**

Puede ver y gestionar:

* Convocatorias
* Alineaciones
* Formaciones
* Información interna del equipo
* Estadísticas de sus jugadores

No puede:

* Modificar configuraciones de la liga
* Gestionar otros equipos

#### **Delegado de campo**

Puede:

* Registrar eventos del partido
* Consultar convocatorias
* Ver estadísticas del partido en curso
* Acceder a información interna del equipo

No puede:

* Modificar alineaciones
* Gestionar la liga

#### **Administrador**

Tiene acceso completo a:

* Configuración de la liga
* Gestión de equipos
* Asignación de roles
* Calendario de partidos
* Estadísticas globales
* Información interna de todos los equipos

## **3. Visibilidad según el estado de la liga**

#### **Liga en estado CREADA o CONFIGURACIÓN**

* Solo administradores pueden ver y editar configuraciones internas.
* Entrenadores y delegados pueden ver su equipo si ya han sido asignados.
* Jugadores solo ven información básica si ya pertenecen a un equipo.

#### **Liga en estado EN COMPETICIÓN**

* Toda la información pública está disponible para invitados.
* Entrenadores, delegados y jugadores acceden a información operativa.
* Administradores mantienen acceso completo.

#### **Liga en estado FINALIZADA**

* Toda la información pasa a modo consulta.
* No se permite editar:
  * Equipos
  * Partidos
  * Eventos
  * Estadísticas
* La visibilidad se mantiene según el rol, pero sin permisos de edición.

## **4. Visibilidad según el estado del partido**

#### **Partido PROGRAMADO**

* Invitados pueden ver fecha, hora y equipos.
* Entrenadores y delegados pueden ver convocatorias.
* Administradores pueden modificar fecha y hora.

#### **Partido EN CURSO**

* Invitados pueden ver marcador en tiempo real.
* Delegados pueden registrar eventos.
* Entrenadores pueden ver estadísticas en vivo.
* Administradores pueden supervisar pero no modificar equipos.

#### **Partido FINALIZADO**

* Invitados pueden ver resultado y eventos.
* Todos los roles pueden consultar estadísticas.
* No se permite modificar eventos ni resultados.

## **5. Sincronización de datos**

El sistema garantiza que:

* Los datos mostrados siempre reflejan los eventos registrados.
* La clasificación se actualiza automáticamente tras cada partido finalizado.
* Las estadísticas se recalculan al modificar o eliminar eventos.
* No existen discrepancias entre:
  * Marcador
  * Eventos
  * Estadísticas
  * Clasificación
