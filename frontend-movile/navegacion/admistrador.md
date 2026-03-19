# Admistrador

El administrador tiene el control total o principal de la aplicación. Se encarga de crear y mantener la información actualizada, organizar a los equipos y jugadores, y asegurarse de que todo funcione sin problemas. Además, es quien toma decisiones importantes dentro de la plataforma.

Por ejemplo, puede crear equipos, añadir o eliminar jugadores, publicar convocatorias y alineaciones para los partidos, gestionar calendarios y resultados, y controlar el acceso de los usuarios. También supervisa que no haya errores y que la experiencia de uso sea correcta.



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


* **Añadir:** Aparecera un menú flotante para añadir jugadores al equipo, equipo, liga, partidos, entrenador y delegado de campo.
*   **Partido**: Consulta el estado de los partidos.&#x20;

    * Directo. Ver los partidos en directo.
    * Programado. Ver los partidos programados.
    * Finalizado. Ver los partidos finalizados.



    <figure><img src="../../.gitbook/assets/image (44).png" alt="" width="203"><figcaption></figcaption></figure>
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

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
Añadir → Añadir jugadores al equipo.
Partidos → Detalle de partido. 
Perfil → Editar perfil / Cerrar sesión
```

* **Dashboard**. Al iniciar sesión, el usuario accede al _Dashboard_, que funciona como pantalla principal. Habrá un apartado donde se podrán ver los partidos en directo y los 3 proximos por disputar. Si queremos ver todos los partidos, debemos pulsar en el apartado “Ver todo”. Del mismo modo, para consultar los partidos en directo, es necesario pulsar el botón “En directo”. Además, contiene un pequeño resumen de la liga(equipos, jugadores, partidos, delegados de campo).

<figure><img src="../../.gitbook/assets/image (52).png" alt="" width="134"><figcaption></figcaption></figure>

* **Liga.** Desde la sección _Liga_, el administrador puede ver la clasificación general, estadísticas de los equipos y estadísticas de jugadores. Al seleccionar un equipo específico, se accede a su _detalle_, mostrando la información del equipo. Lo mismo ocurre si seleccionamos a un jugador. El administrador tendrá la posibilidad de seguir tanto a la liga como al equipo.

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

*   **Partido**: Dentro de esta sección, tendremos un tabs del estado en el que se encuentran los partidos (Directo, Programado, Finalizado) de la liga escogida.&#x20;

    * &#x20;**Directo**. Consultar los partidos en directo y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación de los equipos. Permitirá crear la alineación del partido.

    <figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

    * **Programado**. Consultar los partidos que se encuentrarn programados y, al seleccionar el que nos interese, acceder tanto a sus encentros anteriores como a la convocatoria del partido. Además, permitirá crear la convocatoria del partido y cambiar el estado de los partidos.

    <figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

    * **Finalizado**.  Consultar los partidos que se encuentrarn finalizados y, al seleccionar el que nos interese, acceder tanto a sus estadísticas como a la alineación del partido y cambiar el estado de los partidos.

    <figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
* **Perfil**: Permitirá ver los roles que tenemos y los usuarios registrados en la aplicación.

<figure><img src="../../.gitbook/assets/image (51).png" alt="" width="307"><figcaption></figcaption></figure>

Para ver el perfil del administrador debemos pulsar el icono superior:

<figure><img src="../../.gitbook/assets/image (57).png" alt="" width="301"><figcaption></figcaption></figure>

5. **Tabs principales.**

* **Dashboard:** Se trata de la pantalla de inicio de la aplicación, que permite visualizar la información más importante sobre la liga.
* **Liga:** Se consulta la clasificación de la liga con las estadísticas de todos los equipos que la forman.
* **Añadir:** Permite añadir jugadores a un equipo.
* **Partido**: Consulta el estado de los partidos (directo, programado, finalizado).&#x20;
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

7. **Añadir Liga.**

En una liga, los equipos se enfrentan en varios partidos (normalmente todos contra todos). Cada partido da puntos (por ejemplo, ganar, empatar o perder), y al final se hace una clasificación. El equipo con más puntos es el ganador de la liga. Para añadir una liga:

```
+ → Añadir Liga
```

Nos redigirá a una pantalla donde se deben rellenar los datos (nombre, temporada, categoria, máximo de quipos, mínimode jugadores y una pequeña descripción), cuando se compruebn que los datos son correctos nos diri:

<figure><img src="../../.gitbook/assets/image (58).png" alt="" width="87"><figcaption></figcaption></figure>

7. **Añadir Partido.**



8. **Añadir Jugador.**

El rol de administrador podrá añadir jugadores al equipo que se encuentra dirigiendo:

```
+ → Añadir Jugadores.
```

Nos redigirá a una pantalla de añadir jugadores. Una vez registrado los jugadores nos redigirá a Dashboard:

<figure><img src="../../.gitbook/assets/image (8).png" alt="" width="149"><figcaption></figcaption></figure>

9. **Registrar Convocatoria.**

Antes de cada encuentro, el entrenador decide qué jugadores van a jugar o estar disponibles (titulares y suplentes). Esa selección se llama convocatoria. Para añadir los jugadores a la convocatoria de un partido:&#x20;

```
Partidos → Programado → Partido → + → Convocatoria
```

Nos redigirá a una pantalla de añadir convocatoria. Una vez registrado los jugadores a la convocatoria nos redigirá al Partido:

<figure><img src="../../.gitbook/assets/image (9).png" alt="" width="131"><figcaption></figcaption></figure>

10. **Registrar Alineación.**

La _alineación_ es la lista de jugadores que empiezan jugando desde el inicio del partido. Para añadir los jugadores a la convocatoria de un partido:&#x20;

```
Partidos → En Directo → Partido → + → Alineación
```

Nos redigirá a una pantalla de añadir alineación. Una vez registrado los jugadores a la alineación nos redigirá al Partido:

<figure><img src="../../.gitbook/assets/image (10).png" alt="" width="131"><figcaption></figcaption></figure>

11. **Evento.**

Para observar los eventos que tenemos podemos ir:

```
Partidos → En directo → Partido → + → Mis Evento
```

Vemos los eventos que tenemos y podemos modificarlos e incluso eliminarlos si es conveniente:

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt="" width="128"><figcaption></figcaption></figure>

En el caso de que queramos crear un evento pulsamos en '+', escogemos el evento y nos dirigira al evento que hemos seleccionado:

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

12. **Estado Partidos.**

Los partidos pueden modificarse para cambiar el estado en el que se encuentran (en directo, programado o finalizado).

```
Partidos → En directo → Partido → + → Estado
Partidos → Programado → Partido → + → Estado
Partidos → Finalizado → Partido → + → Estado
```

Todas las pantallas redigiran a cambiar estado Partido, una ver seleccionado pulsaremos el botón de 'Restablecer Estado':

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt="" width="127"><figcaption></figcaption></figure>

13. **Restricciones.**

El administrador no contiene ninguna restricción contiene todos los permisos de la aplicación.
