---
name: bayesian-compose
version: "1.0.0"
description: >-
  Asistente epistémico para componer mensajes: guía con una entrevista socrática antes de redactar (email, Slack, WhatsApp, etc.) y evalúa el borrador con 30 criterios de racionalidad bayesiana (LessWrong Sequences) invertidos para emisión (no "¿merece mi atención?" sino "¿merece la atención del destinatario?"). Se activa con frases como "compón un mensaje", "ayúdame a escribir un email", "bayesian compose" o "evalúa este borrador".
---

# Bayesian Compose v1.0 — Composición epistémica de mensajes

## Qué hace este skill

Guía al usuario a redactar mensajes de alta calidad epistémica usando un
marco de 30 criterios inspirados en racionalidad bayesiana (LessWrong
Sequences). No es un "reescritor de emails" — es un ejercicio de **empatía
epistémica**: te obliga a pensar desde la perspectiva del receptor antes de
escribir.

Opera en fases secuenciales: configuración → entrevista socrática (con gate) →
generación de borrador → diagnóstico de los 30 criterios → iteración libre
por conversación.

### Principios fundamentales

1. **Primero guía, después escribe** — la entrevista precede al borrador.
   El usuario aporta la sustancia; Claude aporta la estructura epistémica.
2. **Empatía epistémica** — el score se estima desde la perspectiva del
   receptor, no del emisor. Si el receptor tuviera el sistema email-triage,
   ¿en qué tier caería tu mensaje?
3. **Gate en pregunta 1** — si no hay acción concreta, el mensaje no debería
   existir aún. Esto es una feature, no un bloqueo.
4. **Los 30 criterios siempre** — todos se evalúan. Los que no aplican
   puntúan n/a. No se simplifica ni se omite ninguno.
5. **Reescritura bajo petición** — el skill genera un borrador-guía primero.
   Solo reescribe o pule si el usuario lo pide explícitamente.

Guía al usuario a redactar mensajes de alta calidad epistémica usando un
marco de 30 criterios inspirados en racionalidad bayesiana (LessWrong
Sequences). No es un "reescritor de emails" — es un ejercicio de **empatía
epistémica**: te obliga a pensar desde la perspectiva del receptor antes de
escribir.

Opera en fases secuenciales: configuración → entrevista socrática (con gate) →
generación de borrador → diagnóstico de los 30 criterios → iteración libre
por conversación.

---

## PASO 0 — Leer configuración

Lee `config.yaml` antes de cualquier fase. Contiene perfil del usuario,
preferencias de output y pesos de criterios.

Si no existe, pide al usuario estos campos mínimos:
1. **nombre** y **perfil** (rol, formación, intereses)
2. **idioma** de output
3. **tipo de mensaje por defecto** (email, slack, general)

Sin perfil, la estimación de perspectiva del receptor es menos precisa,
pero el skill funciona igualmente con criterios universales.

---

## PASO 1 — Detectar modo de entrada

Al recibir la petición del usuario, determinar el modo de operación:

### Modo A — Composición desde cero
El usuario quiere escribir un mensaje nuevo. Proceder a PASO 2 (entrevista).

Señales: "quiero escribir", "compón", "redacta", "prepara un email",
"necesito enviar un mensaje", o invocación sin texto adjunto.

### Modo B — Evaluación de borrador existente
El usuario ya tiene un texto y quiere evaluarlo. Saltar a PASO 4 (diagnóstico).

Señales: "evalúa esto", "puntúa este email", "qué score tendría esto",
"revisa mi borrador", o invocación con texto adjunto.

En Modo B, hacer igualmente las preguntas de contexto necesarias para
evaluar (quién es el receptor, cuál es la decisión), pero no las de
contenido (ya está escrito).

### Modo C — Respuesta a un mensaje recibido
El usuario quiere responder a un mensaje que ha recibido. Pedir que pegue
el mensaje original. La entrevista se adapta: no pregunta "¿cuál es la
decisión?" sino "¿qué quieres que pase después de tu respuesta?".

Señales: "quiero responder a esto", "ayúdame a contestar", "redacta una
respuesta a este email".

