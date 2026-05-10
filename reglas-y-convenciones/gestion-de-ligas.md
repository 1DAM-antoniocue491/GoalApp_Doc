# Gestión de ligas

Esta sección define las reglas de negocio relacionadas con la creación, configuración, gestión y finalización de las ligas dentro del sistema. El objetivo es garantizar un funcionamiento coherente, evitar inconsistencias y asegurar que la competición siga un flujo lógico y controlado.

## **1. Ciclo de vida de una liga**

Las ligas siguen un ciclo de vida basado en estados. Cada estado determina qué acciones están permitidas y cuáles están restringidas.

### **Estados de la liga**

Una liga puede encontrarse en uno de los siguientes estados:

* **CONFIGURACIÓN**: Se añaden equipos, se asignan roles y se completan los datos previos al inicio.
* **EN CURSO:** La liga está activa y se disputan partidos oficiales.
* **FINALIZADA**:La liga está cerrada y solo disponible en modo consulta.

## **2. Reglas de transición entre estados**

El sistema controla estrictamente cómo puede avanzar una liga entre estados para garantizar coherencia.

#### **De CONFIGURACIÓN → EN CURSO**

* La liga debe tener **al menos dos equipos registrados**.
* Todos los equipos deben tener asignados:
  * 1 entrenador
  * 1 delegado de campo
* No se permite iniciar la competición si faltan roles esenciales.

#### **De EN EN CURSO→ FINALIZADA**

* Todos los partidos deben estar en estado **FINALIZADO**.
* No puede finalizarse si quedan partidos pendientes o en curso.

## **3. Restricciones durante la competición**

Una vez que la liga entra en estado **EN COMPETICIÓN**, se aplican las siguientes restricciones:

{% hint style="danger" %}
No se pueden añadir equipos.
{% endhint %}

{% hint style="danger" %}
No se pueden eliminar equipos.
{% endhint %}

{% hint style="danger" %}
No se pueden modificar reglas o configuraciones de la liga.
{% endhint %}

{% hint style="danger" %}
No se pueden cambiar roles asignados a equipos (entrenador/delegado).
{% endhint %}

Estas restricciones garantizan que la competición sea estable y justa.

## **4. Gestión general de ligas**

#### **Creación de ligas**

* Solo un usuario autenticado puede crear una liga.
* El creador obtiene automáticamente el rol de **Administrador** en esa liga.

#### **Edición de ligas**

* Solo los administradores pueden editar la liga.
* La edición solo es posible en los estados **CREADA** y **CONFIGURACIÓN**.

#### **Eliminación de ligas**

* Solo puede eliminarse si:
  * No tiene partidos registrados, o
  * Todos los partidos están eliminados
* Una liga en estado **EN COMPETICIÓN** o **FINALIZADA** no puede eliminarse.

## **5. Relación entre ligas y equipos**

* Un equipo pertenece a una única liga.
* Una liga puede tener múltiples equipos.
* Los equipos deben estar completamente configurados antes de iniciar la competición.
