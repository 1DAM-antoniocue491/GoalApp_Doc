---
icon: bullseye-arrow
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# OBJ-1. Gestión de usuarios y roles

Este objetivo cubre las funcionalidades relacionadas con la creación de cuentas, el inicio y cierre de sesión y la gestión básica de usuarios. Además, incluye el control de acceso inicial en base a los roles definidos, permitiendo que cada usuario acceda al sistema con el perfil que le corresponda.

| ID    | Nombre                                         | Descripción                                                                                                              | Roles implicados                                      | Prioridad |
| ----- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- | --------- |
| RF-01 | Registro de usuarios                           | El sistema permitirá el registro de nuevos usuarios mediante un formulario.                                              | Administrador                                         | Alta      |
| RF-02 | Inicio de sesión                               | El sistema permitirá a los usuarios iniciar sesión mediante credenciales válidas.                                        | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-03 | Validación de credenciales                     | El sistema validará las credenciales introducidas durante el inicio de sesión.                                           | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-04 | Cierre de sesión                               | El sistema permitirá cerrar la sesión de un usuario autenticado.                                                         | Administrador, Entrenador, Delegado de campo, Jugador | Media     |
| RF-05 | Asignación de rol de usuario                   | El sistema asignará un rol a cada usuario registrado.                                                                    | Administrador                                         | Alta      |
| RF-06 | Control de acceso por rol                      | El sistema controlará el acceso a las funcionalidades según el rol del usuario autenticado.                              | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-07 | Creación de usuarios por el administrador      | El sistema permitirá al administrador crear usuarios asignándoles un rol específico.                                     | Administrador                                         | Alta      |
| RF-08 | Modificación del rol de usuario                | El sistema permitirá al administrador modificar el rol de un usuario existente.                                          | Administrador                                         | Media     |
| RF-09 | Desactivación de usuarios                      | El sistema permitirá al administrador desactivar usuarios del sistema.                                                   | Administrador                                         | Media     |
| RF-10 | Bloqueo de acceso a usuarios desactivados      | El sistema impedirá el acceso al sistema a usuarios que se encuentren desactivados.                                      | Administrador                                         | Alta      |
| RF-11 | Recuperación de contraseña                     | El sistema permitirá a los usuarios restablecer su contraseña mediante un mecanismo de recuperación.                     | Administrador, Entrenador, Delegado de campo, Jugador | Media     |
| RF-12 | Gestión de sesión activa                       | El sistema mantendrá la sesión activa mientras el usuario esté autenticado.                                              | Administrador, Entrenador, Delegado de campo, Jugador | Media     |
| RF-13 | Protección de funcionalidades                  | El sistema impedirá el acceso a funcionalidades protegidas sin autenticación previa.                                     | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-14 | Asociación de usuarios a ligas                 | El sistema permitirá asociar usuarios a una liga con un rol determinado.                                                 | Administrador                                         | Alta      |
| RF-15 | Roles múltiples por usuario                    | El sistema permitirá que un usuario tenga distintos roles en diferentes ligas.                                           | Administrador                                         | Media     |
| RF-16 | Control de acciones según estado de la liga    | El sistema limitará las acciones disponibles en función del estado de la liga (en creación, en juego o finalizada).      | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-17 | Restricción de cambios en liga en juego        | El sistema impedirá la modificación de usuarios asociados a una liga en estado **en juego**, salvo por el administrador. | Administrador                                         | Alta      |
| RF-18 | Bloqueo de modificaciones en liga finalizada   | El sistema impedirá la modificación de usuarios asociados a una liga en estado **finalizada**.                           | Administrador                                         | Alta      |
| RF-19 | Conservación del historial de usuarios         | El sistema conservará el historial de usuarios asociados a una liga finalizada.                                          | Administrador                                         | Media     |
| RF-20 | Reactivación de ligas finalizadas              | El sistema permitirá al administrador reactivar una liga finalizada cambiando su estado a **en creación**.               | Administrador                                         | Media     |
| RF-21 | Reutilización de usuarios en ligas reactivadas | El sistema permitirá reutilizar la estructura de usuarios de una liga reactivada.                                        | Administrador                                         | Media     |
| RF-22 | Reasignación de roles en ligas reactivadas     | El sistema permitirá reasignar usuarios y roles cuando una liga reactivada se encuentre en estado **en creación**.       | Administrador                                         | Media     |
| RF-23 | Actualización dinámica de permisos             | El sistema actualizará los permisos del usuario cuando cambie el estado de la liga.                                      | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
| RF-24 | Visualización de opciones permitidas           | El sistema mostrará únicamente las opciones permitidas según el rol del usuario y el estado de la liga.                  | Administrador, Entrenador, Delegado de campo, Jugador | Media     |
| RF-25 | Prevención de accesos no autorizados           | El sistema impedirá la ejecución de acciones no permitidas aunque se intente acceder directamente a ellas.               | Administrador, Entrenador, Delegado de campo, Jugador | Alta      |
