# Roles y permisos

### Descripción general

Para garantizar la seguridad, la confidencialidad de los datos y el control de acceso dentro de la aplicación, el sistema implementa un modelo de autorización basado en **roles y permisos**.

* **Rol:** define el conjunto de responsabilidades y capacidades de un usuario dentro del sistema.
* **Permiso:** define una acción concreta que un usuario puede realizar.

El acceso a las funcionalidades del sistema depende del rol asignado, y el sistema validará siempre el rol antes de permitir la ejecución de cualquier acción.

***

### Roles disponibles en el sistema

El sistema contempla los siguientes roles principales:

* **Administrador (Admin)**
* **Entrenador (Coach)**
* **Jugador (Player)**
* **Observador (Viewer)**
* **Delegado de campo (Delegate)**

***

### Modelo jerárquico de roles

El sistema define una jerarquía de roles, donde los roles superiores heredan permisos de los roles inferiores.

Jerarquía:

* **Admin**
  * **Coach**
  * **Player**
    * **Viewer**

Esto implica:

* Un **Player** dispone de todos los permisos de **Viewer**.
* Un **Coach** dispone de todos los permisos de **Player** y **Viewer**.
* Un **Admin** dispone de todos los permisos del sistema.

***

### Rol funcional adicional: Delegado de campo (Delegate)

El rol **Delegado de campo** se considera un rol funcional y contextual.

Esto significa que:

* No forma parte de la jerarquía de herencia de permisos.
* Se asigna con el objetivo de permitir acciones concretas relacionadas con el registro de eventos durante un partido.
* Sus permisos están limitados a partidos específicos asignados.

***

### Matriz de permisos

La definición completa de permisos por rol se presenta en la sección **Matriz de permisos**, donde se detalla de forma estructurada qué acciones puede realizar cada tipo de usuario.
