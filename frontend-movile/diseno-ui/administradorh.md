# Administrador

El administrador tiene acceso a diferentes herramientas que le facilitan la gestión de la liga y el mantenimiento de la información actualizada.&#x20;

1. **Navegación principal.**

La aplicación incluira una barra de navegación persistente con las siguientes secciones:

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

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

El **onboarding** es la primera sección que aparece después del login o del registro. El onboarding será el mismo para todos los usuarios sin importar el rol.\
Su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

{% columns %}
{% column %}
Desde aquí el usuario puede:

* **Crear una nueva liga.**
* **Editar una liga** si tiene permisos.
* **Unirse a una liga existente** mediante código.
* **Consultar sus ligas.**
* **Filtrarlas** por estado.
* **Entrar** en una liga.
* **Reactivar** una liga finalizada.
* **Seleccionar favoritas.**
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.

3. **Dashboard (Inicio)**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

La **base visual** es la misma para todos los usuarios, pero las acciones disponibles cambian según su nivel de permiso.

{% columns %}
{% column %}


El objetivo del dashboard es ofrecer a cada usuario una vista inicial adaptada a su rol para que pueda:

* **Consultar información** general sobre la liga.
* **Actuar sobre los partidos** si tiene permisos.
* **Acceder rápidamente a la información** más relevante.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



Los roles contemplados en esta sección son:

* **Administrador**
* **Delegado de campo**
* **Entrenador**
* **Jugador / Observador.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.



{% columns %}
{% column %}
El **objetivo** de esta pantalla Jornada es:

* **Visualizar encuentros según su estado** (en vivo, programado o finalizado).
* **Iniciar encuentros** según el rol.
* **Trabajar sobre convocatoria** del partido.
* **Crear partidos manualmente.**
* **Generar el calendario automáticamente.**
* **Editar y elimina tanto el calendario como partidos** concretos.
* **Crear Equipos.**
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}





{% columns %}
{% column valign="middle" %}
El **objetivo** de esta pantalla Equipos es:

* **Crear partidos manualmente.**
* **Generar el calendario automáticamente.**
* **Editar y eliminar el calendario**.
* **Editar información de equipos.**
* **Crear Equipos.**
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}





{% columns %}
{% column valign="middle" %}
El **objetivo** de esta pantalla Clasificación es:

* **Crear partidos manualmente.**
* **Generar el calendario automáticamente.**
* **Editar y eliminar el calendario**.
* **Visualizar la clasificación.**
* **Crear Equipos.**


{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



3. **Añadir.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación. Pueden hacerse desde dos formas diferentes:

* **Generar código:** Se generará un código asociado al rol seleccionado, el cual podrá compartirse con el usuario que se desea invitar para que forme parte de la liga.
* **Invitar al usuario**: Mediante invitaciones por correo electrónico. Sin embargo, debido a la falta de tiempo durante el desarrollo del proyecto, esta funcionalidad no ha podido implementarse completamente.

{% columns %}
{% column valign="middle" %}
El objetivo principal de add es:

* **Añadir usuarios y roles.**
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

&#x20;

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



{% columns %}
{% column valign="middle" %}


El **objetivo** principal de esta pantalla es:

* **Ver la información personal**.
* **Editar los datos básicos** del usuario.
* **Cerrar la sesión actual.**
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

