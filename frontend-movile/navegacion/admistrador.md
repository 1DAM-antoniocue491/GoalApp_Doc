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
Perfil → Editar perfil / Cerrar sesió
```

5. **Dashboard.**

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

* **Ver calendario.** Al pulsar en 'Ver calendario' se nos refigirá a calendario a todos los partidos programados de esa liga.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Partidos en Vivo.** Para los partidos en vivo se podrán hacer las siguientes acciones:
  *   **Añadir Evento.** Al seleccionar la opción 'Añadir evento', se mostrará un modal que permite elegir entre diferentes tipos de evento, como gol, tarjeta amarilla, tarjeta roja o sustitución:

      * **Gol**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente. Además, se dispone de una opción para marcar si se trata de un gol en propia puerta.
        * Equipo que produce el evento.
        * Nombre del Jugador.
        * Check en ql caso de que sea gol en propia.
      * **Amarilla**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
        * Equipo que produce el evento.
        * Nombre del Jugador.
        * Minuto en que ocurrio el evento.
        * Motivo.
      * **Roja**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
        * Equipo que produce el evento.
        * Nombre del Jugador.
        * Minuto en que ocurrio el evento.
        * Motivo.
      * **Sustitución**. Se deberá indicar el equipo responsable del evento, junto con el jugador que abandona el terreno de juego y el que entra en su sustitución.
        * Equipo que produce el evento.
        * Nombre del jugador que entra.
        * Nombre del jugador que sale.
        * Minuto en que ocurrio el evento.


  * **Ver plantillas.** Al seleccionar la opción '**Ver plantilla'**, se mostrarán los jugadores titulares y suplentes de ambos equipos participantes en el partido.
  *   **Finalizar partido:** Al seleccionar la opción **“Finalizar”**, se mostrará una ventana modal con la información correspondiente al cierre del partido.

      * Equipo que produce el evento.
      * MVP del partido.
      * Puntución MVP
      * Incidencias.


* **Partidos Programados:** Para los partidos en programados se podrán hacer las siguientes acciones:
  *   **Añadir convocatoria y alineación.** En la misma tarjeta del partido aparece un botón denominado '**Convocatoria'**. Al pulsarlo, se mostrarán todos los usuarios con rol de jugador pertenecientes a ambos equipos, diferenciados entre equipo local y visitante.

      Las distintas opciones disponibles para cada jugador son las siguientes:

      * **Fuera:** El jugador no podrá disputar el partido, ya que no ha sido convocado.
      * **Suplente:** El jugador estará disponible para participar en el encuentro en caso de sustitución.
      * **Titular:** El jugador comenzará el partido formando parte de la alineación inicial.

      Una vez tengamos escogido a todos los jugadores, los cambios podrán ser almacenados pulsando el botón de 'Guardar'.
  *   **Editar.** Pulsamos el botón de **'editar' aparecerá un modal para cambiar:**

      * el estado del partido
      * Fecha de inicio.
      * Hora.


  * **Inicializar Partido.** Pulsando el botón de 'Iniciar' el partido cambiará de estado al 'en vivo'.



6. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.

Dentro de los **tres puntitos** que aparecen en el encabezado, tenemos diferentes opciones para realizar en la aplicación:

* **Nuevo Equipo:** Permite añadir nuevos equipos a la liga al pulsar sobre la opción 'Nuevo Equipo'. Nos paracera un modal con diferentes campos a rellenar:
  * Nombre del equipo.
  * Ciudad.
  * Color.
  * Estadio.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
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
<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Nuevo Partido:** Permite generar manualmente un calendario en función de los equipos que formen parte de la liga. Al pulsar sobre la opción 'Nuevo Partido', se mostrará un modal con distintos campos que deberán completarse:
  * Equipo Local.
  * Equipo Visitante.
  * Fecha y Hora.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
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


<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



* **Eliminar calendario**: Función para eliminar todos los partidos de la liga. Al pulsar sobre la opción 'Eliminar calendario', se mostrará un aviso de confirmación para evitar eliminaciones accidentales.:

{% columns %}
{% column %}


<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Toda la información generada estará disponible a través de diferentes pestañas:

*   **Jornada**. Se diferencian por los partidos estados (en vivo, programados, finalizados).

    * **Partidos en Vivo.** Para los partidos en vivo se podrán hacer las siguientes acciones:
      *   **Añadir Evento.** Al seleccionar la opción 'Añadir evento', se mostrará un modal que permite elegir entre diferentes tipos de evento, como gol, tarjeta amarilla, tarjeta roja o sustitución:

          * **Gol**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente. Además, se dispone de una opción para marcar si se trata de un gol en propia puerta.
            * Equipo que produce el evento.
            * Nombre del Jugador.
            * Minutos que ocurrrio el evento.
          * **Amarilla**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
            * Equipo que produce el evento.
            * Nombre del Jugador.
            * Minuto en que ocurrio el evento.
            * Motivo.
          * **Roja**. La información a completar incluye el equipo que ha generado el evento y el jugador correspondiente.&#x20;
            * Equipo que produce el evento.
            * Nombre del Jugador.
            * Minuto en que ocurrio el evento.
            * Motivo.
          * **Sustitución**. Se deberá indicar el equipo responsable del evento, junto con el jugador que abandona el terreno de juego y el que entra en su sustitución.
            * Equipo que produce el evento.
            * Nombre del jugador que entra.
            * Nombre del jugador que sale.
            * Minuto en que ocurrio el evento.


      * **Ver plantillas.** Al seleccionar la opción '**Ver plantilla'**, se mostrarán los jugadores titulares y suplentes de ambos equipos participantes en el partido.
      *   **Finalizar partido:** Al seleccionar la opción **“Finalizar”**, se mostrará una ventana modal con la información correspondiente al cierre del partido.

          * Equipo que produce el evento.
          * MVP del partido.
          * Puntución MVP
          * Incidencias.


    *   **Partidos Programados:** Para los partidos en programados se podrán hacer las siguientes acciones:

        *   **Añadir convocatoria y alineación.** En la misma tarjeta del partido aparece un botón denominado '**Convocatoria'**. Al pulsarlo, se mostrarán todos los usuarios con rol de jugador pertenecientes a ambos equipos, diferenciados entre equipo local y visitante.

            Las distintas opciones disponibles para cada jugador son las siguientes:

            * **Fuera:** El jugador no podrá disputar el partido, ya que no ha sido convocado.
            * **Suplente:** El jugador estará disponible para participar en el encuentro en caso de sustitución.
            * **Titular:** El jugador comenzará el partido formando parte de la alineación inicial.

            Una vez tengamos escogido a todos los jugadores, los cambios podrán ser almacenados pulsando el botón de 'Guardar'.


    *   **Editar.** Pulsamos el botón de **'editar' aparecerá un modal para cambiar:**

        * el estado del partido
        * Fecha de inicio.
        * Hora.


    * **Inicializar Partido.** Pulsando el botón de 'Iniciar' el partido cambiará de estado al 'en vivo'.


* **Equipos**. Se mostraran los diferentes equipos que contiene la liga.

<figure><img src="../../.gitbook/assets/image (115).png" alt="" width="188"><figcaption></figcaption></figure>

* Clasificación. Permitirá visualizar la clasificación de la liga, ordenada en función de la puntuación obtenida por cada equipo.

<figure><img src="../../.gitbook/assets/image (114).png" alt="" width="188"><figcaption></figcaption></figure>

7. **Añadir.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación.

Podrán unir por dos formas diferentes:

* **Generando Codigo.** Debemos pulsar sobre el icono de la llave para que aparezca un modal en el que podremos seleccionar el rol que tendrá el usuario dentro de la liga. Una vez elegido, pulsaremos en 'Generar' y se creará un código de invitación que podrá compartirse con el usuario. Posteriormente, este deberá introducir dicho código en el apartado 'Unirse a liga' del dashboard para acceder a la liga.&#x20;

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (117).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (118).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

*   **Invitar.** Debemos pulsar el botón '**Invitar'** y seleccionar el rol del usuario que queremos incorporar a la liga. A continuación, se deberá completar la información necesaria según el rol elegido y, finalmente, pulsar nuevamente el botón '**Invitar'** para confirmar la acción.

    Sin embargo, debido a la falta de tiempo durante el desarrollo del proyecto, esta funcionalidad no ha podido implementarse completamente.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

8. **Estadísticas.**

La **pantalla de Estadísticas** muestra de forma detallada la información más relevante de la liga, tanto a nivel de equipos como de jugadores. En esta sección se recopilan y presentan las estadísticas más importantes generadas a lo largo de la competición, permitiendo consultar el rendimiento general de la liga.

Esta pantalla permite al usuario analizar fácilmente la evolución de la liga y comparar el rendimiento entre equipos y jugadores de manera clara y organizada.

<figure><img src="../../.gitbook/assets/image (187).png" alt="" width="188"><figcaption></figcaption></figure>



9. **Perfil.**

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



10. **Restricciones.**

El administrador no contiene ninguna restricción contiene todos los permisos de la aplicación.
