# Administración

El administrador tiene el control total de la aplicación. Se encarga de crear y mantener la información actualizada, organizar a los equipos y jugadores, y asegurarse de que todo funcione sin problemas. Además, es quien toma decisiones importantes dentro de la plataforma.

Puede crear ligas, equipos, añadir o eliminar jugadores, publicar convocatorias y alineaciones para los partidos, gestionar calendarios y resultados, y controlar el acceso de los usuarios. También supervisa que no haya errores y que la experiencia de uso sea correcta.



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

La navegación y las funcionalidades de la aplicación para usuarios autenticados presentan un comportamiento consistente y completo:

* **Acceso completo según rol y permisos:** Todas las secciones y acciones disponibles en la aplicación se habilitan de acuerdo con el rol del usuario.&#x20;
* **Validación de acciones sensibles:** Permite modificar información del perfil o ver información detallada de equipos, partidos e incluso jugadores.



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

El **onboarding** su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

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

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

{% columns %}
{% column valign="middle" %}
Debemos pulsar el botón 'Cambiar de liga' para volver al onboarding.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (146).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Ver notificaciones.** Al pulsar el icono de la campana en el encabezado, el usuario podrá visualizar todas las notificaciones recibidas más recientes.

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

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

{% column %}


<figure><img src="../../.gitbook/assets/image (149).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Finalizar Partidos en Vivo.** Al seleccionar la opción 'Finalizar', se desplegará un modal para completar la información correspondiente. Tras rellenar todos los datos, el usuario deberá confirmar pulsando 'Finalizar partido'.



*   **Añadir Evento.** Al seleccionar la opción 'Añadir evento', se mostrará un modal que permite elegir entre diferentes tipos de evento, como gol, tarjeta amarilla, tarjeta roja o sustitución



    * **Gol**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente. Además, se dispone de una opción para marcar si se trata de un gol en propia puerta.
    * **Amarilla**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
    * **Roja**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
    * **Sustitución**. Se deberá indicar el equipo responsable del evento, junto con el jugador que abandona el terreno de juego y el que entra en su sustitución.
* **Ver plantillas.** Al pulsar 'Ver plantilla', se mostrará una pantalla con las plantillas de los equipos que están disputando el partido.
* **Ver calendarios.** Al pulsar 'Ver calendarios', se redirigirá al usuario a la pestaña de calendario, mostrando los partidos en estado programado.
* **Ver partido programado.**&#x20;
* **Inicializar Partido.**&#x20;
* **Convocatoria.**
* **Alineación Titular.**



2. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas.**

Dentro de Calendario tenemos diferentes opciones para realizar en la aplicación:

Podemos **generar el calendario** de dos maneras distintas. Una vez seleccionada una opción, la otra quedará deshabilitada y no podrá escogerse:

* **Crear Calendario:** Permite generar automáticamente un calendario en función de los equipos que formen parte de la liga al pulsar sobre la opción 'Crear Calendario'. Nos paracera un modal con diferentes campos a rellenar:
  * Tipo de Calendario.
  * Fecha de Inicio.
  * Días de Partido.
  * Hora de los partidos.



{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



*   **Nuevo Partido:** Permite generar manualmente un calendario en función de los equipos que formen parte de la liga. Al pulsar sobre la opción 'Nuevo Partido', se mostrará un modal con distintos campos que deberán completarse:

    * Equipo Local.
    * Equipo Visitante.
    * Fecha y Hora.







{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (150).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (151).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



* **Nuevo Partido:** Permite generar manualmente un calendario en función de los equipos que formen parte de la liga. Al pulsar sobre la opción 'Crear encuentro', se mostrará un modal con distintos campos que deberán completarse:
  * Equipo Local.
  * Equipo Visitante.
  * Fecha y Hora.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Una vez creado el calendario podemos modificarlo e incluso eliminarlo:

* **Editar calendario**: Función para gestionar y actualizar los partidos de la liga.  Al pulsar sobre la opción 'Editar calendario', se mostrará un modal con distintos campos que pueden modificarse:
  * Tipo de Calendario.
  * Fecha de Inicio.
  * Días de Partido.
  * Hora de Inicio.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Eliminar calendario**: Función para eliminar todos los partidos de la liga. Al pulsar sobre la opción 'Eliminar calendario', se mostrará un aviso de confirmación para evitar eliminaciones accidentales:

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



Si únicamente se desea editar un partido, también es posible hacerlo de forma individual:

* Editar Partido: Debemos pulsar el botón de 'Editar' y nos aparecerá un modal

<figure><img src="../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>





<figure><img src="../../.gitbook/assets/image (115).png" alt="" width="188"><figcaption></figcaption></figure>

* Clasificación. Permitirá visualizar la clasificación de la liga, ordenada en función de la puntuación obtenida por cada equipo.

<figure><img src="../../.gitbook/assets/image (114).png" alt="" width="188"><figcaption></figcaption></figure>

**d. Añadir.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación.

Podrán unir por dos formas diferentes:

* **Generando Codigo.** Debemos pulsar sobre el icono de la llave para que aparezca un modal en el que podremos seleccionar el rol que tendrá el usuario dentro de la liga. Una vez elegido, pulsaremos en 'Generar' y se creará un código de invitación que podrá compartirse con el usuario. Posteriormente, este deberá introducir dicho código en el apartado 'Unirse a liga' del dashboard para acceder a la liga.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Invitar.**

**e. Estadísticas.**



**f. Perfil.**

El perfil es la pantalla donde el usuario puede ver y gestionar sus datos personales dentro de la aplicación.

* **Editar Perfil**. Al seleccionar el icono de editar ubicado en la parte superior derecha, se mostrará una pantalla con los datos del usuario, permitiendo su modificación.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (121).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Cerrar Sesión.** Al pulsar el botón de ‘Cerrar sesión’, se mostrará un aviso de confirmación y, si el usuario acepta, será redirigido a la pantalla de inicio de sesión.

<figure><img src="../../.gitbook/assets/image (123).png" alt="" width="375"><figcaption></figcaption></figure>



3. **Restricciones.**

El administrador no contiene ninguna restricción contiene todos los permisos de la aplicación.
