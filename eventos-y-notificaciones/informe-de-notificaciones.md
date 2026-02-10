# Informe de notificaciones

### Objetivo del sistema de notificaciones

El sistema de notificaciones garantiza que los usuarios reciban información relevante y oportuna sobre los partidos, resultados, estadísticas y cambios administrativos, respetando siempre las reglas de negocio y los permisos definidos por rol. Su función principal es mantener informados a los actores clave sin generar saturación ni ruido innecesario.

### Principios del sistema

* Las notificaciones se envían únicamente cuando la información es relevante para el rol del usuario.
* No se envían notificaciones durante el partido por cada evento.
* La notificación principal se genera **al finalizar el partido**, cuando el resultado y las estadísticas ya están consolidados.
* Los espectadores reciben solo información pública.
* Entrenadores, jugadores y delegados reciben información interna del partido.
* El sistema se apoya en los triggers que recalculan estadísticas y clasificación.

### Tipos de notificaciones

#### Notificaciones automáticas

Generadas por el sistema sin intervención humana.

* Finalización de partido
* Actualización de clasificación
* Actualización de estadísticas
* Cambios de estado de liga
* Eliminación o modificación de partidos o equipos
* Asignación de roles (entrenador, delegado, jugador)

#### Notificaciones públicas

Dirigidas a usuarios básicos/espectadores.

* Resultado final del partido
* Clasificación actualizada
* Próximos partidos
* Eventos destacados (solo información pública)

#### Notificaciones internas

Dirigidas a roles con permisos específicos.

* Informe completo del partido
* Estadísticas de jugadores
* Estadísticas de equipo
* Cambios administrativos relevantes

### Flujo de notificaciones al finalizar un partido

#### 1. Registro de eventos durante el partido

El delegado registra goles, tarjetas o sustituciones. Los triggers actualizan:

* Marcador
* Estadísticas de jugador
* Estadísticas de equipo

#### 2. Cambio de estado del partido

El partido pasa de **EN CURSO** a **FINALIZADO**.

#### 3. Recalculo automático

Los triggers ejecutan:

* Consolidación del resultado
* Recalculo de clasificación
* Actualización de estadísticas globales

#### 4. Generación del informe del partido

El sistema compone un informe con:

* Resultado final
* Lista de eventos
* Estadísticas individuales
* Estadísticas de equipo
* Cambios en la clasificación

#### 5. Envío de notificaciones según rol

**Entrenadores (local y visitante)**

Reciben:

* Informe completo del partido
* Estadísticas de jugadores
* Cambios en clasificación

**Delegado de campo**

Recibe:

* Informe completo
* Validación de eventos registrados

**Jugadores**

Reciben:

* Resultado
* Estadísticas personales
* Estadísticas del equipo

**Usuarios básicos / espectadores**

Reciben:

* Resultado final
* Clasificación actualizada

### Contenido de las notificaciones

#### Entrenadores y delegados

* Resultado final
* Eventos detallados
* Goles, tarjetas, sustituciones
* Estadísticas de cada jugador
* Estadísticas del equipo
* Clasificación actualizada
* Sanciones aplicadas

#### Jugadores

* Resultado
* Sus estadísticas personales
* Estadísticas del equipo

#### Espectadores

* Resultado
* Clasificación

### Integración con reglas de negocio

#### Control por rol

El sistema respeta el RBAC:

* Solo el delegado registra eventos
* Solo entrenadores y delegados reciben información interna
* Jugadores reciben información limitada
* Espectadores solo ven datos públicos

#### Estados de liga y partido

Las notificaciones dependen del estado:

* En **CREADA** o **CONFIGURACIÓN** no se envían avisos deportivos
* En **EN COMPETICIÓN** se activan todas
* En **FINALIZADA** solo se envían avisos de consulta

#### Estadísticas y clasificación

Las notificaciones se envían únicamente cuando:

* El partido finaliza
* La clasificación se recalcula
* Las estadísticas se actualizan

No se envían notificaciones por cada evento individual.

### Arquitectura funcional del sistema de notificaciones

#### Backend

* Generación de notificaciones automáticas
* Validación de roles
* Integración con triggers
* Envío de notificaciones push
* Registro de notificaciones internas

#### Base de datos

Tabla de notificaciones con:

* id
* user\_id
* mensaje
* fecha
* leído

#### Frontend

* Bandeja de notificaciones
* Notificaciones push
* Filtros por tipo
* Acceso directo al informe del partido

### Beneficios del sistema

* Reduce saturación de notificaciones
* Mantiene informados a todos los roles sin ruido
* Aprovecha la lógica automática del sistema
* Profesionaliza la experiencia del usuario
* Facilita la consulta de resultados y estadísticas
* Aumenta la participación de jugadores y espectadores

### Conclusión

El sistema de notificaciones se convierte en un componente esencial del proyecto, alineado con las reglas de negocio, los roles y la lógica automática basada en triggers. Su diseño garantiza que cada usuario reciba la información adecuada en el momento adecuado, sin sobrecargar la experiencia y manteniendo la coherencia operativa de la plataforma.