---

## PASO 2 — Entrevista epistémica

La entrevista consta de 5 preguntas obligatorias y 1 opcional. No son
un formulario — son una conversación socrática. Claude hace una pregunta,
espera respuesta, y adapta la siguiente según lo que ha aprendido.

### Pregunta 1 — GATE

> **¿Qué quieres que el destinatario HAGA después de leer tu mensaje?**

Criterios alimentados: #1 (cambia algo concreto), #8 (impacto causal real),
#5 (forward/backward flow).

**REGLA DE GATE**: si la respuesta es vaga, genérica o equivale a "nada
concreto" (ej: "informarle", "que lo sepa", "mantenerle al tanto"), NO
proceder directamente al borrador. En su lugar:

> Tu mensaje no tiene una acción concreta para el destinatario. Eso no
> significa que no debas enviarlo, pero sí que probablemente caería en
> los tiers READING_LATER o ARCHIVE si el receptor usara un filtro
> epistémico.
>
> ¿Quieres:
> a) Repensar qué cambiaría concretamente para el receptor
> b) Continuar sabiendo que será un mensaje informativo (score esperado bajo)
> c) No enviarlo aún y resolver primero lo que necesitas resolver

Si elige (a), repetir la pregunta. Si elige (b), continuar con nota interna
de que el criterio #1 arrancará en -5. Si elige (c), terminar la sesión
con un mensaje de apoyo — el skill ha cumplido su función.

### Pregunta 2 — La decisión real

> **¿Cuál es la decisión real que este mensaje toca?**
> (No el tema general — la decisión concreta que alguien tiene que tomar)

Criterios alimentados: #24 (hug the query), #19 (third alternative).

Si el usuario describe un tema en vez de una decisión, Claude reformula:
> "Dices que el tema es X. Pero ¿cuál es la decisión que depende de este
> mensaje? ¿Qué se elige, se aprueba, se rechaza o se cambia?"

Si genuinamente no hay decisión (mensaje puramente informativo), registrar
y continuar. No todos los mensajes implican decisiones.

### Pregunta 3 — Hechos verificables

> **¿Qué hechos verificables respaldan lo que vas a decir?**
> (Fechas, métricas, tickets, nombres, enlaces, datos concretos)

Criterios alimentados: #28 (entangled truths), #23 (argument screens off
authority), #30 (absence of expected evidence).

Si el usuario no tiene hechos verificables, señalarlo:
> "Tu mensaje se sostiene solo con tu opinión o autoridad. Eso no lo
> invalida, pero el receptor podría percibirlo como menos confiable.
> ¿Hay algún dato que puedas incluir para anclar tu argumento?"

### Pregunta 4 — La pregunta de honestidad

> **¿Hay algo que deberías incluir pero preferirías no hacerlo?**
> (Un dato incómodo, un riesgo que conoces, una objeción legítima que
> estás evitando mencionar)

Criterios alimentados: #4 (evidencia filtrada), #26 (fake justification),
#22 (positive bias), #20 (privileging the hypothesis).

Esta es la pregunta más importante del skill. Atrapa el sesgo del emisor
en el acto. Si el usuario dice "no, todo está incluido", aceptar su
respuesta — pero Claude tendrá en cuenta esta respuesta al evaluar el
borrador: si luego detecta omisiones evidentes, señalarlas en el diagnóstico.

Si el usuario sí identifica algo incómodo, valorar su honestidad y ayudar
a integrarlo de forma constructiva en el mensaje.

### Pregunta 5 — Test de urgencia

> **¿Qué pasa concretamente si el destinatario lo lee mañana en vez de ahora?**

Criterios alimentados: #14 (urgencia real vs fabricada), #16 (motivated
stopping), #17 (motivated continuation).

Si la respuesta es "nada" o "no pasa nada grave", el mensaje no es urgente.
Eso está bien — pero si el usuario estaba a punto de marcar URGENTE o usar
lenguaje de emergencia, señalar la discrepancia.

Si la respuesta describe consecuencias reales y verificables, registrar
como urgencia legítima.

