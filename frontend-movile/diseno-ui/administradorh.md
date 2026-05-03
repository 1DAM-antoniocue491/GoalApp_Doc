# Administrador

El administrador tiene acceso a diferentes herramientas que le facilitan la gestión de la liga y el mantenimiento de la información actualizada.&#x20;

1. **Navegación principal.**

La aplicación incluira una barra de navegación persistente con las siguientes secciones:

* **Iniciar Sesión y Resgistrase:** El registro y el inicio de sesión son procesos fundamentales en la aplicación: el registro permite a un usuario crear una cuenta nueva introduciendo sus datos personales, mientras que el inicio de sesión le permite identificarse con esas credenciales para acceder a las funcionalidades privadas del sistema.
* **Dashboard:** El **Dashboard** es la pantalla principal de la aplicación, a la que accede el usuario después de iniciar sesión. Desde aquí puede gestionar las funciones más importantes de forma rápida y sencilla.
* **Inicio:** La **pantalla de Inicio** es la vista principal que aparece una vez que el usuario selecciona una liga. Desde aquí puede ver la información más relevante y acceder a las distintas funcionalidades relacionadas con esa liga.
* **Calendario:** La pantalla de **Calendario** mostrara la información de la liga.
  * **Jornada.** Mostraran los distintos equipos de una liga distinguiendose del estado en el que se encuentran (en vivo, programados, finalizados).
  * **Equipos.** Mostraran los distintos equipos que componen la liga.
  * **Clasificación**. Mostrara la clasificación de los equipos que componen la liga.
* **Añadir:** Aparecera un menú flotante para añadir partidos, crear calendarios, añadir equipos y gestionar usuarios.
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
  * **Equipos**. Ver las estadísticas de los equipos por distintas estadísticas (goles, derrotas, victorias, etc.)
  * **Jugadores**. Ver las estadísticas de los jugadores por distintas estadísticas (goles, MVP, etc.)
* **Perfil:** La **pantalla de perfil** es la sección donde el usuario puede consultar su información personal dentro de la aplicación.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

2. **Inicio Sesión y Registrarse.**

Sus objetivos principales son:

* Permitir el acceso a usuarios ya registrados.
* Permitir el alta de nuevos usuarios.
* Concentrar ambos flujos en una misma interfaz.
* Mantener la coherencia visual del sistema desde el primer contacto.

**a. Login**

Permitir que un usuario ya registrado acceda a su cuenta mediante sus credenciales.

* El usuario introduce su correo y contraseña.
* El sistema valida las credenciales.
* Si son correctas, accede al sistema.
* Tras autenticarse, el usuario es redirigido al **Onboarding**.

**b. Registro**

Permitir el alta de nuevos usuarios en la plataforma.

* El usuario completa sus datos básicos.
* Debe confirmar la contraseña.
* Debe aceptar los términos y condiciones.
* Si el formulario es válido, se crea la cuenta.
* Tras el registro exitoso, el usuario accede al sistema y es dirigido al **Onboarding**.

3. **Onboarding.**

El **onboarding** es la primera sección que aparece después del login o del registro.\
Su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

Desde aquí el usuario puede:

* **crear una nueva liga.**
* **editar una liga** si tiene permisos.
* **unirse a una liga existente** mediante código.
* **consultar sus ligas.**
* **filtrarlas** por estado.
* **entrar** en una liga.
* **reactivar** una liga finalizada.

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.



3. **Dashboard (Inicio)**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.\
La base visual es la misma para todos los usuarios, pero las acciones disponibles cambian según su nivel de permiso.

El objetivo del dashboard es ofrecer a cada usuario una vista inicial adaptada a su rol para que pueda:

* Consultar el estado general de la liga.
* Actuar sobre los partidos si tiene permisos.
* Revisar resultados recientes.
* Acceder rápidamente a la información más relevante.

Los roles contemplados en esta sección son:

* **Administrador**
* **Delegado de campo**
* **Entrenador**
* **Jugador / Observador.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.

El objetivo de esta pantalla es:

