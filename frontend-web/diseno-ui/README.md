# Diseño UI

La interfaz de esta aplicación esta diseñada para facilitar **la creación y la gestión de ligas de fútbol de forma sencilla e intuitiva**.&#x20;

El diseño prioriza la claridad visual y la facilidad de navegación, permitiendo a los usuarios acceder rápidamente a las principales funciones de la aplicación, como crear una liga, añadir equipos, consultar la clasificación, estadísticas, ver el calendario de partidos.&#x20;

La aplicación cuanta con una **interfaz diferente según el rol** que contenga el usuario (administrador, entrenador, delegado de campo, jugador, usuario regitrado y usuario no registrado).



1. **Guía de Estilos.**

La **guía de estilos** es un documento que recoge las normas de diseño para mantener una apariencia y funcionamiento coherente.

**a. Colores.**

Para la interfaz de la aplicación se ha optado por una **paleta de colores oscuros**, tomando como referencia el diseño visual de otras aplicaciones similares relacionadas con el fútbol.

<table><thead><tr><th align="center" valign="middle">Uso</th><th>Colores</th></tr></thead><tbody><tr><td align="center" valign="middle">Los colores para los fondos:              </td><td><p></p><p><img src="../../.gitbook/assets/image (172).png" alt="" data-size="original"></p></td></tr><tr><td align="center" valign="middle">Los colores para los textos:</td><td><img src="../../.gitbook/assets/image (173).png" alt="" data-size="original"></td></tr><tr><td align="center" valign="middle">Los colores de las tarjetas:</td><td><img src="../../.gitbook/assets/image (174).png" alt="" data-size="original"></td></tr><tr><td align="center" valign="middle">Los colores para comprobar acciones:</td><td><img src="../../.gitbook/assets/image (175).png" alt="" data-size="original"></td></tr></tbody></table>

b. **Tipografía.**

La **tipografía** es el conjunto de características que definen el estilo de la letra utilizada, incluyendo el tipo de fuente y su tamaño.

{% columns %}
{% column %}
Se ha seleccionado la tipografía **Inter** debido a su diseño moderno, limpio y altamente legible, lo que facilita la visualización de la información dentro de la aplicación. Además, su estilo minimalista mantiene una apariencia coherente y profesional en todas las pantallas, mejorando la experiencia de usuario y la claridad de la interfaz.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

c. **Espacios y Radios.**

Los radios de las esquinasy espacios que se aplicarán en las tarjetas serán los siguientes valores, definidos para mantener un diseño más suave y moderno en la interfaz:



<figure><img src="../../.gitbook/assets/image (11).png" alt="" width="190"><figcaption></figcaption></figure>

**d. Componentes.**

Los **componentes** son partes reutilizables de la interfaz de una aplicación que agrupan estructura, diseño y funcionalidad en un mismo elemento.

| Componentes                                                                                                                                                                                                                                                       | Referencias                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Los tarjetas que hemos utilizado en nuestra aplicación son:                                                                                                                                                                                                       | <img src="../../.gitbook/assets/image (13).png" alt="" data-size="original"> |
| El botón para añadir a los usuarios de una liga:                                                                                                                                                                                                                  | <img src="../../.gitbook/assets/image (14).png" alt="" data-size="original"> |
| Los botones principales que presentará nuestra aplicación son:                                 **Primary Button:** Para acciónes principales, como guardar.                                       **Secundary Button:** Para acciones segundarias, como cancelar. | <img src="../../.gitbook/assets/image.png" alt="" data-size="original">      |

2. **Inicio Sesión y Registrarse.**

El registro y el inicio de sesión son procesos fundamentales en la aplicación: el registro permite a un usuario crear una cuenta nueva introduciendo sus datos personales, mientras que el inicio de sesión le permite identificarse con esas credenciales para acceder a las funcionalidades privadas del sistema.

Sus objetivos principales son:

* Permitir el acceso a usuarios ya registrados.
* Permitir el alta de nuevos usuarios.
* Concentrar ambos flujos en una misma interfaz.
* Mantener la coherencia visual del sistema desde el primer contacto.

**a. Login**

Permitir que un usuario ya registrado acceda a su cuenta mediante sus credenciales.

* El usuario introduce su correo y contraseña.
* El sistema valida las credenciales.
* Si son correctas, accede al sistema.
* Tras autenticarse, el usuario es redirigido al **Onboarding**.

<figure><img src="../../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

**b. Registro**

Permitir el alta de nuevos usuarios en la plataforma.

* El usuario completa sus datos básicos.
* Debe confirmar la contraseña.
* Debe aceptar los términos y condiciones.
* Si el formulario es válido, se crea la cuenta.
* Tras el registro exitoso, el usuario accede al sistema y es dirigido al **Onboarding**.

<figure><img src="../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

3. **Onboarding.**

El **Onboarding** es la pantalla principal de la aplicación a la que accede el usuario tras iniciar sesión. En esta vista, todos los usuarios comparten la misma interfaz, independientemente del rol que tengan asignado.

\
Su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

Desde aquí el usuario puede:

* **crear una nueva liga.**
* **unirse a una liga existente** mediante código.
* **consultar sus ligas.**
* **filtrarlas** por estado.
* **entrar** en una liga.
* **reactivar** una liga finalizada.

<figure><img src="../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.
