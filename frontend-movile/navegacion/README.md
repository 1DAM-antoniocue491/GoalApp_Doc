# Navegación

La navegación de nuestra aplicación esta diseñada para ser de forma sencilla e intuitiva, permitiendo a los usuarios poder acceder rapidamente a diferentes funcionalidades a través de la aplicación.

1. **Inicio Sesión y Registrarse.**

Sus objetivos principales son:

* Permitir el acceso a usuarios ya registrados.
* Permitir el alta de nuevos usuarios.
* Concentrar ambos flujos en una misma interfaz.
* Mantener la coherencia visual del sistema desde el primer contacto.

**a. Login**

Permitir que un usuario ya registrado acceda a su cuenta mediante sus credenciales.

{% columns %}
{% column valign="middle" %}
* El usuario introduce su correo y contraseña.
* El sistema valida las credenciales.
* Si son correctas, accede al sistema.
* Tras autenticarse, el usuario es redirigido al **Onboarding**.
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (176).png" alt=""><figcaption></figcaption></figure>
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

2. **Onboarding.**

El **onboarding** su función es situar al usuario dentro de GoalApp antes de entrar al dashboard de una liga concreta. El onboarding es el mismo para todos los usuarios sin distinguir de su rol.

Las funciones de Onboarding son:

* **Crear liga.** Si pulsa **Crear liga**, se abre el modal **Nueva Liga**, donde puede configurar datos como:
  * Nombre de la liga.
  * Temporada.
  * Categoría.
  * Cantidad máxima de partidos.
  * Minutos posibles de los partidos.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

Cuando confirma la acción, la liga se crea y el usuario queda asociado como **administrador**.

* **Editar y eliminar**, desde el cual es posible modificar y actualizar la configuración de la misma e incluso eliminarla. En esta sección se puede editar información adicional relacionada con la liga, permitiendo una gestión más completa y personalizada. Si pulsa en los ajustes de la liga, se abre el modal **Configuración de Liga**, donde puede configurar datos como:
  * Nombre de la liga.
  * Temporada.
  * Categoría.
  * Número mínimo y máximo de equipos.
  * Mínimo y máximo de convocados.
  * Mínimo y máximo de jugadores que forman parte de la plantilla.
  * Duración de los partidos.
  * Cantidad máxima de partidos.

{% columns %}
{% column valign="middle" %}
<div align="center"><figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure></div>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (12) (1).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Unirme a una liga.** Si pulsa **Unirme**, se abre un modal para introducir un **código de invitación**. Si el código es válido, la liga se añade a su cuenta y tendrá los permisos del rol asignado.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<div align="center"><figure><img src="../../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure></div>
{% endcolumn %}
{% endcolumns %}

* **Entrar en una liga.** Si pulsa **Entrar** en una tarjeta, accede directamente al dashboard de esa liga.

{% columns %}
{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/image (107).png" alt="" width="188"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

* **Reactivar una liga.** Si una liga está en estado **finalizado**, solo el **administrador** puede usar **Reactivar liga**.\
  Cuando la reactiva:
  * La liga vuelve a estar activa.
  * Conserva todos sus datos.
  * Desaparece del filtro **Finalizadas.**
  * Vuelve a **Todas.**
  * La acción principal cambia a **Entrar**.

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/image (8) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column valign="middle" %}
<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}
