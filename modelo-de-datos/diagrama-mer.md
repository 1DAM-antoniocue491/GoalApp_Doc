# Diagrama MER

El **Modelo Entidad–Relación (MER)** representa gráficamente la estructura de la base de datos y las relaciones entre las entidades principales del sistema. Este diagrama sirve como referencia visual para comprender cómo se conectan los usuarios, equipos, ligas, partidos y demás componentes del proyecto.

A continuación se presentan los diagramas organizados por áreas funcionales, junto con una breve explicación de cada uno.

### **1. Visión General del Modelo**

Este diagrama muestra todas las entidades principales del sistema y sus relaciones. Incluye:

* Usuarios, roles y jugadores
* Equipos y ligas
* Partidos y eventos
* Formaciones y alineaciones
* Notificaciones

<figure><img src="../.gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Este diagrama permite obtener una visión completa del sistema y entender cómo interactúan las distintas partes entre sí.

### **2. Usuarios y Roles**

Este diagrama detalla la relación entre:

* `usuarios`
* `roles`
* `usuario_rol`
* `jugadores`

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Puntos clave:

* Un usuario puede tener múltiples roles.
* Un jugador siempre está asociado a un usuario.
* La tabla intermedia `usuario_rol` implementa la relación N:N.

### **3. Equipos, Ligas y Jugadores**

Este diagrama muestra cómo se relacionan:

* `ligas`
* `equipos`
* `jugadores`

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Puntos clave:

* Cada equipo pertenece a una liga.
* Cada jugador pertenece a un equipo.
* Cada equipo tiene asignado un entrenador y un delegado (ambos usuarios).

### **4. Partidos y Eventos**

Este diagrama representa:

* `partidos`
* `eventos_partido`

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Puntos clave:

* Un partido siempre se da entre dos equipos de la misma liga.
* Un partido puede tener múltiples eventos.
* Cada evento está asociado a un jugador y a un partido.

### **5. Formaciones y Alineaciones**

Este diagrama incluye:

* `formaciones`
* `posicion`
* `formacion_equipo`
* `formacion_partido`

<figure><img src="../.gitbook/assets/image (8) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Puntos clave:

* Una formación define un conjunto de posiciones.
* Un equipo puede tener varias formaciones disponibles.
* En cada partido, un equipo selecciona una formación concreta.
* Las alineaciones deben respetar la formación definida.

### **6. Notificaciones**

Este diagrama muestra la relación entre:

* `notificaciones`
* `usuarios`

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Puntos clave:

* Cada notificación tiene un usuario destinatario.
* Se registra el estado (leída/no leída) y la fecha de envío.

### **7. Notas sobre el MER**

* Todas las relaciones críticas están reforzadas mediante claves foráneas.
* Las cardinalidades reflejan las reglas de negocio del sistema.
* El modelo está diseñado para permitir escalabilidad y futuras ampliaciones.