* Visualizar encuentros según su estado (en vivo, programado o finalizado),
* Ver la información por jornadas, equipos y clasificación,
* Iniciar encuentros según el rol,
* Trabajar sobre convocatoria y previa del partido,
* Crear partidos manualmente,
* Generar el calendario automáticamente,
* Editar tanto el calendario como partidos concretos.
* Editar información de equipos.

**a. Resultados Esperados.**

El **administrador** puede generar un calendario automático para toda la liga o crear partidos de forma manual.

Si pulsa **Crear calendario automático**, se abre un modal donde define:

* Tipo de calendario.
* Fecha de inicio.
* Días de partido.
* Hora de los encuentros.

Si ese calendario ya existe, puede abrir **Editar calendario** para actualizar esos parámetros generales.

Si pulsa **Nuevo partido**, se abre un modal de creación manual del partido.\
En este caso debe indicar:

* Equipo local.
* Equipo visitante.
* Fecha.
* Hora.
* Estadio.
* Jornada.

Cuando el partido ha sido creado **manualmente**, su edición es **más completa**, porque permite modificar también:

* Equipo local.
* Equipo visitante.
* Delegado del campo.
* Fecha.
* Hora.
* Estadio.

Cuando el partido ha sido generado por el **calendario automático**, la edición es **más limitada**.\
En ese caso no se modifican los equipos del enfrentamiento, sino solo datos operativos como:

* Fecha.
* Hora.
* Estadio.



3. **Añadir.**

El administrador cuando pulse aparecerá un menú flotante con diferentes opciones:

* Añadir Partido.
* Crear Calendario.
* Añadir Equipo.
* Gestionar Usuarios.

**a. Resultados Esperados.**

* **Añadir partido**: al pulsar esta opción, se abre un modal para la creación manual de un partido, donde se deben indicar los siguientes datos:
  * Equipo local.
  * Equipo visitante.
  * Fecha.
  * Hora.
  * Estadio.
  * Jornada.
* **Crear calendario**: al seleccionar esta opción, se abre un modal en el que se definen los siguientes parámetros:
  * Tipo de calendario.
  * Fecha de inicio.
  * Días de partido.
  * Hora de los encuentros.
* **Añadir equipo**: al pulsar esta opción, se abre un modal para crear un nuevo equipo, donde se deben introducir:
  * Logo,
  * Nombre del equipo.
  * Ciudad.
  * Color.
  * Estadio.
* **Gestionar usuarios**: al seleccionar esta opción, se accede a una pantalla desde la que se pueden invitar nuevos usuarios, indicando:
  * Correo electrónico.
  * Rol dentro de la liga.



4. **Estadísticas**.

La pantalla **Estadísticas** reúne los principales datos de rendimiento de la liga en una sola vista.\
Su estructura general es común para todos los roles, pero cambia en un punto clave: **si el usuario es jugador, aparece además el bloque “Mis estadísticas”** con sus datos personales dentro de la competición.

El objetivo de esta pantalla es permitir al usuario:

* Consultar el estado estadístico de la temporada.
* Identificar a los jugadores y equipos más destacados.
* Revisar tendencias generales de rendimiento.
* Si el usuario es jugador, visualizar también su aportación personal.



5. **Perfil**

El **Perfil** es la sección donde el usuario puede ver y gestionar su información personal dentro de la aplicación.

El objetivo principal de esta pantalla es:

* Ver la información personal.
* Editar los datos básicos del usuario.
* Cerrar la sesión actual.

**a. Comportamiento esperado**

* **Ver Perfil.** Abre un modal con la información personal del usuario en modo consulta.
* **Editar Perfil.** Cambia el modal a modo edición para actualizar los datos permitidos.
* **Guardar.** Guarda los cambios realizados y devuelve el modal al modo visualización.
* **Cancelar**. Descarta los cambios no guardados y vuelve al modo visualización
* **Cerrar la sesión.** Finaliza la sesión del usuario y lo saca del sistema.

**b. Reglas funcionales.**

* El perfil siempre pertenece al **usuario autenticado**..
* El modal puede cerrarse con el icono **X**.
* En modo edición, solo deben poder modificarse los campos habilitados.
* Si el usuario pulsa **Cancelar**, no se aplican cambios.
* Si pulsa **Guardar**, la información se actualiza en su cuenta.
* **Cerrar sesión** debe redirigir al iniciar sesión.

