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
| Medida de rendimiento | <Mantener vivo al jugador, evitar el gasto innecesario de pociones y reducir las decisiones incorrectas> |
| Entorno | <Videojuego cooperativo, situaciones de combate, jugador, NPC aliado, enemigos y recursos disponibles> |
| Actuadores | <Usar una poción para curar al jugador o decidir no utilizarla> |
| Sensores | <Nivel de vida del jugador, daño recibido, cantidad de enemigos, intensidad del combate, pociones disponibles y riesgo de muerte> |

**Objetivo y métrica.** <Lograr que el NPC tome decisiones correctas sobre cuándo curar al jugador, priorizando su supervivencia y evitando gastar pociones cuando no sea necesario. Evaluar qué tan bien decide el NPC teniendo en cuenta los dos tipos de errores:
falsos positivos: penalizar el uso innecesario de pociones, y falsos negativos: penalizar con mayor gravedad las decisiones que provocan la muerte del jugador. La métrica debe priorizar la supervivencia del jugador por encima del ahorro de recursos. No son lo mismo, el objetivo indica qué queremos que logre el agente; la métrica establece cómo vamos a medir si lo está logrando. En este caso, no alcanza con contar decisiones correctas: también hay que considerar la gravedad de cada error.>

## 2. El sistema

**Cómo decide.** <Agente: la regla con la que elige la acción.>

**Variables que usa y por qué.** <>

**Cómo se corre en vivo.** <>

**Dos casos de ejemplo.**

| Caso inventado | Valores | Salida del sistema |
|---|---|---|
| A | <> | <> | <> | <SÍ/NO> |
| B | <> | <> | <> | <SÍ/NO> |

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

**Entrenamiento contra prueba.** <>

## 4. El error más caro

<>

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
| 2 | <> | <> | <> |
| 3 | <> | <> | <> |
| 4 | <> | <> | <> |
**Corridas contra el evaluador**

| Corrida | Nota | Agujero que encontró | Qué cambiamos |
|---|---|---|---|
| 1 | <> | <> | <> |
