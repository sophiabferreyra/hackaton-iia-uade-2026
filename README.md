# <T21> · <¿El NPC aliado cura al jugador ahora?>

**Integrantes:** <Julieta Ferro> · <Sophia Ferreyra>
**IA declarada:** <Chat GPT>
**Pista:** <Agente>
**Publicación en LinkedIn:** <link>

---

## 1. Formulación y PEAS

**La pregunta.** <Para cada caso, ¿La IA debe usar una poción para curar al jugador? SÍ = si no lo cura ahora, el jugador muere en los próximos segundos.>

| PEAS | Su sistema |
|---|---|
| Medida de rendimiento | <Mantener vivo al jugador, evitar muertes y administrar eficientemente los recursos de curación. Se prioriza evitar la muerte del jugador por encima de ahorrar recursos> |
| Entorno | <Videojuego cooperativo, situaciones de combate, jugador, NPC aliado, enemigos y recursos disponibles> |
| Actuadores | <Usar una poción para curar al jugador o decidir no utilizarla> |
| Sensores | <Nivel de vida del jugador, daño recibido, cantidad de enemigos, intensidad del combate, pociones disponibles y riesgo de muerte> |

**Objetivo y métrica.** <El objetivo es lograr que el NPC tome decisiones correctas sobre cuándo curar al jugador, priorizando su supervivencia y evitando gastar pociones cuando no sea necesario. 
La métrica evalúa qué tan bien decide el NPC teniendo en cuenta los dos tipos de errores: falsos positivos: penalizar el uso innecesario de pociones, y falsos negativos: penalizar con mayor gravedad las decisiones que provocan la muerte del jugador. Debe priorizar la supervivencia del jugador por encima del ahorro de recursos. 
No son lo mismo, el objetivo indica qué queremos que logre el agente; la métrica establece cómo vamos a medir si lo está logrando. En este caso, no alcanza con contar decisiones correctas; también hay que considerar la gravedad de cada error.>

## 2. El sistema

**Cómo decide.** <Agente: la regla con la que elige la acción.>

**Variables que usa y por qué.** <Las variables que usa son: Vida del jugador (%),	Enemigos cerca (cantidad), y	Pociones restantes (cantidad) debido a que es importante tenerlas en cuenta a todas para tomar una decisión efectiva>

**Cómo se corre en vivo.** <Pasos concretos para resolver un caso nuevo: https://colab.research.google.com/drive/18CDGtFdjNo9CX9uqCoX2ZqqitmpNpaWq?usp=sharing >

**Dos casos de ejemplo.**

| Caso inventado | Valores | Salida del sistema |
|---|---|---|
| Caso inventado | Vida | Enemigos | Posiones | Salida del sistema |
| A | <15> | <5> | <3> | <SÍ> |
| B | <80> | <1> | <4> | <NO> |

## 3. Medición

**Entrenamiento (casos 1–14)**

| | Predice SÍ | Predice NO |
|---|---|---|
| **Real SÍ** | VP = <9> | FN = <0> |
| **Real NO** | FP = <2> | VN = <3> |

**Prueba (casos 15–20)**

| | Predice SÍ | Predice NO |
|---|---|---|
| **Real SÍ** | VP = <2> | FN = <0> |
| **Real NO** | FP = <2> | VN = <2> |

| Métrica | Entrenamiento | Prueba |
|---|---|---|
| Exactitud | <0.86> | <0.67> |
| Precisión | <0.82> | <0.5> |
| Sensibilidad | <1.0> | <1.0> |
| Especificidad | <0.6> | <0.5> |

**Entrenamiento contra prueba.** <Sí. El modelo obtiene mejores resultados con los datos de entrenamiento que con los datos de prueba porque durante el entrenamiento el modelo aprende a partir de 14 casos conocidos. Luego, en la prueba, se enfrenta a 6 casos nuevos que no utilizó para aprender. Por eso, su rendimiento puede variar. Hay indicios de una disminución del rendimiento en los datos de prueba, pero no podemos afirmar que exista sobreajuste. El modelo demuestra cierta capacidad de generalización, ya que logra identificar correctamente todos los casos en los que el jugador necesita curación (sensibilidad del 100%), incluso con datos nuevos. Sin embargo, comete más errores al decidir cuándo no debe curar.>

## 4. El error más caro

<El falso negativo es peor, porque significa que el NPC decide NO CURAR cuando el jugador realmente necesita ayuda. Como consecuencia, el jugador puede morir, perder su progreso y perjudicar la experiencia de juego. En cambio, un falso positivo solamente implica gastar una poción innecesariamente. 
Aumentamos el costo del falso negativo de 10 a 20, manteniendo el falso positivo en 2. Esto redujo el umbral de decisión de 0,1667 a 0,09. De esta manera, el NPC necesita una menor probabilidad estimada para decidir curar al jugador, priorizando su supervivencia por encima del ahorro de pociones.>

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
| 1 | <Verificar PEAS> | <Algunas adiciones al PEAS> | <Nada, buscabamos saber si le parecia correcto> |
| 2 | <Sistema: ¿Agente o reglas?> | <Agente> | <Reglas. Porque si la regla es muy rígida, puede cometer errores graves. Por otro lado, el agente maneja mucho mejor los escenarios de riesgo y los costos de los errores> |
| 3 | <Código> | <Código> | <La primera versión del código debido a que falaba los casos del entrenamiento> |
| 4 | <Sobreajuste o generalización> | <Respuesta> | <Nada> |
| 5 | <Reducción de FN> | <El cambio en el umbral> | <La madificación del árbol de decisión debido a que no habia cambios> |
| 6 | <> | <> | <> |
**Corridas contra el evaluador**

| Corrida | Nota | Agujero que encontró | Qué cambiamos |
|---|---|---|---|
| 1 | <> | <> | <> |
