# Administrador

El administrador tiene acceso a diferentes herramientas que le facilitan la gestión de la liga y el mantenimiento de la información actualizada.&#x20;

1. **Navegación principal.**

La aplicación incluira una barra de navegación persistente con las siguientes secciones:

* **Iniciar Sesión y Resgistrase:** El registro y el inicio de sesión son procesos fundamentales en la aplicación: el registro permite a un usuario crear una cuenta nueva introduciendo sus datos personales, mientras que el inicio de sesión le permite identificarse con esas credenciales para acceder a las funcionalidades privadas del sistema.
* **Dashboard:** El **Dashboard** es la pantalla principal de la aplicación, a la que accede el usuario después de iniciar sesión. Desde aquí puede gestionar las funciones más importantes de forma rápida y sencilla.
* **Inicio:** La **pantalla de Inicio** es la vista principal que aparece una vez que el usuario selecciona una liga. Desde aquí puede ver la información más relevante y acceder a las distintas funcionalidades relacionadas con esa liga.
* **Calendario:** La **pantalla de** **Calendario** se gestiona los encuentros de la liga.
* **Equipos:** La **pantalla de Equipos** muestra todos los equipos que forman parte de la liga mediante una clasificación por puntos y permite crear nuevos equipos.
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
* **Usuarios:** La **pantalla de Usuarios** es la sección donde el usuario puede invitar a otros usuarios a formar parte de la liga, asignándoles distintos roles definidos por el administrador.

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

2. **Inicio Sesión y Registrarse.**

El registro y el inicio de sesión son procesos fundamentales en la aplicación: el registro permite a un usuario crear una cuenta nueva introduciendo sus datos personales, mientras que el inicio de sesión le permite identificarse con esas credenciales para acceder a las funcionalidades privadas del sistema.

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

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

**b. Registro**

Permitir el alta de nuevos usuarios en la plataforma.

* El usuario completa sus datos básicos.
* Debe confirmar la contraseña.
* Debe aceptar los términos y condiciones.
* Si el formulario es válido, se crea la cuenta.
* Tras el registro exitoso, el usuario accede al sistema y es dirigido al **Onboarding**.

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

3. **Onboarding.**

El **Onboarding** es la pantalla principal de la aplicación, a la que accede el usuario después de iniciar sesión.&#x20;

\
Su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

Desde aquí el usuario puede:

* **crear una nueva liga.**
* **unirse a una liga existente** mediante código.
* **consultar sus ligas.**
* **filtrarlas** por estado.
* **entrar** en una liga.
* **reactivar** una liga finalizada.

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.

3. **Dashboard (Inicio)**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

La **base visual** es la misma para todos los usuarios, pero las acciones disponibles cambian según su nivel de permiso.

El objetivo del dashboard es ofrecer a cada usuario una vista inicial adaptada a su rol para que pueda:

* **Consultar información** general sobre la liga.
* **Editar una liga.**
* **Editar los partidos**.
* **Cambiar el estado** de los partidos
* **Añadir la convocatoria** de los partidos.
* **Acceder rápidamente a la información** más relevante.

<figure><img src="../../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

Los roles contemplados en esta sección son:

* **Administrador**
* **Delegado de campo**
* **Entrenador**
* **Jugador / Observador.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas.**

El **objetivo** de esta pantalla Jornada es:

* **Iniciar encuentros** según el rol.
* **Trabajar sobre convocatoria** del partido.
* **Crear partidos manualmente.**
* **Generar el calendario automáticamente.**
* **Editar y elimina tanto el calendario como partidos** concretos.

<figure><img src="../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

3. **Equipos.**

La **pantalla de Equipos** muestra los diferentes equipos que forman parte de la liga, organizados en una clasificación por puntos según los resultados de los partidos. Además, desde esta sección es posible crear nuevos equipos.

El **objetivo** de esta pantalla es:

* **Visualizar clasificación** de la liga.
* **Añadir nuevos equipos.**

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

4. **Estadísticas.**

La **pantalla de Estadísticas** muestra de forma detallada la información más relevante de la liga, tanto a nivel de equipos como de jugadores. En esta sección se recopilan y presentan las estadísticas más importantes generadas a lo largo de la competición, permitiendo consultar el rendimiento general de la liga.

Esta pantalla permite al usuario analizar fácilmente la evolución de la liga y comparar el rendimiento entre equipos y jugadores de manera clara y organizada.

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>



3. **Usuarios.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación mediante invitaciones enviadas por correo electrónico, facilitando así su incorporación a nuestra liga de una forma más organizada y eficiente. Sin embargo, debido a la falta de tiempo durante el desarrollo del proyecto, esta funcionalidad no ha podido implementarse completamente. Aun así, consideramos que se trata de una característica importante para el futuro de la aplicación, por lo que profundizaremos más en ella en la sección de mejoras futuras, donde se detallarán las posibles ampliaciones y funcionalidades previstas.

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

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
<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
