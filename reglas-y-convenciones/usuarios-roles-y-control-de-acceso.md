# Usuarios, Roles y Control de Acceso

Esta sección define las reglas de negocio relacionadas con la gestión de usuarios, la asignación de roles y el control de acceso dentro del sistema de gestión de ligas amateur de fútbol. Su objetivo es garantizar un modelo de permisos coherente, seguro y adaptable a la participación de cada usuario en distintas ligas.

### **1. Control de acceso basado en roles (RBAC)**

El sistema utiliza un modelo de **Control de Acceso Basado en Roles (RBAC)**. Esto significa que:

* Todas las acciones disponibles dependen del **rol asignado al usuario dentro de cada liga**.
* El acceso se determina por el **rol**, no por la identidad del usuario.
* Un usuario puede tener **roles diferentes en distintas ligas**.
* Los permisos no se asignan directamente a usuarios, sino a roles.

#### **Reglas principales**

* Todo usuario debe registrarse para utilizar el sistema.
* Los usuarios no autenticados solo pueden acceder a información pública.
* Los usuarios autenticados acceden a funcionalidades según su rol en cada liga.
* Un mismo usuario puede participar en varias ligas simultáneamente.
* Los roles determinan qué acciones puede realizar un usuario en cada liga.

### **2. Roles del sistema**

Los roles representan perfiles funcionales dentro de una liga. Algunos ejemplos habituales son:

* **Administrador**
* **Entrenador**
* **Delegado de campo**
* **Jugador**
* **Viewer**
* (Opcionales en el futuro: Árbitro, Moderador, Analista…)

Cada rol tiene permisos específicos definidos por el sistema.

### **3. Asignación de roles dentro de una liga**

La asignación de roles se realiza automáticamente según la participación del usuario y las acciones administrativas.

#### **Reglas de asignación**

* El **creador de una liga** obtiene automáticamente el rol de **Administrador** en esa liga.
* Cuando un administrador asigna un **entrenador** a un equipo, el usuario obtiene el rol de **Entrenador** en esa liga.
* Cuando un administrador asigna un **delegado de campo**, el usuario obtiene el rol de **Delegado de campo** en esa liga.
* Cuando un usuario es añadido como **jugador** a un equipo, obtiene el rol de **Jugador** en esa liga.

#### **Características clave**

* Un usuario puede tener múltiples roles en distintas ligas.
* Un usuario puede tener varios roles dentro de la misma liga si así lo permite la organización.
* La asignación de roles está vinculada a acciones administrativas, no a la edición manual de permisos.

### **4. Acceso a funcionalidades según rol**

El sistema determina qué puede hacer cada usuario en función de su rol:

* **Administrador**: gestión completa de la liga (equipos, roles, configuración…)
* **Entrenador**: gestión del equipo, alineaciones, convocatorias
* **Delegado de campo**: registro de eventos del partido
* **Jugador**: acceso a información de su equipo y estadísticas personales
* **Usuario no autenticado**: solo información pública

Cada rol tiene un conjunto de permisos predefinidos que garantizan coherencia y seguridad.

### **5. Visibilidad de la información**

La visibilidad también depende del rol:

* Usuarios invitados → solo clasificación y resultados
* Usuarios autenticados → información adicional según su rol
* Administradores → acceso completo a la liga
