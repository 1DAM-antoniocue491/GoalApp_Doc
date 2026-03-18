# Usuario Registrado

El usuario una vez registrado e iniciado sesión accederá a una interfaz mucho más amplia que el usuario sin registrar.&#x20;



1. **Estructura de navegación.**

E apartado de _MainTabs_, disponible en modo completo para usuarios autenticados, que contiene las secciones principales de la aplicación: _Dashboard_, _Liga_, _Partidos_ y _Perfil_. Estas secciones permiten al usuario navegar entre los distintos apartados de forma sencilla mediante una barra de navegación.

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
* **Liga:** Se consulta la clasificación de la liga con las estadísticas de todos los equipos que la forman
* **Partido**: Consulta el estado de los partidos.&#x20;
* **Perfil:** Permite ver la información del usuario registrado.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

3. **Comportamiento Global.**

La navegación y las funcionalidades de la aplicación para usuarios autenticados presentan un comportamiento consistente y completo:

* **Sin cabecera:**\
  Dado que el usuario ya ha iniciado sesión, no se muestran mensajes ni botones que inviten a registrarse o iniciar sesión.
* **Acceso completo según rol y permisos:**\
  Todas las secciones y acciones disponibles en la aplicación se habilitan de acuerdo con el rol del usuario.&#x20;
* **Validación de acciones sensibles:** Permite modificar información del perfil o ver información detallada de quipos, partidos e incluso jugadores.



4. **Flujo de usuario.**

El **flujo de usuario** describe cómo se desplaza un usuario autenticado dentro de la aplicación y qué acciones puede realizar en cada sección:

* **Dashboard**. Al iniciar sesión, el usuario accede al _Dashboard_, que funciona como pantalla principal. Habrá un apartado donde se podrán ver los partidos en directo y los 3 proximos por disputar. Si queremos ver todos los partidos, debemos pulsar en el apartado “Ver todo”. Del mismo modo, para consultar los partidos en directo, es necesario pulsar el botón “En directo”.
* **Liga.** Desde la sección _Liga_, el usuario puede ver la clasificación general y estadísticas de los equipos. Al seleccionar un equipo específico, se accede a su _detalle_, mostrando&#x20;

```
Dashboard → Información Liga
Liga → Detalle de ligas, equipos y jugadores.
Partidos → Detalle de partido. 
Perfil → Editar perfil / Cerrar sesión
```



Seguiremos contando con un task en la parte inferior (inicio, liga, partidos, perfil).

* **Dashboard:** Será la pantalla de inicio. Podremos elegir la liga que más nos interese visitar. Habrá un apartado donde se podrán ver los partidos en directo y los 3 proximos por disputar. Si queremos ver todos los partidos, debemos pulsar en el apartado “Ver todo”. Del mismo modo, para consultar los partidos en directo, es necesario pulsar el botón “En directo”.

<figure><img src="../../.gitbook/assets/image (33).png" alt="" width="124"><figcaption></figcaption></figure>

* Liga:

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>
