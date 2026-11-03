# <T19> · <¿Bajamos la dificultad de este jefe?>

**Integrantes:** <Julieta Ferro> · <Sophia Ferreyra>
**IA declarada:** <Chat GPT>
**Pista:** <Reglas>
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

**Cómo decide.** <Reglas: la lista de reglas si‑entonces.>

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
| **Real SÍ** | VP = <> | FN = <> |
| **Real NO** | FP = <> | VN = <> |

**Prueba (casos 15–20)**

| | Predice SÍ | Predice NO |
|---|---|---|
| **Real SÍ** | VP = <> | FN = <> |
| **Real NO** | FP = <> | VN = <> |

| Métrica | Entrenamiento | Prueba |
|---|---|---|
| Exactitud | <> | <> |
| Precisión | <> | <> |
| Sensibilidad | <> | <> |
| Especificidad | <> | <> |

**Entrenamiento contra prueba.** <¿Hay diferencia? ¿Por qué? ¿Sobreajuste o generalización?>

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

**Corridas contra el evaluador**

| Corrida | Nota | Agujero que encontró | Qué cambiamos |
|---|---|---|---|
| 1 | <> | <> | <> |
