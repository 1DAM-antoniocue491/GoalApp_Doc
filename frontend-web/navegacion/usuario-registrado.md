# Usuario Registrado

El rol de usuario Entrenador dispone de acceso a la gestión de convocatorias de su equipo para cada partido, pudiendo seleccionar a los jugadores disponibles y administrar la lista de participantes. Asimismo, puede definir la alineación titular mediante la asignación del once inicial con el que el equipo comenzará el encuentro.



1. **Estructura de navegación.**



```
```

2. **Navegación Disponible.**

La aplicación incluira una barra de navegación persistente con las siguientes secciones:

* **Inicio:** La **pantalla de Inicio** es la vista principal que aparece una vez que el usuario selecciona una liga. Desde aquí puede ver la información más relevante y acceder a las distintas funcionalidades relacionadas con esa liga.
* **Calendario:** La **pantalla de** **Calendario** se gestiona los encuentros de la liga.
* **Equipos:** La **pantalla de Equipos** muestra todos los equipos que forman parte de la liga mediante una clasificación por puntos y permite crear nuevos equipos.
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
* **Usuarios:** La **pantalla de Usuarios** es la sección donde el usuario puede invitar a otros usuarios a formar parte de la liga, asignándoles distintos roles definidos por el administrador.

<figure><img src="../../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

3. **Comportamiento Global.**

La navegación y las funcionalidades de la aplicación para el rol de usuario Entrenador presentan un comportamiento consistente y adaptado a sus permisos:

* **Acceso según rol y permisos:** El entrenador dispone de acceso a las secciones y funcionalidades habilitadas para la gestión de su equipo dentro de la liga.
* **Gestión y validación de acciones:** El entrenador puede consultar información detallada relacionada con equipos, partidos y jugadores, además de gestionar acciones específicas como convocatorias y alineaciones.



4. **Flujo de usuario.**

El **flujo de usuario** describe cómo se desplaza un usuario autenticado dentro de la aplicación y qué acciones puede realizar en cada sección:

```
Onboarding → Creación Ligas.
Dashboard → Información Liga escogida.
Liga → Detalle de las Jornadas, Equipos y Clasificación.
Añadir → Gestionar Usuarios.
Estadísticas → Ver estadísticas de los Equipos y Jugadores. 
Perfil → Editar perfil / Cerrar sesión
```

**a. Onboarding.**

El **onboarding** su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta. El Onboarding es el **mismo para todos los roles**.

Las funciones de Onboarding son:

* **Crear liga.** Si pulsa **Crear liga**, se abre el modal **Nueva Liga**, donde puede configurar datos como:
  * Nombre de la liga.
  * Temporada.
  * Categoría.
  * Cantidad máxima de partidos.
  * Minutos posibles de los partidos.



{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Cuando confirma la acción, la liga se crea y el usuario queda asociado como **administrador**.

* **Unirme a una liga.** Si pulsa **Unirme**, se abre un modal para introducir un **código de invitación**. Si el código es válido, la liga se añade a su cuenta y tendrá los permisos del rol asignado.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Entrar en una liga.** Si pulsa **Entrar** en una tarjeta, accede directamente al dashboard de esa liga.



{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



* **Reactivar una liga.** Si una liga está en estado **finalizado**, solo el **administrador** puede usar **Reactivar liga**.\
  Cuando la reactiva:
  * La liga vuelve a estar activa.
  * Conserva todos sus datos.
  * Desaparece del filtro **Finalizadas.**
  * Vuelve a **Todas.**
  * La acción principal cambia a **Entrar**.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

**b. Dashboard.**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

* **Volver al onboarding.** El encabezado de la aplicación permite al usuario volver a la pantalla de onboarding mediante el menú desplegable.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

{% columns %}
{% column valign="middle" %}
Debemos pulsar el botón 'Cambiar de liga' para volver al onboarding.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Ver notificaciones.** Al pulsar el icono de la campana en el encabezado, el usuario podrá visualizar todas las notificaciones recibidas más recientes.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

{% columns %}
{% column valign="middle" %}
Para ver todas la notificaciones debemos pulsar en 'Ver todas la notificaciones'.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (148).png" alt="" width="288"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



{% columns %}
{% column %}
Si hubiesemos pulsado en 'Ver todas las notificaciones'  estás estarían organizadas según su tipo (todas, en vivo, resultados, etc.) y su estado (todas,leídas, no leídas).
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Ver plantillas.** Al pulsar 'Ver plantilla', se mostrará una pantalla con las plantillas de los equipos que están disputando el partido.
* **Ver calendarios.** Al pulsar 'Ver calendarios', se redirigirá al usuario a la pestaña de calendario, mostrando los partidos en estado programado.
* **Ver partido programado.**&#x20;
* **Convocatoria.**
* **Alineación Titular.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas.** El usuario con el rol de **Observador** podrá ver todos los partidos que se disputan en la liga:

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

3. **Equipos.**

La **pantalla de Equipos** muestra los diferentes equipos que forman parte de la liga, organizados en una clasificación por puntos según los resultados de los partidos.&#x20;

En la pantalla de Equipos se pueden realizar la siguiente acción:

*   **Información individual de cada equipo:** Al seleccionar un equipo, se mostrará información detallada y específica relacionada con dicho equipo.&#x20;



<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (169).png" alt=""><figcaption></figcaption></figure>

4. **Estadísticas.**

La **pantalla de Estadísticas** muestra de forma detallada la información más relevante de la liga, tanto a nivel de equipos como de jugadores. En esta sección se recopilan y presentan las estadísticas más importantes generadas a lo largo de la competición, permitiendo consultar el rendimiento general de la liga.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**5.Usuarios.**

La página de **Usuarios** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación.

El rol de usuario Observador no dispone de permisos para invitar a nuevos usuarios, por lo que únicamente puede visualizar a los miembros que forman parte de la liga.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

**6. Perfil.**

La pantalla de Perfil es la sección donde el usuario puede consultar y gestionar sus datos personales dentro de la aplicación. Se puede acceder a ella pulsando el icono de perfil situado en la parte derecha del encabezado.

* **Editar perfil:** Al pulsar el botón '**Editar perfil'**, el usuario podrá modificar la información de su cuenta registrada.

{% columns %}
{% column valign="middle" %}


<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt="" width="191"><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Cerrar Sesión.** Al pulsar el botón de 'Cerrar sesión' se mostrará un aviso de confirmación y, si el usuario acepta, será redirigido a la pantalla de inicio de sesión.
