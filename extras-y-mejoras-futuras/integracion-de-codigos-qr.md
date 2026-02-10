# Integración de Códigos QR

Los **códigos QR** encajan de forma natural en tu proyecto porque resuelven varios problemas a la vez: acceso rápido, control de permisos, verificación en campo y simplificación del flujo de información. Este informe reúne su utilidad, impacto técnico y cómo se integran con tu arquitectura (FastAPI, JWT, triggers y roles).

### Función estratégica de los códigos QR en el proyecto

Los QR actúan como **puentes seguros** entre el mundo físico (campo, entrenadores, delegados, jugadores) y la información digital del sistema. Permiten acceder a datos o registrar acciones sin necesidad de navegar por menús o buscar elementos manualmente.

Su valor principal es que **reducen fricción** y **aumentan la fiabilidad operativa** durante los partidos.

### Para qué sirven en tu sistema

#### Acceso rápido a información del partido

Un QR asociado a un partido permite que delegados, entrenadores o jugadores accedan directamente a:

* Ficha del partido
* Convocatoria
* Eventos registrados
* Estado del encuentro

Esto evita búsquedas y reduce errores en momentos de presión.

#### Registro seguro de eventos en campo

El delegado escanea el QR del partido y accede directamente al módulo de eventos. El QR incluye un **token firmado (JWT)** que:

* Identifica el partido
* Verifica que el usuario tiene permisos
* Evita manipulación
* Permite acceso rápido sin navegar por la app

Esto agiliza registrar goles, tarjetas o sustituciones.

#### Control de permisos según rol

El QR no da acceso universal: el backend valida el token y el rol del usuario antes de permitir acciones.

Ejemplos:

* Un **Delegado** puede registrar eventos.
* Un **Entrenador** solo consulta.
* Un **Jugador** solo ve información.
* Un **Espectador** accede a datos públicos.

El QR no sustituye la seguridad; solo acelera el acceso.

#### Compartir información de forma controlada

El botón “Compartir” genera:

* Un **informe** para WhatsApp
* Un **QR** con acceso temporal

Esto permite compartir:

* Partidos
* Convocatorias
* Clasificaciones
* Estadísticas

El QR puede tener expiración o permisos limitados.

### Beneficios técnicos

#### Menos carga en el frontend

El QR evita pantallas intermedias y reduce navegación.

#### Seguridad sin almacenar estado

El JWT dentro del QR permite:

* Expiración
* Firma criptográfica
* Validación sin tabla adicional

Ideal para accesos rápidos.

#### Escalabilidad

El sistema puede manejar más ligas y partidos sin aumentar complejidad en la interfaz.

#### Integración natural con FastAPI

FastAPI valida el token, verifica permisos y devuelve datos en milisegundos.

### Beneficios operativos

#### Acceso universal

Jugadores, entrenadores y espectadores pueden consultar información sin necesidad de navegar por menús complejos.

#### Profesionalización del sistema

El uso de QR aporta una experiencia moderna y alineada con apps deportivas reales.

### Conclusión

Los códigos QR no son un añadido estético: son una **pieza clave** que conecta la operativa del campo con la lógica interna del sistema, garantizando:

* Acceso rápido
* Seguridad
* Control de permisos
* Escalabilidad
* Experiencia fluida

Son especialmente útiles en un entorno donde se registran eventos en tiempo real y donde los roles tienen permisos muy diferenciados.
