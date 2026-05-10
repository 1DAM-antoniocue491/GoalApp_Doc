# Jugador

El rol de jugador una vez registrado e iniciado sesión accederá a una interfaz parecida a la de usuario registrado pero podrá ser convocado para un partido y pertener a la alineación inicial. Además, podrá acceder a sus estadísticas personales.

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

3. **Flujo de usuario.**

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
  * **Ver plantillas.** Al seleccionar la opción '**Ver plantilla'**, se mostrarán los jugadores titulares y suplentes de ambos equipos participantes en el partido.
* **Partidos Programados:** Visualizar partidos programados.

6. **Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.

Toda la información generada estará disponible a través de diferentes pestañas:

*   **Jornada**. Se diferencian por los partidos estados (en vivo, programados, finalizados).

    *   **Partidos en Vivo.** Para los partidos en vivo se podrán hacer las siguientes acciones:



        * **Ver plantillas.** Al seleccionar la opción '**Ver plantilla'**, se mostrarán los jugadores titulares y suplentes de ambos equipos participantes en el partido.


    * **Partidos Programados:** Para los partidos en programados se podrán hacer las siguientes acciones:
      * **Visualizar partidos programados.**


* **Equipos**. Se mostraran los diferentes equipos que contiene la liga.

<figure><img src="../../.gitbook/assets/image (115).png" alt="" width="188"><figcaption></figcaption></figure>

* Clasificación. Permitirá visualizar la clasificación de la liga, ordenada en función de la puntuación obtenida por cada equipo.

<figure><img src="../../.gitbook/assets/image (114).png" alt="" width="188"><figcaption></figcaption></figure>

7. **Añadir.**

El tab de **Add** está diseñado para permitir la asignación de distintos roles a los usuarios dentro de la aplicación. Solo se podrán visualizar los usuarios que forman parte de la liga.

8. **Estadísticas.**

La **pantalla de Estadísticas** muestra de forma detallada la información más relevante de la liga, tanto a nivel de equipos como de jugadores. En esta sección se recopilan y presentan las estadísticas más importantes generadas a lo largo de la competición, permitiendo consultar el rendimiento general de la liga.

Esta pantalla permite al usuario analizar fácilmente la evolución de la liga y comparar el rendimiento entre equipos y jugadores de manera clara y organizada.

<figure><img src="../../.gitbook/assets/image (187).png" alt="" width="188"><figcaption></figcaption></figure>

Además, podrá ver sus estadísticas personales:



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



9. **Restricciones.**

Las limitaciones que presenta este usuario son:

* No podrá crear/ editar/eliminar equipos.
* No podrá asignar roles ni eliminarlos.
* No podra crear/editar/eliminar un evento.
* No podrá editar la liga que se ha unido.
