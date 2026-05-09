# Admistrador

El administrador tiene el control total de la aplicación. Se encarga de crear y mantener la información actualizada, organizar a los equipos y jugadores, y asegurarse de que todo funcione sin problemas. Además, es quien toma decisiones importantes dentro de la plataforma.

Puede crear ligas, equipos, añadir o eliminar jugadores, publicar convocatorias y alineaciones para los partidos, gestionar calendarios y resultados, y controlar el acceso de los usuarios. También supervisa que no haya errores y que la experiencia de uso sea correcta.



1. **Estructura de navegación.**

El apartado de (tabs), disponible en modo completo para usuarios autenticados, que contiene las secciones principales de la aplicación: _Dashboard_, Calendarios, estadisticas y _Perfil_. Estas secciones permiten al usuario navegar entre los distintos apartados de forma sencilla mediante una barra de navegación.

```
src
└── (tabs)
    ├── _layout.tsx
    ├── add.tsx
    ├── calendar.tsx
    ├── index.tsx
    ├── profile.tsx
    └── statistics.tsx
```

2. **Navegación Disponible.**

Las navegaciones que podemos encontrar en nuestra aplicación a traves de un tabs son:

* **Inicio:** La **pantalla de Inicio** es la vista principal que aparece una vez que el usuario selecciona una liga. Desde aquí puede ver la información más relevante y acceder a las distintas funcionalidades relacionadas con esa liga.
* **Calendario:** La pantalla de **Calendario** mostrara la información de la liga.
  * **Jornada.** Mostraran los distintos equipos de una liga distinguiendose del estado en el que se encuentran (en vivo, programados, finalizados).
  * **Equipos.** Mostraran los distintos equipos que componen la liga.
  * **Clasificación**. Mostrara la clasificación de los equipos que componen la liga.
* **Añadir:** Aparecera una pantalla para **gestionar usuarios**.
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
  * **Equipos**. Ver las estadísticas de los equipos por distintas estadísticas (goles, derrotas, victorias, etc.)
  * **Jugadores**. Ver las estadísticas de los jugadores por distintas estadísticas (goles, MVP, etc.)
* **Perfil:** La **pantalla de perfil** es la sección donde el usuario puede consultar su información personal dentro de la aplicación.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

3. **Comportamiento Global.**

La navegación y las funcionalidades de la aplicación para usuarios autenticados presentan un comportamiento consistente y completo:

* **Sin cabecera:** Dado que el usuario ya ha iniciado sesión, no se muestran mensajes ni botones que inviten a registrarse o iniciar sesión.
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


<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Cuando confirma la acción, la liga se crea y el usuario queda asociado como **administrador**.

* **Editar y eliminar**, desde el cual es posible modificar y actualizar la configuración de la misma e incluso eliminarla. En esta sección se puede editar información adicional relacionada con la liga, permitiendo una gestión más completa y personalizada. Si pulsa en los ajustes de la liga, se abre el modal **Configuración de Liga**, donde puede configurar datos como:
  * Nombre de la liga.
  * Temporada.
  * Categoría.
  * Número mínimo y máximo de equipos.
  * Mínimo y máximo de convocados.
  * Mínimo y máximo de jugadores que forman parte de la plantilla.
  * Duración de los partidos.
  * Cantidad máxima de partidos.

{% columns %}
{% column valign="middle" %}
<div align="center"><figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure></div>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (13).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



* **Unirme a una liga.** Si pulsa **Unirme**, se abre un modal para introducir un **código de invitación**. Si el código es válido, la liga se añade a su cuenta y tendrá los permisos del rol asignado.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<div align="center"><figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure></div>
{% endcolumn %}
{% endcolumns %}

* **Entrar en una liga.** Si pulsa **Entrar** en una tarjeta, accede directamente al dashboard de esa liga.



{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (107).png" alt="" width="188"><figcaption></figcaption></figure>
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
{% column %}
<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

**b. Dashboard.**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

* **Volver al onboarding.** El encabezado de la aplicación permite al usuario regresar a la pantalla de onboarding al ser pulsado.

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

* **Ver notificaciones.** Al pulsar el icono de la campana en el encabezado, el usuario podrá visualizar todas las notificaciones recibidas, organizadas según su tipo (todas, en vivo, resultados, etc.). Para cerrar la pantalla pulsaremos el botón de retroceder.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (112).png" alt="" width="188"><figcaption></figcaption></figure>
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

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.

Dentro de los **tres puntitos** que aparecen en el encabezado, tenemos diferentes opciones para realizar en la aplicación:

* **Nuevo Equipo:** Permite añadir nuevos equipos a la liga al pulsar sobre la opción 'Nuevo Equipo'. Nos paracera un modal con diferentes campos a rellenar:
  * Nombre del equipo.
  * Ciudad.
  * Color.
  * Estadio.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Podemos generar el calendario de dos maneras distintas. Una vez seleccionada una opción, la otra quedará deshabilitada y no podrá escogerse:

* **Crear Calendario:** Permite generar automáticamente un calendario en función de los equipos que formen parte de la liga al pulsar sobre la opción 'Crear Calendario'. Nos paracera un modal con diferentes campos a rellenar:
  * Tipo de Calendario.
  * Fecha de Inicio.
  * Días de Partido.
  * Hora de Inicio.



{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (7) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Nuevo Partido:** Permite generar manualmente un calendario en función de los equipos que formen parte de la liga. Al pulsar sobre la opción 'Nuevo Partido', se mostrará un modal con distintos campos que deberán completarse:
  * Equipo Local.
  * Equipo Visitante.
  * Fecha y Hora.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Una vez creado el calendario podemos modificarlo e incluso eliminarlo:

* **Editar calendario**: Función para gestionar y actualizar los partidos de la liga.  Al pulsar sobre la opción 'Editar calendario', se mostrará un modal con distintos campos que pueden modificarse:
  * Tipo de Calendario.
  * Fecha de Inicio.
  * Días de Partido.
  * Hora de Inicio.

{% columns %}
{% column %}


<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



* **Eliminar calendario**: Función para eliminar todos los partidos de la liga. Al pulsar sobre la opción 'Eliminar calendario', se mostrará un aviso de confirmación para evitar eliminaciones accidentales.:

{% columns %}
{% column %}


<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Toda la información generada estará disponible a través de diferentes pestañas:

* Jornada. Se di
* Equipos. Se mostraran los diferentes equipos que contiene la liga.

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
