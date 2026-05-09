# Jugador

El rol de jugador una vez registrado e iniciado sesión accederá a una interfaz parecida a la de usuario registrado pero ademas le permitirá ver sus propias estadísticas personales.



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

* **Dashboard:** Se trata de la pantalla de inicio de la aplicación, que permite visualizar la información más importante sobre la liga.
*   **Liga:** Mostrara la información de la liga.

    * Clasificación. Consultar la clasificación de la liga según los equipos.
    * Equipo. Clasificaciones según criterios como máximos goleadores, victorias, etc.
    * Jugadores. Clasificaciones de jugadores máximos goleadores, MVP, etc.

    <figure><img src="../../.gitbook/assets/image (43).png" alt="" width="227"><figcaption></figcaption></figure>


*   **Partido**: Consulta el estado de los partidos.&#x20;

    * Directo. Ver los partidos en directo.
    * Programado. Ver los partidos programados.
    * Finalizado. Ver los partidos finalizados.



    <figure><img src="../../.gitbook/assets/image (44).png" alt="" width="203"><figcaption></figcaption></figure>
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

3. **Comportamiento Global.**

La navegación y las funcionalidades de la aplicación para usuarios autenticados presentan un comportamiento consistente y completo:

* **Sin cabecera:**\
  Dado que el usuario ya ha iniciado sesión, no se muestran mensajes ni botones que inviten a registrarse o iniciar sesión.
* **Acceso completo según rol y permisos:**\
  Todas las secciones y acciones disponibles en la aplicación se habilitan de acuerdo con el rol del usuario.&#x20;
* **Validación de acciones sensibles:** Permite modificar información del perfil o ver información detallada de equipos, partidos e incluso jugadores.



4. **Flujo de usuario.**

El **flujo de usuario** describe cómo se desplaza un usuario autenticado dentro de la aplicación y qué acciones puede realizar en cada sección:

```
Dashboard → Información Liga
Liga → Detalle de ligas, equipos y jugadores.
Partidos → Detalle de partido. 
Perfil → Editar perfil / Cerrar sesión
```

* **Dashboard**. Al iniciar sesión, el usuario accede al _Dashboard_, que funciona como pantalla principal. Habrá un apartado donde se podrán ver los partidos en directo y los 3 proximos por disputar. Si queremos ver todos los partidos, debemos pulsar en el apartado “Ver todo”. Del mismo modo, para consultar los partidos en directo, es necesario pulsar el botón “En directo”.

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="155"><figcaption></figcaption></figure>

* **Liga.** Desde la sección _Liga_, el usuario puede ver la clasificación general, estadísticas de los equipos y estadísticas de jugadores. Al seleccionar un equipo específico, se accede a su _detalle_, mostrando la información del equipo. Lo mismo ocurre si seleccionamos a un jugador, con la unica diferencia que el propio jugado podrá observar sus estadísticas. El usuario tendrá la posibilidad de seguir tanto a la liga como al equipo.

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

*   **Partido**: Dentro de esta sección, tendremos un tabs del estado en el que se encuentran los partidos (Directo, Programado, Finalizado) de la liga escogida.&#x20;

    * &#x20;**Directo**. Consultar los partidos en directo y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación de los equipos.

    <figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

    * **Programado**. Consultar los partidos que se encuentrarn programados y, al seleccionar el que nos interese, acceder tanto a sus encentros anteriores como a la convocatoria del partido.

    <figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

    * **Finalizado**.  Consultar los partidos que se encuentrarn finalizados y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación del partido.

    <figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
* **Perfil**: Los campos se han rellenado cuando el usuario se ha registrado. Además, podremos modificar los datos personales una vez iniciados en la aplicación.

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1).png" alt="" width="332"><figcaption></figcaption></figure>

5. **Tabs principales.**

* **Dashboard:** Se trata de la pantalla de inicio de la aplicación, que permite visualizar la información más importante sobre la liga.
* **Liga:** Se consulta la clasificación de la liga con las estadísticas de todos los equipos que la forman
* **Partido**: Consulta el estado de los partidos (directo, programado, finalizado).&#x20;
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

6. **Restricciones.**

Las limitaciones que presenta este usuario son:

* No podrá crear, modificar, eliminar ligas de fútbol.
* No podrá crear, modificar, eliminar equipos.
* No podrá asignar roles, modificar, eliminar ni eliminarlos.
* No podra crear, modificar, eliminar un evento.
* No podrá consultar estadísticas personales de un jugador.
* No podrá cambiar y eliminar el estado de los partidos.
