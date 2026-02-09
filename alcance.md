# Alcance

#### Visión general

La aplicación permitirá:

* Crear y gestionar **múltiples ligas**, configurando su formato de competición.
* Registrar **equipos**, incluyendo información básica como nombre y escudo.
* Gestionar **jugadores**, asignándolos a equipos y registrando datos relevantes.
* Crear y programar **partidos**, asignando fechas y equipos.
* Introducir **resultados**, goles, tarjetas e incidencias.
* Generar automáticamente la **clasificación**, actualizada tras cada partido.
* Consultar **estadísticas básicas**, como máximos goleadores o rachas de resultados.
* Diferenciar **roles de usuario**, limitando las acciones según permisos (administrador o usuario).

***

#### Cobertura funcional

La aplicación cubrirá las funcionalidades necesarias para la creación y gestión de ligas de fútbol, permitiendo administrar toda la información clave relacionada con competiciones, equipos, jugadores y partidos. El sistema se estructura en los siguientes módulos funcionales:

**1. Gestión de usuarios**

La aplicación permitirá el registro e inicio de sesión de usuarios, así como la gestión básica de sus datos personales. Se incluirán funcionalidades como:

* Crear cuenta
* Iniciar sesión y cerrar sesión
* Editar perfil
* Cambiar contraseña

**2. Gestión de ligas**

Los usuarios podrán crear y administrar ligas de fútbol, estableciendo su información general y su sistema de puntuación. Las funcionalidades contempladas son:

* Crear, editar y eliminar ligas
* Definir datos generales (nombre, temporada, categoría, descripción, logo)
* Configurar sistema de puntuación (victoria, empate, derrota)

**3. Gestión de equipos**

La aplicación permitirá registrar equipos dentro de una liga y administrar su información y su plantilla. Se incluirán funciones como:

* Crear, editar y eliminar equipos
* Asignar un equipo a una liga
* Añadir información general (ciudad, colores, fecha de creación, descripción, logo)
* Registrar entrenador y capitán
* Consultar historial de temporadas

**4. Gestión de jugadores y entrenadores**

Los usuarios podrán dar de alta jugadores y entrenadores asociados a un equipo, así como editar o eliminar su información. Incluye:

* Crear, editar y eliminar jugadores
* Asociar jugadores a un equipo y liga
* Crear, editar y eliminar entrenadores
* Asignar entrenador a un equipo

**5. Gestión de partidos**

El sistema permitirá generar y organizar partidos dentro de una liga, gestionar su estado y registrar resultados. Se contemplan funcionalidades como:

* Programar partidos (fecha, hora inicio y fin)
* Generar calendario automático
* Registrar resultados (goles local/visitante)
* Cambiar estado del partido (programado, jugado, cancelado)
* Visualizar próximos partidos

**6. Gestión de alineaciones y formaciones**

La aplicación incluirá un módulo de gestión táctica para organizar alineaciones y formaciones tanto por equipo como por partido:

* Crear formaciones (ej: 4-3-3, 5-4-1)
* Definir posiciones por formación (GK, CB, CM…)
* Asignar formación a un equipo
* Registrar alineación del partido (titulares y suplentes)
* Registrar formación usada en un partido

**7. Estadísticas y visualización**

Se permitirá consultar información actualizada de la liga y estadísticas relevantes:

* Clasificación de liga
* Información general de liga (equipos, jugadores, situación en tabla)
* Máximos goleadores
* Tarjetas amarillas y rojas por partido
* Estadísticas básicas de equipos y jugadores

**8. Funcionalidades fuera de alcance**

El sistema no incluirá funcionalidades como:

* Pagos online o suscripciones
* Integración con redes sociales
* Aplicación para smartwatch
* Transmisión en vivo de partidos

***

#### Producto mínimo viable

El Producto Mínimo Viable (MVP) de la aplicación se centrará en ofrecer las funcionalidades esenciales para que un usuario pueda crear una liga, registrar equipos y jugadores, generar un calendario de partidos y consultar resultados y clasificación.

El MVP incluirá:

**1. Autenticación básica**

* Registro de usuario
* Inicio de sesión y cierre de sesión

**2. Gestión mínima de ligas**

* Crear liga
* Editar liga
* Eliminar liga
* Definir nombre, temporada y categoría

**3. Gestión mínima de equipos**

* Crear equipo
* Editar equipo
* Eliminar equipo
* Asociar equipo a una liga

**4. Gestión mínima de jugadores**

* Crear jugador
* Editar jugador
* Eliminar jugador
* Asociar jugador a un equipo

**5. Gestión mínima de partidos**

* Generar calendario automático
* Registrar resultado del partido (goles local/visitante)
* Visualizar próximos partidos

**6. Visualización esencial**

* Ver clasificación de la liga
* Ver resultados de partidos
* Ver lista de equipos y jugadores
