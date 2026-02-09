# Clasificación y Estadísticas

Esta sección define las reglas de negocio relacionadas con el cálculo de la clasificación de la liga y la generación de estadísticas de jugadores y equipos. Su objetivo es garantizar que los resultados reflejen fielmente lo ocurrido en los partidos y que los datos se mantengan siempre actualizados y consistentes.

## **5.1 Clasificación de la Liga**

La clasificación de la liga se genera automáticamente en función de los resultados consolidados de los partidos. El sistema recalcula la clasificación cada vez que un partido finaliza o se modifica un evento que afecte al marcador.

### **5.1.1 Reglas generales de la clasificación**

* La clasificación se recalcula **al finalizar cada partido**.
* La clasificación se basa exclusivamente en:
  * Resultados consolidados
  * Goles a favor
  * Goles en contra
  * Diferencia de goles
  * Puntos obtenidos
* Si se modifica un evento o un resultado, la clasificación se recalcula automáticamente.

### **5.1.2 Sistema de puntos**

Los puntos se asignan según el resultado final del partido:

{% hint style="success" %}
**Victoria:** 3 puntos
{% endhint %}

{% hint style="info" %}
**Empate:** 1 punto
{% endhint %}

{% hint style="danger" %}
**Derrota:** 0 puntos
{% endhint %}

Estos puntos se suman a la tabla de clasificación de cada equipo.

### **5.1.3 Actualización de la clasificación**

La clasificación se actualiza cuando:

* Un partido pasa a estado **FINALIZADO**.
* Se modifica un evento que afecte al marcador (por ejemplo, un gol).
* Se elimina un evento que afecte al marcador.
* Se corrige un resultado consolidado.

En todos los casos, el sistema recalcula automáticamente:

* Puntos
* Goles a favor
* Goles en contra
* Diferencia de goles
* Posición en la tabla

## **5.2 Estadísticas del Sistema**

Las estadísticas se generan exclusivamente a partir de los eventos registrados durante los partidos. No se permite la edición manual de estadísticas para garantizar integridad y transparencia.

### **5.2.1 Reglas generales de estadísticas**

* Las estadísticas se basan únicamente en los eventos del partido.
* No se permite la edición manual de estadísticas.
* Si se elimina o modifica un evento:
  * Se recalculan estadísticas del jugador.
  * Se recalculan estadísticas del equipo.
  * Se actualiza la clasificación si corresponde.
* Las estadísticas solo se generan para partidos en estado **FINALIZADO**.

### **5.2.2 Tipos de estadísticas generadas**

#### **Estadísticas de jugador**

* Goles anotados
* Tarjetas amarillas
* Tarjetas rojas
* Partidos jugados
* Minutos jugados (si se implementa en el futuro)
* MVP del partido

#### **Estadísticas de equipo**

* Goles a favor
* Goles en contra
* Diferencia de goles
* Puntos
* Posición en la clasificación
* Partidos ganados, empatados y perdidos

### **5.2.3 Reglas específicas de estadísticas**

#### **Goles**

* Se suman al jugador y al equipo.
* Afectan directamente al marcador del partido.

#### **Tarjetas**

* Se registran como parte de las estadísticas del jugador.
* Las tarjetas rojas pueden afectar la participación en eventos posteriores.

#### **Cambios**

* Se utilizan para determinar participación y minutos jugados (si se implementa).

#### **MVP**

* Solo puede haber un MVP por partido.
* Se suma a la estadística individual del jugador.

## **5.3 Relación entre clasificación, estadísticas y eventos**

* Los **eventos** son la única fuente de datos para estadísticas.
* Las **estadísticas** alimentan la clasificación.
* La **clasificación** se recalcula automáticamente al finalizar cada partido.
* Cualquier modificación en eventos → recalcula estadísticas → recalcula clasificación.
