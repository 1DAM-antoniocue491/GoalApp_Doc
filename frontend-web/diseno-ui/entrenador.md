# Entrenador

El rol de usuario Entrenador dispone de acceso a la gestión de convocatorias de su equipo para cada partido, pudiendo seleccionar a los jugadores disponibles y administrar la lista de participantes. Asimismo, puede definir la alineación titular mediante la asignación del once inicial con el que el equipo comenzará el encuentro.



1. **Navegación principal.**

La aplicación incluira una barra de navegación persistente con las siguientes secciones:

* **Inicio:** La **pantalla de Inicio** es la vista principal que aparece una vez que el usuario selecciona una liga. Desde aquí puede ver la información más relevante y acceder a las distintas funcionalidades relacionadas con esa liga.
* **Calendario:** La **pantalla de** **Calendario** se gestiona los encuentros de la liga.
* **Equipos:** La **pantalla de Equipos** muestra todos los equipos que forman parte de la liga mediante una clasificación por puntos.
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
* **Usuarios:** La pantalla de Usuarios es la sección donde el usuario puede visualizar a todos los miembros que forman parte de la liga.

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
* asignas ligas **favoritas**.

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.

3. **Dashboard (Inicio)**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

La **base visual** es la misma para todos los usuarios, pero las acciones disponibles cambian según su nivel de permiso.

El objetivo del dashboard es ofrecer a cada usuario una vista inicial adaptada a su rol para que pueda:

* **Consultar información** general sobre la liga.
* **Acceder rápidamente a la información** más relevante.

<figure><img src="../../.gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

El roles contemplado en esta sección es:

* **Entrenador.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas.**

El **objetivo** de esta pantalla Jornada es:

* **Trabajar sobre convocatoria** del partido.

<figure><img src="../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

3. **Equipos.**

La **pantalla de Equipos** muestra los diferentes equipos que forman parte de la liga, organizados en una clasificación por puntos según los resultados de los partidos. Además, desde esta sección es posible crear nuevos equipos.

El **objetivo** de esta pantalla es:

* **Visualizar clasificación** de la liga.

<figure><img src="../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

4. **Estadísticas.**

La **pantalla de Estadísticas** muestra de forma detallada la información más relevante de la liga, tanto a nivel de equipos como de jugadores. En esta sección se recopilan y presentan las estadísticas más importantes generadas a lo largo de la competición, permitiendo consultar el rendimiento general de la liga.

Esta pantalla permite al usuario analizar fácilmente la evolución de la liga y comparar el rendimiento entre equipos y jugadores de manera clara y organizada.

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>



3. **Usuarios.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación.

Podrán unir por dos formas diferentes:

* **Generando Codigo. S**e creará un código de invitación que podrá compartirse con el usuario. Posteriormente, este deberá introducir dicho código en el apartado 'Unirse a liga' del dashboard para acceder a la liga.
* **Invitar.**

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

5. **Perfil**

El **Perfil** es la sección donde el usuario puede ver y gestionar su información personal dentro de la aplicación.

El **objetivo** principal de esta pantalla es:

* **Ver la información personal**.
* **Editar los datos básicos** del usuario.
* **Cerrar la sesión actual.**

<figure><img src="../../.gitbook/assets/image (136).png" alt="" width="255"><figcaption></figcaption></figure>