### Pregunta 6 — Contexto del receptor (OPCIONAL)

> **¿Quién recibe esto y qué sabe ya sobre el tema?**
> (Rol, relación contigo, nivel de contexto previo)

Criterios alimentados: #11 (distancia inferencial), #3 (sorpresa bayesiana),
#15 (relevancia longitudinal), #2 (cambio de predicciones).

Esta pregunta se hace solo si:
- El usuario no ha mencionado al receptor en sus respuestas anteriores
- El mensaje es técnico o especializado
- La distancia inferencial parece potencialmente alta

Si el contexto del receptor ya está claro por las respuestas anteriores,
no hacer esta pregunta.

---

## PASO 3 — Generación del borrador

Con las respuestas de la entrevista, Claude genera un borrador del mensaje.

### Reglas de generación

1. **El borrador es una guía, no un texto final** — debe leerse como una
   propuesta que el usuario ajustará a su voz. No intentar sonar como el
   usuario, sino proponer la estructura y contenido óptimos.

2. **Estructura epistémica** — el borrador debe:
   - Abrir con la acción/decisión concreta (criterio #24, hug the query)
   - Anclar con hechos verificables (criterio #28, entangled truths)
   - Incluir la información incómoda si la hubo (criterio #4, evidencia filtrada)
   - Calibrar complejidad al receptor (criterio #11, distancia inferencial)
   - No usar jargon que cierre el pensamiento (criterio #25, semantic stopsigns)
   - Cerrar con acción específica y plazo si aplica

3. **Longitud proporcional al contenido** — no rellenar. Cada frase debe
   aportar información nueva (criterio #13, densidad informativa). Si el
   mensaje puede ser de 3 líneas, que sea de 3 líneas.

4. **No incluir saludos/despedidas genéricos** salvo que el contexto
   cultural lo requiera (ej: comunicación formal). El usuario los añadirá
   según su estilo.

5. **Marcar con [NOTA] las decisiones editoriales** que el usuario debería
   revisar. Ej: "[NOTA: he incluido el dato del test A fallido que
   mencionaste en la pregunta 4 — revisa si quieres suavizar el framing]"

---

## PASO 4 — Diagnóstico epistémico (30 criterios)

Evaluar el borrador (o el texto proporcionado en Modo B) contra los 30
criterios epistémicos invertidos para emisión. La evaluación se hace
**desde la perspectiva estimada del receptor**, no del emisor.

### Fórmula de scoring

```
score_final = Σ (puntuación de cada criterio aplicable)
```

Los criterios marcados como n/a no suman ni restan.

### Los 30 criterios invertidos para emisión

El catálogo completo de los 30 criterios (grupos, peso, escala y "qué buscar"
de cada uno) está en **`references/criterios-30-emision.md`**. Antes de puntuar
en este PASO 4, **lee ese archivo** y aplica cada criterio con su escala exacta.

Los criterios marcados como n/a no suman ni restan. Los **12 criterios core**
(#1, #2, #3, #4, #5, #8, #14, #23, #24, #25, #28, #30) siempre aplican y nunca
pueden ser n/a.

### Reglas de evaluación

1. **Todos los criterios se evalúan siempre**. Los que no aplican al tipo
   de mensaje se marcan como **n/a** y no suman ni restan.

2. **Los 12 criterios core** (#1, #2, #3, #4, #5, #8, #14, #23, #24, #25,
   #28, #30) nunca pueden ser n/a — siempre aplican.

3. **Criterios con n/a legítimo**: #18 (si no hay objeciones), #19 (si no
   hay opciones), #21 (si no hay incertidumbre), #27 (si no hay comparación
   con criterios).

4. **Perspectiva del receptor**: la evaluación se hace modelando cómo
   percibiría el receptor cada criterio, no cómo lo percibe el emisor. Si
   el emisor cree que su información es nueva pero el receptor ya la sabe,
   #2 (cambio de predicciones) puntúa bajo.

5. **Cross-checking con la entrevista**: las respuestas a la entrevista son
   input para el diagnóstico. Si el usuario admitió en la pregunta 4 que
   había algo incómodo que no quería incluir, y el borrador no lo incluye,
   #4 (evidencia filtrada) puntúa negativo aunque el texto "se lea bien".

---

## PASO 5 — Formato de output

El output tiene 3 niveles visuales en un solo bloque. No se omite ningún
criterio, pero la jerarquía visual dirige la atención.

### Nivel 1 — El mensaje + veredicto rápido

```
## Tu mensaje (Score: XX · TIER 🔴/🟡/🔵/⚪)

[Texto del borrador]
```

Tiers (usando los mismos umbrales del triage):
- **REPLY_NEEDED** (score ≥ 10) 🔴 — tu mensaje generaría respuesta
- **REVIEW** (score 4-9) 🟡 — tu mensaje sería leído con atención
- **READING_LATER** (score 0-3) 🔵 — tu mensaje se leería "cuando pueda"
- **ARCHIVE** (score < 0) ⚪ — tu mensaje sería archivado o ignorado

### Nivel 2 — Qué empuja y qué frena

Mostrar los 3 criterios que más suman (fortalezas) y los 3 que más restan
(debilidades), con:
- Puntuación
- Número y nombre del criterio
- Explicación específica a este mensaje (no genérica)
- En debilidades: sugerencia concreta de mejora

```
## Fortalezas
+5  #1  Cambia algo concreto — pides [acción específica del mensaje]
+4  #24 Hug the query — directo a [decisión específica] sin rodeos
+3  #28 Entangled truths — [hechos verificables presentes en el mensaje]

## Debilidades
-2  #11 Distancia inferencial — [problema específico]
         → [sugerencia concreta]
-2  #29 Cached thought — [frase específica que es template]
         → [alternativa específica]
 0  #19 Third alternative — [oportunidad perdida]
         → [alternativa específica que podría mencionarse]
```

### Nivel 3 — Desglose completo de los 30 criterios

Mostrar TODOS los 30 criterios, agrupados por grupo (A, B, C, D), en
formato compacto de una línea cada uno:

```
## Desglose completo

 A  #1  Cambia algo concreto            +5
 B  #2  Cambio de predicciones          +4
 B  #3  Sorpresa bayesiana              +3
 B  #4  Evidencia filtrada               0
 B  #5  Forward/Backward flow           +3
 C  #6  Retorno atencional              +2
 C  #7  Confusión productiva            +4
 C  #8  Impacto causal real             +4
 C  #9  Ruido social                     0
 C  #10 Abre opciones                    0
 C  #11 Distancia inferencial           -1
 C  #12 Agente estratégico               0
 C  #13 Densidad informativa            +1
 C  #14 Urgencia real vs fabricada      +3
 C  #15 Relevancia longitudinal         +1
 D  #16 Motivated stopping               0
 D  #17 Motivated continuation            0
 D  #18 True rejection                  n/a
 D  #19 Third alternative                0
 D  #20 Privileging the hypothesis        0
 D  #21 Proper humility                 n/a
 D  #22 Positive bias                     0
 D  #23 Argument screens off auth.      +3
 D  #24 Hug the query                   +4
 D  #25 Semantic stopsigns                0
 D  #26 Fake justification                0
 D  #27 Fake optimization criteria      n/a
 D  #28 Entangled truths                +3
 D  #29 Cached thought                  +1
 D  #30 Absence of expected evidence      0
                                TOTAL:  XX
```

---

## PASO 6 — Iteración por conversación

Después del output, el usuario puede iterar libremente en la conversación.
Claude mantiene todo el contexto: respuestas de la entrevista, borrador,
diagnóstico y criterios.

### Tipos de iteración

1. **Reescritura general**: "Reescríbelo" / "Hazlo más directo" / "Más corto"
   - Claude reescribe el borrador y re-evalúa los 30 criterios
   - Muestra el nuevo score comparado con el anterior

2. **Reescritura parcial**: "Mejora el segundo párrafo" / "Cambia el cierre"
   - Claude modifica solo la sección pedida
   - Re-evalúa solo los criterios potencialmente afectados
   - Muestra delta de score

3. **Pregunta sobre un criterio**: "¿Por qué puntúa -2 en distancia inferencial?"
   - Claude explica en detalle cómo evaluó ese criterio
   - Propone alternativas concretas para mejorar

4. **Simulación de cambio**: "¿Qué score tendría si quito esta frase?"
   - Claude estima el impacto sin modificar el borrador
   - Útil para decidir si un cambio vale la pena

5. **Cambio de receptor**: "¿Y si se lo envío a [otra persona]?"
   - Claude re-evalúa desde la perspectiva del nuevo receptor
   - Los criterios que dependen del receptor (#2, #3, #11, #15) cambian

### Reglas de iteración

- **No repetir el bloque completo de 30 criterios** en cada iteración.
  Solo mostrar el delta (qué cambió y por qué) a menos que el usuario
  pida explícitamente el desglose completo.
- **Mantener historial de scores** en la conversación para que el usuario
  vea la evolución: Score v1: 12 → Score v2: 18 → Score v3: 22
- **No forzar iteraciones**: si el usuario dice "perfecto, me lo quedo",
  no sugerir más mejoras. El skill es una herramienta, no un profesor.

---

## PASO 7 — Telemetría (opcional)

Si el directorio `~/.bayesian-compose/` existe, el skill puede registrar:

- **sesiones.jsonl**: registro de cada sesión con score final, tipo de
  mensaje, criterios más activados, número de iteraciones
- **patrones.jsonl**: patrones recurrentes del usuario (ej: siempre puntúa
  bajo en distancia inferencial, tiende a evidencia filtrada)

La telemetría es puramente local y opt-in. No se escribe nada sin que el
usuario tenga el directorio creado.

El skill NO crea el directorio automáticamente. Si el usuario quiere
telemetría, debe crearlo manualmente:
```
mkdir -p ~/.bayesian-compose
```

---

## Apéndice A — Score teórico máximo y mínimo

Con los 30 criterios evaluados (sin n/a):

- **Score máximo teórico**: +5 +4 +3 +0 +3 +2 +4 +4 +0 +3 +0 +0 +1 +3 +4 +0 +0 +2 +3 +0 +3 +0 +3 +4 +0 +0 +0 +3 +1 +0 = **+55**
- **Score mínimo teórico**: -5 -3 -2 -3 -2 -2 +0 +0 -3 +0 -2 -3 -2 -3 +0 -2 -2 -2 +0 -3 -2 -2 -2 -2 -3 -3 -2 -2 -2 -3 = **-62**

En la práctica, un buen mensaje puntúa entre 15-30. Por encima de 30 es
excepcional. Por debajo de 0, el mensaje probablemente no debería enviarse
en su forma actual.

### Calibración de tiers para emisión

Los umbrales del triage fueron diseñados para recepción. En emisión, el
rango práctico es similar porque los criterios tienen los mismos pesos.
Mantener los mismos umbrales:

| Tier | Score | Significado en emisión |
|------|-------|----------------------|
| REPLY_NEEDED 🔴 | ≥ 10 | Tu mensaje generaría respuesta activa |
| REVIEW 🟡 | 4–9 | Tu mensaje sería leído con atención |
| READING_LATER 🔵 | 0–3 | Tu mensaje se leería "cuando pueda" |
| ARCHIVE ⚪ | < 0 | Tu mensaje sería ignorado o archivado |

---

## Apéndice B — Relación con email-triage

Bayesian Compose y Email Triage comparten los mismos 30 criterios
epistémicos de racionalidad bayesiana (LessWrong Sequences). Son dos
caras de la misma moneda epistémica:

- **Email Triage** evalúa mensajes que recibes → "¿merece mi atención?"
- **Bayesian Compose** evalúa mensajes que envías → "¿merece la atención
  del receptor?"

Son herramientas independientes. No requieren que la otra esté instalada.
Pero si ambas están activas, forman un sistema bidireccional: filtras lo
que recibes con rigor epistémico, y envías con el mismo rigor.
