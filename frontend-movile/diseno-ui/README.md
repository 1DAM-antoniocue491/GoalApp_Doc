# Diseño UI

La interfaz de esta aplicación esta diseñada para facilitar **la creación y la gestión de ligas de fútbol de forma sencilla e intuitiva**. El diseño prioriza la claridad visual y la facilidad de navegación, permitiendo a los usuarios acceder rápidamente a las principales funciones de la aplicación, como crear una liga, añadir equipos, consultar la clasificación, estadísticas, ver el calendario de partidos. La aplicación cuanta con una interfaz diferente según el rol que contenga el usuario (administrador, entrenador, delegado de campo, jugador, usuario regitrado y usuario no registrado).



1. **Guía de Estilos.**

La **guía de estilos** es un documento que recoge las normas de diseño para mantener una apariencia y funcionamiento coherente.

**a. Colores.**

Para la interfaz de la aplicación se ha optado por una **paleta de colores oscuros**, tomando como referencia el diseño visual de otras aplicaciones similares relacionadas con el fútbol.

<table><thead><tr><th align="center" valign="middle">Uso</th><th>Colores</th></tr></thead><tbody><tr><td align="center" valign="middle">Los colores para los fondos:              </td><td><img src="../../.gitbook/assets/image (4).png" alt="" data-size="original"></td></tr><tr><td align="center" valign="middle">Los colores para los textos:</td><td><img src="../../.gitbook/assets/image (3) (1).png" alt="" data-size="original"></td></tr><tr><td align="center" valign="middle">Los colores de las tarjetas:</td><td><img src="../../.gitbook/assets/image (5).png" alt="" data-size="original"></td></tr><tr><td align="center" valign="middle">Los colores para comprobar acciones:</td><td><img src="../../.gitbook/assets/image (6).png" alt="" data-size="original"></td></tr></tbody></table>

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

| Componentes                                                 | Referencias                                                                 |
| ----------------------------------------------------------- | --------------------------------------------------------------------------- |
| Los tarjetas que hemos utilizado en nuestra aplicación son: | <img src="../../.gitbook/assets/image (9).png" alt="" data-size="original"> |

2. **Inicio Sesión y Registrarse.**

Sus objetivos principales son:

* Permitir el acceso a usuarios ya registrados.
* Permitir el alta de nuevos usuarios.
* Concentrar ambos flujos en una misma interfaz.
* Mantener la coherencia visual del sistema desde el primer contacto.

**a. Login**

Permitir que un usuario ya registrado acceda a su cuenta mediante sus credenciales.

{% columns %}
{% column %}


* El usuario introduce su correo y contraseña.
* El sistema valida las credenciales.
* Si son correctas, accede al sistema.
* Tras autenticarse, el usuario es redirigido al **Onboarding**.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (177).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

**b. Registro**

Permitir el alta de nuevos usuarios en la plataforma.

{% columns %}
{% column %}


* El usuario completa sus datos básicos.
* Debe confirmar la contraseña.
* Debe aceptar los términos y condiciones.
* Si el formulario es válido, se crea la cuenta.
* Tras el registro exitoso, el usuario accede al sistema y es dirigido al **Onboarding**.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

3. **Onboarding.**

El **onboarding** es la primera sección que aparece después del login o del registro. El onboarding será el mismo para todos los usuarios sin importar el rol.\
Su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta.

{% columns %}
{% column %}
Desde aquí el usuario puede:

* **Crear una nueva liga.**
* **Editar una liga** si tiene permisos.
* **Unirse a una liga existente** mediante código.
* **Consultar sus ligas.**
* **Filtrarlas** por estado.
* **Entrar** en una liga.
* **Reactivar** una liga finalizada.
* **Seleccionar favoritas.**
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="563"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Por tanto, esta sección no es todavía un panel operativo de partido o gestión diaria, sino el **punto de acceso y organización inicial** del sistema.
