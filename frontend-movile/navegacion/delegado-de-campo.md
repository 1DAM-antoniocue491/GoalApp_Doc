# Delegado de Campo

El rol de delegado de campo una vez registrado e iniciado sesión permitirá registrar eventos en los partidos.



1. **Estructura de navegación.**

El apartado de _MainTabs_, disponible en modo completo para usuarios autenticados, que contiene las secciones principales de la aplicación: _Dashboard_, _Liga_, _Partidos_ y _Perfil_. Estas secciones permiten al usuario navegar entre los distintos apartados de forma sencilla mediante una barra de navegación.

```
Root
└── MainTabs (modo completo)
    ├── Dashboard
    ├── Liga
    ├── Partidos
    └── Perfil
        └── Editar perfil
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

<figure><img src="../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

* **Dashboard**.  Al iniciar sesión, el usuario accede al _Dashboard_, que funciona como pantalla principal.  Si queremos ver todos los partidos programados, debemos pulsar en el apartado “Ver todo”. Del mismo modo, para consultar los partidos en directo, es necesario pulsar el botón “En directo”.&#x20;

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1) (1).png" alt="" width="155"><figcaption></figcaption></figure>

* **Liga.**&#x44;esde la sección _Liga_,  al seleccionar un equipo específico, se accede a su _detalle_, mostrando la información del equipo. Lo mismo ocurre si seleccionamos a un jugador.&#x20;

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

*   **Partido**: Dentro de esta sección, tendremos un tabs del estado en el que se encuentran los partidos (Directo, Programado, Finalizado) de la liga escogida.&#x20;

    * &#x20;**Directo**. Consultar los partidos en directo y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación de los equipos. Además, permitirás crear eventos del partido (goles, tarjetas, sustituciones, MVP), finalizar el evento y editar eventos.

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

    * **Programado**. Consultar los partidos que se encuentrarn programados y, al seleccionar el que nos interese, acceder tanto a sus encentros anteriores como a la convocatoria del partido. Además, permitirás poner en directo el partido.

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>
*   **Finalizado**.  Consultar los partidos que se encuentrarn finalizados y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación del partido.

    <figure><img src="../../.gitbook/assets/image (2) (1).png" alt="" width="375"><figcaption></figcaption></figure>



* **Perfil**: Los campos se han rellenado cuando el usuario se ha registrado. Además, podremos modificar los datos personales una vez iniciados en la aplicación.

<figure><img src="../../.gitbook/assets/image (3).png" alt="" width="297"><figcaption></figcaption></figure>

5. **Tabs principales.**

* **Dashboard:** Se trata de la pantalla de inicio de la aplicación, que permite visualizar la información más importante sobre la liga.
* **Liga:** Se consulta la clasificación de la liga con las estadísticas de todos los equipos que la forman
* **Partido**: Consulta el estado de los partidos (directo, programado, finalizado).&#x20;
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

7. **Eventos.**

Para observar los eventos que tenemos podemos ir:

```
Partidos → En directo → Partido → Elipsis → Mis Evento
```

Vemos los eventos que tenemos y podemos modificarlos e incluso eliminarlos si es conveniente:

<figure><img src="../../.gitbook/assets/image (4).png" alt="" width="154"><figcaption></figcaption></figure>

En el caso de que queramos crear un evento pulsamos en '+', escogemos el evento y nos dirigira al evento que hemos seleccionado:

<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

8. **Estado Partidos.**

Los partidos pueden modificarse para cambiar el estado en el que se encuentran (en directo, programado o finalizado).

```
Partidos → En directo → Partido → Elipsis → Estado
Partidos → Programado → Partido → Elipsis → Estado
Partidos → Finalizado → Partido → Elipsis → Estado
```

Todas las pantallas redigiran a cambiar estado Partido, una ver seleccionado pulsaremos el botón de 'Restablecer Estado':

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt="" width="127"><figcaption></figcaption></figure>



9. **Restricciones.**

Las limitaciones que presenta este usuario son:

* No podrá crear ligas de fútbol.
* No podrá crear equipos.
* No podrá asignar roles ni eliminarlos.
* No podrá consultar estadísticas personales de un jugador.
* No podrá añadir alineación.
* No podrá añadir convocatoria.
