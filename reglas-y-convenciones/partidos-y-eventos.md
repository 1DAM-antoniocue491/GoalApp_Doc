# Partidos y eventos

Esta sección define las reglas de negocio relacionadas con la gestión de partidos y el registro de eventos dentro de una liga. Su objetivo es garantizar que los encuentros se desarrollen de forma coherente, que los datos sean consistentes y que las estadísticas reflejen fielmente lo ocurrido en el terreno de juego.

## **1. Gestión de Partidos**

Los partidos representan los encuentros oficiales entre equipos dentro de una liga. Cada partido sigue un ciclo de vida definido por estados y está sujeto a restricciones específicas.

### **Reglas generales de los partidos**

* Todo partido pertenece a una **liga**.
* Un partido siempre enfrenta a **dos equipos distintos**.
* Ambos equipos deben pertenecer a la **misma liga**.
* Un partido debe tener:
  * Fecha y hora programadas
  * Estado válido
  * Equipos correctamente asignados

### **Estados del partido**

Un partido puede encontrarse en uno de los siguientes estados:

* **PROGRAMADO** El partido está planificado pero aún no ha comenzado.
* **EN CURSO** El partido se está disputando.
* **FINALIZADO** El partido ha terminado y su resultado queda consolidado.

### **Reglas de transición entre estados**

#### **De PROGRAMADO → EN CURSO**

* Se permite cuando llega la hora del partido o cuando el delegado lo inicia manualmente.
* Al pasar a EN CURSO:

{% hint style="danger" %}
No se pueden modificar los equipos participantes.
{% endhint %}

{% hint style="danger" %}
No se puede cambiar la convocatoria.
{% endhint %}

#### **De EN CURSO → FINALIZADO**

* Solo puede realizarse cuando el partido ha concluido.
* Al finalizar:
  * El resultado queda **consolidado**.
  * Se recalculan:
    * Clasificación
    * Estadísticas de jugadores
    * Estadísticas de equipos

#### **Edición de fecha y hora**

{% hint style="success" %}
Mientras el partido está en **PROGRAMADO**, se puede modificar fecha y hora.
{% endhint %}

{% hint style="danger" %}
No se permite modificar fecha u hora si el partido está **EN CURSO** o **FINALIZADO**.
{% endhint %}

## **2. Registro de Eventos del Partido**

Los eventos representan acciones ocurridas durante el partido, como goles, tarjetas y cambios. Son fundamentales para generar estadísticas y determinar el resultado.

### **Reglas generales de los eventos**

* Solo el **delegado de campo** puede registrar eventos.
* Todo evento debe incluir:
  * Tipo de evento
  * Minuto de juego
  * Jugador asociado
* No se permite registrar eventos si el partido **no está EN CURSO**.
* Todo evento debe estar asociado a un **jugador convocado** para el partido.

### **Tipos de eventos permitidos**

* **Gol**
* **Tarjeta amarilla**
* **Tarjeta roja**
* **Cambio**
* **MVP del partido**

El sistema puede ampliarse con nuevos tipos de eventos en el futuro.

### **Reglas específicas de eventos**

#### **Goles**

* Afectan directamente al marcador del partido.
* Se suman automáticamente a:
  * Goles del equipo
  * Estadísticas del jugador

#### **Tarjetas**

* **Tarjeta amarilla**: se registra sin restricciones adicionales.
* **Tarjeta roja**: se registra sin restricciones adicionales.

#### **Cambios**

* Solo pueden realizarse entre jugadores convocados.
* No se permiten cambios que contradigan convocatoria o alineación definida.

#### **MVP**

* Solo puede asignarse una vez por partido.
* Debe asignarse a un jugador participante.

## **3. Relación entre partidos, eventos y estadísticas**

* Los eventos son la **única fuente** para generar estadísticas.
* Si se modifica o elimina un evento:
  * Se recalculan estadísticas del jugador.
  * Se recalculan estadísticas del equipo.
  * Se recalcula la clasificación si corresponde.
* El resultado final del partido depende exclusivamente de los eventos registrados.
