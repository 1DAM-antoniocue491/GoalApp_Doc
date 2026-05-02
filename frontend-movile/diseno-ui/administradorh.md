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
* **Añadir:** Aparecera un menú flotante para añadir partidos, crear calendarios, añadir equipos y getionar usuarios..
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
  * **Equipos**. Ver las estadísticas de los equipos por distintas estadísticas (goles, derrotas, victorias, etc.)
  * **Jugadores**. Ver las estadísticas de los jugadores por distintas estadísticas (goles, MVP, etc.)
* **Perfil:** La **pantalla de perfil** es la sección donde el usuario puede consultar su información personal dentro de la aplicación.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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

**a. Comportamiento Esperado.**

Cuando el usuario entra al onboarding, ve primero dos acciones principales:

* **Crear liga**
* **Unirme**&#x20;

Debajo aparece el bloque **Mis ligas**, donde puede buscar, filtrar y seleccionar cualquiera de las ligas asociadas a su cuenta.

Si pulsa **Crear liga**, se abre el modal **Nueva Liga**, donde puede configurar datos como:

* Subir logo.
* Nombre de la liga.
* Temporada,
* Categoría,
* Número mínimo y máximo de equipos,
* Mínimo y máximo de convocados,
* Mínimo y máximo de jugadores que forman parte de la plantilla.
* Duración de los partidos,
* Cantidad máxima de partidos.

Cuando confirma la acción, la liga se crea y el usuario queda asociado como **administrador**.

Si el usuario tiene permisos de administración sobre una liga, puede abrir el modal **Editar Liga** para actualizar esa configuración.\
Desde ahí también puede **eliminar la liga** si corresponde.

Si pulsa **Unirme**, se abre un modal para introducir un **código de invitación**.\
Si el código es válido, la liga se añade a su cuenta y después podrá entrar con el rol asignado.

Si pulsa **Entrar** en una tarjeta, accede directamente al dashboard de esa liga.

Si una liga está en estado **finalizado**, solo el **administrador** puede usar **Reactivar liga**.\
Cuando la reactiva:

* La liga vuelve a estar activa.
* Conserva todos sus datos.
* Desaparece del filtro **Finalizadas.**
* Vuelve a **Todas.**
* La acción principal cambia a **Entrar**.

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

a. Resultados Esperados.

Si pulsa **Crear calendario automático**, se abre un modal donde define:

* Tipo de calendario.
* Fecha de inicio.
* Días de partido.
* Hora de los encuentros.



4. **Partidos**.

El administrador podrá visualizar los distintos partidos, claramente diferenciados según su estado: en directo, programados o finalizados.

a.  **Directo.**

Podremos visualizar los partidos que se estén disputando en directo según la liga que seleccionemos. Al pulsar sobre un partido, se mostrarán sus estadísticas (tarjetas amarillas, tarjetas rojas y goles), así como la alineación correspondiente.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Pulsando en los tres puntitos podremos:

* Cambiar Estado. Permite modificar el estado de los partidos (directo, programados y finalizados).
* Añadir Evento. Permite agregar un nuevo evento.
* Añadir Alineación. Permite agregar la alineación del partido.



&#x20;b. **Programados**.

Podremos visualizar los partidos que se encuentren programados según la liga que seleccionemos. Al pulsar sobre un partido, se mostrarán los encuentros anteriores sobre los dos equipos, así como la convocatoria correspondiente. Por último, apareceran con un icono los jugadores que formaran parte del once inicial.

<figure><img src="../../.gitbook/assets/image (83).png" alt="" width="375"><figcaption></figcaption></figure>

Pulsando en los tres puntitos podremos:

* Cambiar Estado. Permite modificar el estado de los partidos (directo, programados y finalizados).
* Añadir Convocatoria. Permite agregar la convocatoria del partido.
* Añadir Alineación. Permite agregar la alineación del partido.

c.  **Finalizados**.

Podremos visualizar los partidos que se encuentren finalizados según la liga que seleccionemos. Al pulsar sobre un partido, se mostrarán sus estadísticas (tarjetas amarillas, tarjetas rojas y goles), así como la alineación correspondiente.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

Pulsando en los tres puntitos podremos:

* Cambiar Estado. Permite modificar el estado de los partidos (directo, programados y finalizados).



5. **Perfil**.

El administrador podrá observar su información personal (email, teléfono, fecha de nacimiento, género) y editar su información.

<figure><img src="../../.gitbook/assets/image (74).png" alt="" width="350"><figcaption></figcaption></figure>

Pulsando en el botón de setting se podrá:

* Cerrar Sesión.
* Roles y Usuarios. Se podrán ver los roles que existen en la aplicación y los usuarios con su rol asignado.
