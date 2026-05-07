# Usuario Registrado

El usuario una vez registrado e iniciado sesión accederá a una interfaz mucho más amplia que el usuario sin registrar.&#x20;

1. **Estructura de navegación.**

El apartado de (tabs), disponible en modo completo para usuarios autenticados, que contiene las secciones principales de la aplicación: _Dashboard_, Calendarios, estadisticas y _Perfil_. Estas secciones permiten al usuario navegar entre los distintos apartados de forma sencilla mediante una barra de navegación.

```
src
└── (tabs)
    ├── _layout.tsx
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
* **Estadísticas**: La **pantalla de estadísticas** es la sección donde el usuario puede consultar datos y métricas relacionadas con los equipos o los jugadores.
  * **Equipos**. Ver las estadísticas de los equipos por distintas estadísticas (goles, derrotas, victorias, etc.)
  * **Jugadores**. Ver las estadísticas de los jugadores por distintas estadísticas (goles, MVP, etc.)
* **Perfil:** La **pantalla de perfil** es la sección donde el usuario puede consultar su información personal dentro de la aplicación.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

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
Onboarding → Información Ligas.
Dashboard → Información Liga escogida.
Liga → Detalle de las Jornadas, Equipos y Clasificación.
Estadísticas → Ver estadísticas de los Equipos y Jugadores. 
Perfil → Editar perfil / Cerrar sesión
```

**a. Onboarding.**

El **onboarding** su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

* **Unirme a una liga.** Si pulsa **Unirme**, se abre un modal para introducir un **código de invitación**.\
  Si el código es válido, la liga se añade a su cuenta y después podrá entrar con el rol asignado.
* **Entrar en una liga.** Si pulsa **Entrar** en una tarjeta, accede directamente al dashboard de esa liga.

**b. Dashboard.**

El **dashboard según el rol** es la pantalla principal de trabajo dentro de una liga.

* **Volver al onboarding.** El encabezado de la aplicación permite al usuario regresar a la pantalla de onboarding al ser pulsado.
* **Ver notificaciones.** Al pulsar el icono de la campana en el encabezado, el usuario podrá visualizar todas las notificaciones recibidas, organizadas según su tipo (todas, en vivo, resultados, etc.). Para cerrar la pantalla pulsaremos el botón de retroceder.
* **Ver plantillas.** Al pulsar ‘Ver plantilla’, se mostrará una pantalla con las plantillas de los equipos que están disputando el partido.
* **Ver calendarios.** Al pulsar ‘Ver calendarios’, se redirigirá al usuario a la pestaña de calendario, mostrando los partidos en estado programado.
* **Ver partido programado.**&#x20;
* **Inicializar Partido.**&#x20;
* **Convocatoria.**
* **Alineación Titular.**

**c. Calendario.**

La pantalla **Calendario** organiza los encuentros de la liga principalmente por **jornadas**, pero también permite visualizarlos por **equipos** y por **clasificación**, ofreciendo distintas formas de consultar la competición.

* **Jornada**. Se podrán ver todos los partidos según el estado en el que se encuentren (en vivo, programados o finalizados).
* **Equipo.**
* **Clasificación.**

**e. Estadísticas.**

**f. Perfil.**

El perfil es la pantalla donde el usuario puede ver y gestionar sus datos personales dentro de la aplicación.

* **Editar Perfil**. Al seleccionar el icono de editar ubicado en la parte superior derecha, se mostrará una pantalla con los datos del usuario, permitiendo su modificación.
* **Cerrar Sesión.** Al pulsar el botón de ‘Cerrar sesión’, se mostrará un aviso de confirmación y, si el usuario acepta, será redirigido a la pantalla de inicio de sesión.

3. **Restricciones.**

Las limitaciones que presenta este usuario son:

* No podrá crear ligas de fútbol.
* No podrá crear equipos.
* No podrá asignar roles ni eliminarlos.
* No podra crear un evento.
* No podrá consultar estadísticar personales de un jugador.
* No podrá ver estadísticas personales del jugador.
