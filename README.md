# <T21> · <¿El NPC aliado cura al jugador ahora?>

**Integrantes:** <Julieta Ferro> · <Sophia Ferreyra>
**IA declarada:** <Chat GPT>
**Pista:** <Agente>
**Publicación en LinkedIn:** <https://www.linkedin.com/feed/update/urn:li:activity:7524463547028860928/>

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

**Línea base trivial.** <Como línea base trivial, evaluamos un sistema que responde siempre SÍ: decide curar al jugador en el 100% de los casos sin importar el estado del combate.
Resultado de la línea base: En el conjunto de entrenamiento (14 casos), este sistema trivial acierta en los 9 casos donde realmente habías que curar, pero comete 5 Falsos Positivos (gasta pociones innecesariamente cuando la vida del jugador era alta y no había peligro). Su exactitud es del 64% con una sensibilidad de 1.0.
En comparación con nuestro modelo, nuestro sistema basado en árbol de decisiones con umbral de costos logra mejorar la exactitud de entrenamiento al 86% y reduce los Falsos Positivos a solo 2, manteniendo intacta la sensibilidad perfecta de 1.0. Es decir, nuestro modelo es mucho más eficiente gestionando las pociones que la regla trivial de curar siempre, sin sacrificar la vida del jugador.>

| Checklist (Clase 6) | Respuesta |
|---|---|
| ¿Qué datos? | <20 casos tabulados en T21.csv (14 de entrenamiento y 6 de prueba) con variables de vida del jugador, cantidad de enemigos y pociones restantes, sin datos de personas reales> |
| ¿Qué métrica? | <Exactitud, Precisión, Sensibilidad y Especificidad, calculadas rigurosamente a partir de la matriz de confusión para evaluar el impacto de los errores (Falsos Positivos vs. Falsos Negativos)> |
| ¿Comparado contra qué? | <Contra una línea base trivial que responde siempre SÍ (curar siempre), demostrando que nuestro modelo optimiza el uso de recursos sin perder sensibilidad ante el riesgo crítico de muerte del jugador.> |
| ¿Quién lo midió? | <El equipo de trabajo de forma automatizada mediante el script de Python en Google Colab> |

## 6. Riesgo: el camino completo

<El NPC recibe información sobre la vida del jugador, la cantidad de enemigos y las pociones disponibles. → El árbol de decisión analiza esos datos y estima la probabilidad de que el jugador necesite curación. → Según la probabilidad estimada y el umbral establecido, el NPC decide si utiliza una poción o no. → Si decide correctamente, puede salvar al jugador o conservar recursos. Si se equivoca, puede gastar una poción innecesariamente o dejar morir al jugador. Si los datos de entrada son incorrectos o incompletos, el modelo puede estimar mal la situación y tomar una decisión equivocada. Por ejemplo, si no detecta que el jugador está recibiendo mucho daño, puede decidir NO CURAR y provocar su muerte, causando que el jugador pierda su progreso.>

## 7. Bitácora

**Uso de la IA**

| # | Qué le pedimos | Qué aceptamos | Qué rechazamos y por qué |
|---|---|---|---|
| 1 | <Verificar PEAS> | <Algunas adiciones al PEAS> | <Nada, buscabamos saber si le parecia correcto> |
| 2 | <Sistema: ¿Agente o reglas?> | <Agente> | <Reglas. Porque si la regla es muy rígida, puede cometer errores graves. Por otro lado, el agente maneja mucho mejor los escenarios de riesgo y los costos de los errores> |
| 3 | <Código> | <Código> | <La primera versión del código debido a que falaba los casos del entrenamiento> |
| 4 | <Sobreajuste o generalización> | <Respuesta> | <Nada> |
| 5 | <Reducción de FN> | <El cambio en el umbral> | <La modificación del árbol de decisión debido a que no había cambio alguno en el resultado> |
| 6 | <> | <> | <> |
**Corridas contra el evaluador**

| Corrida | Nota | Agujero que encontró | Qué cambiamos |
|---|---|---|---|
| 1 | <8> | <Agujero principal: En la sección 2, ¿cómo decide su sistema? Si alguien no abre el Colab, ¿puede saber qué preguntas hace el árbol, en qué orden y con qué umbral elige curar? Otros: ¿Qué matriz tenían antes de bajar el umbral de 0,1667 a 0,09? ¿Algún caso pasó de NO a SÍ? · Sus sensores incluyen daño recibido, intensidad del combate y riesgo de muerte: ¿en qué columna de la ficha están?> | <Nada> |
