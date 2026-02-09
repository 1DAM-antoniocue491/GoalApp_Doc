# Integridad y Seguridad

La integridad y la seguridad del sistema son pilares fundamentales para garantizar un funcionamiento fiable, coherente y protegido frente a accesos indebidos o inconsistencias en los datos. Esta sección describe los mecanismos implementados para asegurar la calidad de la información, la correcta aplicación de las reglas de negocio y la protección de los usuarios y sus datos.

## **1. Integridad de Datos**

La integridad del modelo de datos se garantiza mediante un conjunto de restricciones, claves y reglas que aseguran que la información almacenada sea válida, consistente y coherente con la lógica del sistema.

### **Claves primarias y foráneas**

* Todas las tablas principales incluyen **claves primarias (PK)** para identificar de forma única cada registro.
* Las relaciones entre entidades se implementan mediante **claves foráneas (FK)** que garantizan la integridad referencial.
* Las FK están configuradas para evitar registros huérfanos o inconsistentes.

### **Eliminaciones en cascada controladas**

* Se aplican eliminaciones en cascada únicamente cuando es seguro y coherente:
  * Eliminar un partido elimina sus eventos asociados.
  * Eliminar una formación de partido elimina su alineación.
* En entidades críticas (usuarios, ligas, equipos), las eliminaciones están restringidas para evitar pérdida accidental de información.

### **Restricciones NOT NULL, UNIQUE y CHECK**

* **NOT NULL** asegura que los campos esenciales siempre tengan valor.
* **UNIQUE** evita duplicidades en campos como correos electrónicos o nombres de usuario.
* **CHECK** valida reglas específicas, como:
  * Tipos de eventos permitidos.
  * Estados válidos de ligas y partidos.
  * Formatos de posiciones en formaciones.

### **Auditoría**

Todas las tablas principales incluyen:

* `created_at`: fecha de creación del registro.
* `updated_at`: fecha de última modificación.

Esto permite:

* Trazabilidad completa.
* Control de cambios.
* Depuración eficiente.

## **2. Seguridad del Sistema**

La seguridad se centra en proteger el acceso a la información, garantizar la autenticidad de los usuarios y evitar acciones no autorizadas.

### **Control de acceso basado en roles (RBAC)**

* El sistema utiliza un modelo RBAC donde los permisos dependen del **rol del usuario dentro de cada liga**.
* Un usuario puede tener roles distintos en distintas ligas.
* El acceso se define por el rol, no por el usuario.
* Los roles se asignan automáticamente según la participación del usuario (administrador, entrenador, delegado, jugador).

### **Autenticación y protección de credenciales**

* Las contraseñas se almacenan utilizando **hash seguro**, nunca en texto plano.
* El sistema puede integrar mecanismos adicionales como:
  * Políticas de contraseñas fuertes.
  * Recuperación segura de cuentas.
  * Validación por correo electrónico.

### **Restricciones de acceso**

* Usuarios no autenticados solo pueden ver información pública.
* Usuarios autenticados acceden a funcionalidades según su rol.
* Acciones sensibles (crear ligas, asignar roles, gestionar equipos) están restringidas a administradores.

### **Validación de acciones**

El sistema valida que:

* Un usuario solo pueda gestionar equipos o ligas donde tenga rol asignado.
* Un entrenador solo pueda gestionar su propio equipo.
* Un delegado solo pueda gestionar su propio equipo.
* Un jugador solo pueda acceder a información de su equipo y liga.

### **Protección contra inconsistencias**

* No se permite registrar eventos de partido asociados a jugadores no convocados.
* No se permite modificar configuraciones de una liga en estado EN COMPETICIÓN o FINALIZADA.
* No se permite eliminar equipos con partidos programados o jugados.

## **3. Seguridad de la Información**

### **Datos sensibles**

* Se protege la información personal de los usuarios.
* No se almacenan datos innecesarios (minimización de datos).
* No se almacenan contenidos multimedia pesados ni mensajes privados.

### **Acceso a datos**

* Solo los usuarios con permisos adecuados pueden consultar o modificar información sensible.
* Las operaciones críticas quedan registradas mediante auditoría.

### **Prevención de errores y fraudes**

* Validaciones estrictas en la creación de partidos, eventos y alineaciones.
* Restricciones para evitar manipulación de estadísticas o resultados.

## **6. Resumen de Integridad y Seguridad**

* Integridad garantizada mediante PK, FK, restricciones y auditoría.
* Seguridad basada en RBAC con roles por liga.
* Contraseñas protegidas mediante hash.
* Acciones sensibles restringidas a roles autorizados.
* Validaciones estrictas para evitar inconsistencias en ligas, equipos, partidos y eventos.
* Protección de datos personales y minimización de información almacenada.
