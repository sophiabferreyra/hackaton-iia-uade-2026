# <T19> · <¿Bajamos la dificultad de este jefe?>

**Integrantes:** <Julieta Ferro> · <Sophia Ferreyra>
**IA declarada:** <Chat GPT>
**Pista:** <Agente>
**Publicación en LinkedIn:** <link>

---

## 1. Formulación y PEAS

**La pregunta.** <Para cada caso, ¿La IA debe bajar la dificultad del jefe final? SÍ significa: que el jugador abandonaría el juego si no se reduce la dificultad>

| PEAS | Su sistema |
|---|---|
| Medida de rendimiento | <Porcentaje de jugadores que derrotan al jefe final> |
| Entorno | <Videojuego, jugador y jefe final> |
| Actuadores | <Reducir la dificultad o mantenarla> |
| Sensores | <Muertes seguidas, vida restante del jefe en el mejor intento, horas jugadas y porcentaje global de jugadores que derrotan al jefe> |

**Objetivo y métrica.** <El objetivo es aumentar la cantidad de jugadores que consiguen derrotar al jefe final, evitando reducir la dificultad innecesariamente. La métrica principal es el porcentaje de jugadores que derrotan al jefe.
No son lo mismo.

## 2. El sistema

**Cómo decide.** <Agente: la regla con la que elige la acción.>

**Variables que usa y por qué.** <Muertes seguidas, vida que le dejó al jefe y horas jugadas, Jugadores que derrotan al jefe (%global), Que otros hayan derrotado o no al jefe no determina que un jugador deje de jugar.>

**Cómo se corre en vivo.** <Pasos concretos para resolver un caso nuevo: [link al Colab, a la planilla o la cuenta a mano](https://colab.research.google.com/drive/1FHhbe5NdpQprvFhMENCLy6Obj2Nt_mSf?usp=sharing).>

**Dos casos de ejemplo.**

| Caso inventado | Valores | Salida del sistema |
|---|---|---|
| A | <5> | <20> | <40> | <NO> |
| B | <76> | <45> | <84> | <SÍ> |

## 3. Medición

**Entrenamiento (casos 1–14)**

| | Predice SÍ | Predice NO |
|---|---|---|
| **Real SÍ** | VP = <7> | FN = <0> |
| **Real NO** | FP = <0> | VN = <7> |

**Prueba (casos 15–20)**

| | Predice SÍ | Predice NO |
|---|---|---|
| **Real SÍ** | VP = <2> | FN = <2> |
| **Real NO** | FP = <0> | VN = <2> |

| Métrica | Entrenamiento | Prueba |
|---|---|---|
| Exactitud | <100%> | <66.67%> |
| Precisión | <100%> | <100%> |
| Sensibilidad | <100%> | <50%> |
| Especificidad | <100%> | <100%> |

**Entrenamiento contra prueba.** <Sí, existe una diferencia debido a la naturaleza de los datos. En el entrenamiento el agente alcanza un 100% de exactitud porque optimizó sus reglas basándose en esos casos específicos. Sin embargo, en la prueba (datos nuevos), la exactitud desciende a 66.67%. Esto evidencia un leve sobreajuste (overfitting), ya que el modelo se acopló tanto al conjunto de entrenamiento que le cuesta generalizar perfectamente ante escenarios totalmente nuevos>

## 4. El error más caro

<¿Es peor el falso positivo o el falso negativo en su problema? ¿Por qué, según la ficha? ¿Qué cambiaron en el sistema para cometer menos ese error?>

## 5. ¿Comparado contra qué?

**Línea base trivial.** <Qué resultado saca un sistema que responde siempre lo mismo, y cómo se compara el suyo.>

| Checklist (Clase 6) | Respuesta |
|---|---|
| ¿Qué datos? | <> |
| ¿Qué métrica? | <> |
| ¿Comparado contra qué? | <> |
| ¿Quién lo midió? | <> |

## 6. Riesgo: el camino completo

<Datos → modelo → decisión → consecuencia aplicado a su caso. Al menos un riesgo concreto.>

## 7. Bitácora

**Uso de la IA**

| # | Qué le pedimos | Qué aceptamos | Qué rechazamos y por qué |
|---|---|---|---|
| 1 | <Redactar el PEAS> | <La redacción de medida de rendimiento, entorno, actuadores y sensores> | <El objetivo y lamétrica eran incorrectos> |
| 2 | <Ayuda con el sistema> | <El código y como agregar un archivo al código> | <El primer código daba los resultados contrarios y el código no funcionaba correctamente con los archivos> |
| 3 | <Ayuda con el sistema> | <El código y como agregar un archivo al código> | <Cambiamos de pista debido a que no se llegaba a ningún lado> |

**Corridas contra el evaluador**

| Corrida | Nota | Agujero que encontró | Qué cambiamos |
|---|---|---|---|
| 1 | <> | <> | <> |
