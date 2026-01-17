# Inicio

**Aplicación de gestión de ligas amateur de fútbol:&#x20;**_**GoalApp**_

<figure><img src=".gitbook/assets/futbol.webp" alt=""><figcaption></figcaption></figure>

## Descripción

El proyecto consiste en el desarrollo de una **aplicación móvil multiplataforma** (Android, iOS y versión web) destinada a la **gestión integral de ligas amateur de fútbol**, orientada a grupos de amigos, asociaciones deportivas, ligas locales y equipos de fútbol base.

La aplicación permitirá administrar de forma sencilla y centralizada todos los elementos necesarios para el funcionamiento de una competición: **ligas, equipos, jugadores, partidos, resultados, clasificaciones y estadísticas**, evitando el uso de hojas de cálculo u otras herramientas externas poco especializadas.

#### Trabajo en equipo y organización

El desarrollo se realiza de forma colaborativa, con una **división clara de roles y responsabilidades** entre los miembros del equipo.

La planificación y seguimiento del proyecto se gestionan mediante **Notion**, donde se documentan las tareas, el alcance (MVP), el modelo de datos, la API y las decisiones técnicas.

#### Arquitectura y enfoque técnico

El proyecto se desarrolla siguiendo una arquitectura **cliente-servidor**, con una clara separación entre frontend y backend:

* **Frontend:** desarrollado con **React Native y Expo**, permitiendo una única base de código para Android, iOS y web.
* **Backend:** implementado como una **API REST**, encargada de gestionar la lógica de negocio, la seguridad y el acceso a los datos.
* **Base de datos:** relacional (MySQL), diseñada para garantizar integridad y escalabilidad.
* **Autenticación:** basada en tokens (JWT), asegurando el acceso controlado a las funcionalidades.

Este enfoque facilita el trabajo en equipo, la escalabilidad del proyecto y la posible ampliación futura de la aplicación.
