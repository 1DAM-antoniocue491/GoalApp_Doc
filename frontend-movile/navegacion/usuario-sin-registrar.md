# Usuario sin Registrar

El usuario que accede por primera vez a la aplicación encontrará una interfaz limitada. En la parte superior, se muestra un encabezado que le recuerda en todo momento la posibilidad de iniciar sesión o registrarse, independientemente de la pantalla en la que se encuentre.

1. **Estructura de navegación.**

La aplicación se organiza a partir de una estructura principal denominada _Root_, desde la cual se gestionan dos flujos de navegación. Por un lado, se encuentra el _AuthStack_, que incluye las pantallas de autenticación, como inicio de sesión (_Login_) y registro (_Register_).

Por otro lado, está el apartado de _MainTabs_, disponible en modo limitado para usuarios no autenticados, que contiene las secciones principales de la aplicación: _Dashboard_, _Liga_, _Partidos_ y _Perfil_. Estas secciones permiten al usuario navegar entre los distintos apartados de forma sencilla mediante una barra de navegación.

```
Root
├── AuthStack
│   ├── Login
│   └── Register
└── MainTabs (modo limitado)
    ├── Dashboard
    ├── Liga
    ├── Partidos
    └── Perfil

```

2. **Navegación Disponible.**

Las navegaciones que podemos encontrar en nuestra aplicación a traves de un tabs son:

* **Dashboard:** Se trata de la pantalla de inicio de la aplicación, que permite visualizar la información más importante sobre la liga.
* **Liga:** Se consulta la clasificación de la liga con las estadísticas de todos los equipos que la forman
* **Partido**: Consulta el estado de los partidos.&#x20;
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

3. **Comportamiento Global.**

Independientemente de la pagina que nos encontremos encontraremos una cabecera que invitara al usuario a registrarse o iniciar sesión.

* **Regitrarse.** Rellenar los campos (nombre, email, contraseña y repetir contraseña) y redirigue a iniciar sesión.
* **Iniciar sesión:** Rellenar campos de email y contraseña, y ridirigue a dashboard.

<figure><img src="../../.gitbook/assets/image (38).png" alt="" width="247"><figcaption></figcaption></figure>

4. **Flujo de Autentificación.**

El flujo para autentificarse en la aplicación será la siguiente:

* **Regitrarse.** El usuario deberá rellenar todos los campos y pulsar el botón de registrarse. Una vez se comprueben que todos los campos son correctos abrirá la pantalla de Iniciar Sesión.
* **Iniciar sesión:** El usuario deberá introducir el correo electrónico y la contraseña proporcionados durante el registro. En caso de haber olvidado la contraseña, dispondrá de una opción para recuperarla. Una vez completados los campos, deberá pulsar el botón de inicio de sesión y, tras la verificación de los datos, se accederá al dashboard, donde se mostrará un mensaje de bienvenida.

```
Registro → Iniciar Sesión → Dashboard
```

5. **Tabs principales.**

Los tabs que podemos encontrar en nuestra aplicación son los siguientes:

* **Dashboard:** Será la pantalla de inicio. Podremos elegir la liga que más nos interese visitar. Habrá un apartado donde se podrán ver los partidos en directo y los 3 proximos por disputar.
* **Liga:** El usuario podrá consultar la clasificación de la liga, la cual se organiza en función de un sistema de puntuación predefinido (0 puntos por derrota, 1 por empate y 3 por victoria). Asimismo, se pueden visualizar de forma detallada de cada equipo los partidos jugados, victorias, derrotas, empates, goles a favor y goles en contra.
* **Partido**: Dentro de esta sección, tendremos un tabs del estado en el que se encuentran los partidos (Directo, Programado, Finalizado) de la liga escogida.&#x20;
* **Perfil.** Los campos estarán vacios hasta que el usuario decida registrarse o iniciar sesión.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

6. **Restricciones.**

En esta versión de la aplicación, se aplican las siguientes limitaciones:

* No se permite el acceso a funcionalidades que requieran usuario autenticado, por lo que algunas secciones solo están disponibles después de iniciar sesión.
* No existe personalización de contenido, por lo que la información mostrada es la misma para todos los usuarios.
