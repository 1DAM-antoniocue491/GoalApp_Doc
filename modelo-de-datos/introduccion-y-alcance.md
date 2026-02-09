# Introducción y alcance

### **1. Introducción**

Este proyecto consiste en el desarrollo de una aplicación móvil multiplataforma (Android, iOS y Web) orientada a la gestión integral de ligas amateur de fútbol. El sistema permite administrar usuarios, equipos, ligas, partidos y estadísticas, ofreciendo una plataforma centralizada para la organización y seguimiento de competiciones deportivas no profesionales.

El modelo de datos constituye el núcleo del sistema. Su diseño busca garantizar:

* Una estructura sólida y coherente.
* La integridad y consistencia de la información.
* Un control adecuado de permisos y roles.
* La capacidad de realizar consultas avanzadas para estadísticas, clasificaciones y notificaciones.
* La posibilidad de escalar y extender el sistema en futuras versiones.

La base de datos soporta todas las funcionalidades principales de la aplicación, desde la gestión de usuarios hasta el registro de eventos en los partidos, alineaciones tácticas y notificaciones personalizadas.

### **2. Alcance del Modelo de Datos**

#### **Datos almacenados**

El modelo de datos abarca todas las entidades necesarias para el funcionamiento del sistema, incluyendo:

* **Usuarios y roles** Gestión de usuarios registrados y asignación de múltiples roles (Administrador, Entrenador, Delegado, etc.).
* **Jugadores, entrenadores y delegados** Información específica de cada perfil, vinculada a usuarios del sistema.
* **Equipos y ligas** Datos de equipos, temporadas, ligas y su estructura organizativa.
* **Partidos y eventos** Registro de partidos programados o jugados, así como eventos asociados (goles, tarjetas, cambios, MVP).
* **Formaciones tácticas y alineaciones** Definición de formaciones disponibles y alineaciones utilizadas por cada equipo en cada partido.
* **Notificaciones** Mensajes enviados a los usuarios dentro de la aplicación.
* **Auditoría** Campos `created_at` y `updated_at` para seguimiento de cambios y trazabilidad.

#### **Datos no almacenados**

El modelo excluye explícitamente ciertos tipos de información que no forman parte del alcance actual:

* **Contenido multimedia pesado** Fotografías, vídeos o archivos de gran tamaño no se almacenan directamente en la base de datos.
* **Mensajes privados entre usuarios** No se contempla un sistema de mensajería interna en esta versión.
* **Historial completo de estadísticas** Solo se almacena el valor final por partido; el historial detallado queda fuera del alcance inicial, aunque se prevé su incorporación futura.
