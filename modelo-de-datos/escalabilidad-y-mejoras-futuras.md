# Escalabilidad y mejoras futuras

El modelo de datos y la arquitectura del sistema han sido diseñados con un enfoque modular y extensible, permitiendo incorporar nuevas funcionalidades sin comprometer la estabilidad ni la coherencia del sistema. Esta sección describe las principales líneas de evolución previstas, así como las consideraciones técnicas que permitirán escalar la plataforma a medida que crezcan las necesidades de los usuarios y de las competiciones gestionadas.

## **1. Escalabilidad del Modelo de Datos**

El modelo actual está preparado para soportar:

#### **Crecimiento en volumen de datos**

* Aumento del número de usuarios, ligas, equipos y partidos.
* Incremento de eventos por partido sin afectar al rendimiento.
* Expansión del historial de temporadas.

#### **Múltiples competiciones simultáneas**

* Soporte para varias ligas activas al mismo tiempo.
* Gestión independiente de roles por liga.
* Aislamiento de datos entre competiciones.

#### **Nuevos tipos de entidades**

El diseño modular permite añadir:

* Nuevos roles.
* Nuevos tipos de eventos.
* Nuevas estadísticas.
* Nuevas estructuras de competición (playoffs, copas, torneos mixtos).

## **2. Mejoras Futuras Previstas**

A continuación se detallan las funcionalidades planificadas o previstas para futuras versiones del sistema.

### **Códigos QR**

El botón “Compartir” genera:

* Un **informe** para WhatsApp
* Un **QR** con acceso temporal

Esto permite compartir:

* Partidos
* Clasificaciones
* Estadísticas

El QR puede tener expiración o permisos limitados.

#### **Evento de Rojas**

Actualmente, el jugador que ha sido convocado tiene la posibilidad de participar en el siguiente partido.

En futuras versiones, se incorporará una restricción que impedirá que el jugador sea convocado, por lo que no podrá disputar el próximo encuentro.

#### **Descargar informes completos.**

En futuras versiones de la aplicación, se añadirá la posibilidad de visualizar un informe completo con toda la información relevante de la liga, incluyendo estadísticas, clasificación, resultados, equipos y jugadores. Además, desde esta sección se permitirá descargar dicho informe en formato PDF para su consulta o almacenamiento.

### **Historial completo de estadísticas**

Actualmente se almacena el valor final por partido. En futuras versiones se podrá:

* Registrar el historial completo de estadísticas por jugador.
* Consultar evolución de rendimiento por temporada.
* Generar informes avanzados.

Esto requerirá nuevas tablas para:

* Estadísticas por minuto.
* Estadísticas acumuladas.
* Versionado de datos.

### **Consultas optimizadas para estadísticas y clasificaciones**

Se incorporarán:

* Índices adicionales para acelerar consultas frecuentes.
* Vistas materializadas para rankings y clasificaciones.
* Cálculo automático de:
  * Goleadores
  * Asistentes
  * Porteros con más porterías a cero
  * Jugador del partido

### **Soporte para torneos y formatos avanzados**

Futuras versiones podrán incluir:

* Fase de grupos.
* Eliminatorias.
* Playoffs.
* Torneos amistosos.
* Copas paralelas a la liga.

Esto implicará nuevas entidades como:

* Grupos
* Rondas
* Llaves de eliminación

### **Predicción del jugador de la jornada mediante IA**

Se plantea integrar modelos de inteligencia artificial para:

* Predecir rendimiento de jugadores.
* Sugerir alineaciones óptimas.
* Detectar jugadores destacados.
* Generar informes automáticos.

El modelo de datos podrá ampliarse con:

* Métricas avanzadas.
* Datos históricos detallados.
* Resultados de modelos predictivos.

#### **Clasificación**

Actualmente, los resultados de los partidos no actualizan automáticamente la clasificación de la liga.

En futuras versiones, se implementará un sistema automático encargado de recalcular y actualizar la clasificación en función de los resultados obtenidos en cada encuentro.

## **3. Consideraciones Técnicas para la Escalabilidad**

#### **Normalización y modularidad**

El modelo está normalizado para evitar redundancias y facilitar ampliaciones.

#### **Integridad referencial**

Las relaciones bien definidas permiten añadir nuevas entidades sin romper el sistema.

#### **Rendimiento**

Se prevé:

* Uso de índices en campos críticos.
* Optimización de consultas de estadísticas.
* Posible uso de caché para datos de lectura frecuente.

#### **Compatibilidad futura**

El diseño actual permite:

* Migraciones controladas.
* Versionado de esquemas.
* Integración con APIs externas.

## **4. Resumen de Escalabilidad y Futuras Mejoras**

* El sistema está preparado para crecer en volumen, complejidad y número de competiciones.
* Se prevén mejoras en estadísticas, panel administrativo, IA y formatos de competición.
* El modelo de datos es modular, extensible y compatible con futuras migraciones.
* La arquitectura soporta múltiples temporadas, roles por liga y competiciones simultáneas.
