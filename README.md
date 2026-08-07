# Bayesian Compose v1.1.0

Composición epistémica de mensajes para Claude Cowork y Claude Code.

> **Compatible con [Agent Plugins 1.0.0](https://agent-plugins.org/specification)** — el formato portátil de empaquetado de la Agentic AI Foundation (OpenAI, Amazon,
> Microsoft, Cursor y Vercel, con Google como *core maintainer*).
> El paquete lleva el manifiesto portable `plugin.json` en la raíz del plugin y
> el skill en `plugins/bayesian-compose/skills/bayesian-compose/SKILL.md`, así que cualquier cliente conformante lo descubre.
>
> **Funciona en ChatGPT.** El skill es texto: instrucciones y criterios, sin
> ejecución local, así que se instala activando **Work** en el selector de ChatGPT y
> añadiéndolo desde **Complementos**, por nombre o por la URL de este repositorio.
> Funciona igual que en Claude. Su frontmatter
> valida contra el conjunto cerrado de [Agent Skills](https://agentskills.io/specification),
> que es lo que ChatGPT, claude.ai y la Skills API exigen para aceptar la subida
> —una clave de más ahí no se ignora, falla con error duro—. Están también en el
> **plan gratuito**, con límites de uso.

## Qué hace

Te entrevista antes de escribir cualquier mensaje (email, Slack, WhatsApp, carta,
cualquier texto) para maximizar su calidad epistémica. Evalúa el borrador resultante
con 30 criterios de racionalidad bayesiana (LessWrong Sequences) desde la
**perspectiva estimada del receptor** — no desde la tuya.

No es un reescritor de emails. Es un ejercicio de **empatía epistémica**: te obliga
a pensar desde el otro lado antes de escribir.

## Filosofía

La mayoría de herramientas de escritura preguntan "¿suena bien?". Este plugin
pregunta algo distinto:

- ¿Cambia algo concreto para el receptor? (Value of Information)
- ¿Le estoy diciendo algo que no esperaba? (Bayesian Surprise)
- ¿Incluyo toda la evidencia, o solo la que me favorece? (Filtered Evidence)
- ¿Exploro de verdad o busco validación? (Forward vs Backward Flow)
- ¿La urgencia es real o fabricada? (Real vs Manufactured Urgency)
- ¿Está anclado a hechos verificables? (Entangled Truths)
- ¿Decidí primero y razoné después? (Fake Justification)
- ¿Hay algo incómodo que estoy omitiendo? (Absence of Expected Evidence)

El resultado no es un texto bonito, sino un mensaje que **merece la atención
del destinatario** — medido con los mismos 30 criterios que el plugin
[email-triage](https://github.com/novanoticia/email-triage-plugin) usa para
filtrar correo entrante.

## Relación con Email Triage

Son dos caras de la misma moneda epistémica:

| | Email Triage | Bayesian Compose |
|---|---|---|
| **Dirección** | Mensajes que recibes | Mensajes que envías |
| **Pregunta** | "¿Merece mi atención?" | "¿Merece la atención del receptor?" |
| **Criterios** | 30 (racionalidad bayesiana) | Los mismos 30, invertidos para emisión |
| **Perspectiva** | Desde ti (receptor) | Desde el otro (receptor estimado) |

Son herramientas independientes. No requieren que la otra esté instalada. Pero
si ambas están activas, forman un sistema bidireccional: filtras lo que recibes
con rigor epistémico y envías con el mismo rigor.

## Cómo funciona

### 1. Entrevista socrática (5+1 preguntas)

Antes de escribir nada, el skill te hace preguntas que mapean los criterios
epistémicos más importantes:

| # | Pregunta | Qué evalúa |
|---|----------|------------|
| 1 | **¿Qué quieres que el destinatario HAGA?** | Si hay acción concreta (GATE: si no la hay, el mensaje quizá no debería existir) |
| 2 | **¿Cuál es la decisión real que toca?** | Si estás hablando de la decisión o rodeándola |
| 3 | **¿Qué hechos verificables respaldan esto?** | Si hay anclas verificables (fechas, métricas, tickets) |
| 4 | **¿Hay algo que deberías incluir pero preferirías no hacerlo?** | Si estás filtrando evidencia (la pregunta más importante) |
| 5 | **¿Qué pasa si lo lee mañana en vez de ahora?** | Si la urgencia es real o fabricada |
| 6 | **¿Quién recibe esto y qué sabe ya?** | Distancia inferencial y calibración al receptor (opcional) |

La **pregunta 1 es un gate**: si no hay acción concreta, el skill te ofrece
repensar, continuar con score bajo esperado, o no enviar aún.

### 2. Borrador guiado

Con tus respuestas, Claude genera un borrador que:
- Abre con la acción/decisión (no con contexto)
- Ancla con hechos verificables
- Incluye la información incómoda si la hubo
- Calibra complejidad al receptor
- No usa jargon que cierre el pensamiento

El borrador es una **guía, no un texto final**. Lo reescribe bajo petición.

### 3. Diagnóstico de 30 criterios

Evalúa el borrador con los 30 criterios, siempre todos, agrupados en 4 ejes:

**Grupo A — Valor de información**
| # | Criterio | Peso |
|---|----------|------|
| 1 | Cambia algo concreto | ±5 |

**Grupo B — Actualización bayesiana**
| # | Criterio | Peso |
|---|----------|------|
| 2 | Cambio de predicciones | ±4 |
| 3 | Sorpresa bayesiana | ±3 |
| 4 | Evidencia filtrada | -3 |
| 5 | Forward/Backward flow | ±3 |

**Grupo C — Diseño atencional y utilidad**
| # | Criterio | Peso |
|---|----------|------|
| 6 | Retorno atencional | ±2 |
| 7 | Confusión productiva | +4 |
| 8 | Impacto causal real | +4 |
| 9 | Ruido social | -3 |
| 10 | Abre opciones | +3 |
| 11 | Distancia inferencial | -2 |
| 12 | Agente estratégico | -3 |
| 13 | Densidad informativa | ±2 |
| 14 | Urgencia real vs fabricada | ±3 |
| 15 | Relevancia longitudinal | +4 |

**Grupo D — Anti-sesgo y calidad argumental**
| # | Criterio | Peso |
|---|----------|------|
| 16 | Motivated stopping | -2 |
| 17 | Motivated continuation | -2 |
| 18 | True rejection | ±2 |
| 19 | Third alternative | +3 |
| 20 | Privileging the hypothesis | -3 |
| 21 | Proper humility | ±3 |
| 22 | Positive bias | -2 |
| 23 | Argument screens off authority | ±3 |
| 24 | Hug the query | ±4 |
| 25 | Semantic stopsigns | -3 |
| 26 | Fake justification | -3 |
| 27 | Fake optimization criteria | -2 |
| 28 | Entangled truths | ±3 |
| 29 | Cached thought | ±2 |
| 30 | Absence of expected evidence | -3 |

12 criterios son **core** (siempre se evalúan): #1, #2, #3, #4, #5, #8, #14,
#23, #24, #25, #28, #30. Los demás se evalúan siempre pero pueden puntuar
n/a si no aplican al tipo de mensaje.

### 4. Output en 3 niveles

**Nivel 1** — El mensaje + score + tier predicho
```
## Tu mensaje (Score: 18 · REPLY_NEEDED 🔴)

[Texto del borrador]
```

**Nivel 2** — Top 3 fortalezas y debilidades con sugerencias de mejora
```
## Fortalezas
+5  #1  Cambia algo concreto — pides revisión del diseño antes del jueves
+4  #24 Hug the query — directo a la decisión de aprobar o iterar

## Debilidades
-2  #11 Distancia inferencial — asumes conocimiento de schema v3
         → Añadir una línea de contexto
```

**Nivel 3** — Desglose completo de los 30 criterios (una línea cada uno)

### 5. Iteración por conversación

Después del diagnóstico, iteras hablando — sin reinvocar el skill:
- "Reescríbelo más directo"
- "Mejora el segundo párrafo"
- "¿Por qué puntúa -2 en distancia inferencial?"
- "¿Qué score tendría si quito esta frase?"
- "¿Y si se lo envío a otra persona?"

### Tiers de predicción

| Tier | Score | Significado |
|------|-------|-------------|
| REPLY_NEEDED 🔴 | ≥ 10 | Tu mensaje generaría respuesta activa |
| REVIEW 🟡 | 4–9 | Tu mensaje sería leído con atención |
| READING_LATER 🔵 | 0–3 | Tu mensaje se leería "cuando pueda" |
| ARCHIVE ⚪ | < 0 | Tu mensaje sería ignorado o archivado |

## Modos de entrada

| Modo | Cuándo | Qué hace |
|------|--------|----------|
| **Composición** | Quieres escribir un mensaje nuevo | Entrevista completa → borrador → diagnóstico |
| **Evaluación** | Ya tienes un borrador | Salta la entrevista de contenido, evalúa directamente |
| **Respuesta** | Quieres responder a un mensaje recibido | Entrevista adaptada al contexto del hilo |

## Instalación

### Desde Cowork (recomendado)

1. Abre **Personalizar** → **Plugins**
2. Haz clic en **Añadir marketplace**
3. Pega: `novanoticia/bayesian-compose-plugin`
4. Haz clic en **Sincronizar**
5. Activa el plugin **bayesian-compose** con el botón "+"

### Desde Claude Code (CLI)

1. Abre Claude Code
2. Ve a **Settings** → **Plugins** → **Add Marketplace**
3. Añade: `novanoticia/bayesian-compose-plugin`
4. Activa el plugin

### Desde Claude Chat (Skills)

1. Descarga el paquete [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/blob/main/bayesian-compose.zip).
2. En Claude Chat, ve a **Skills** → **Importar** y sube el `.zip`.
3. Activa el skill **bayesian-compose** en tu conversación.

### Desde Perplexity (Skills)

1. Descarga el paquete [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/blob/main/bayesian-compose.zip).
2. En Perplexity, ve a **Skills** → **Subir/Importar skill** y selecciona el `.zip`.

> **Nota técnica:** el límite de longitud del campo `description` depende de la plataforma: Perplexity valida **en bytes UTF-8** (límite 1024) y Mistral **en caracteres** (límite 500). La descripción de este skill mide **434 caracteres / 446 bytes**, dentro de ambos umbrales. Si la editas, no superes los **500 caracteres** para conservar la compatibilidad con Mistral.

### Desde Mistral AI (Skills)

1. Descarga el paquete [bayesian-compose.zip](https://github.com/novanoticia/bayesian-compose-plugin/blob/main/bayesian-compose.zip) y **descomprímelo**.
2. En Mistral AI, dentro del espacio **Work**, abre **Skills** y selecciona la **carpeta** resultante (`bayesian-compose/`, la que contiene `SKILL.md`).

### Verificar instalación

Tras instalar, inicia una nueva conversación y escribe:
```
/bayesian-compose
```

Claude debería iniciar la entrevista socrática.

## Configuración

Edita `skills/bayesian-compose/config.yaml` para personalizar:

### Perfil de usuario
```yaml
usuario:
  nombre: "Tu nombre"
  perfil: "Tu rol, formación e intereses"
  idioma: "es"
```

### Tipo de mensaje
```yaml
mensaje:
  tipo_default: "email"      # email, slack, whatsapp, carta, general
  tono_default: "profesional" # profesional, informal, formal, directo, empático
  incluir_saludo: true
  incluir_despedida: true
```

### Entrevista
```yaml
entrevista:
  pregunta_6_auto: true   # Claude decide si hacer la pregunta 6
  gate_estricto: true      # Pregunta 1 bloquea si no hay acción concreta
```

### Output
```yaml
output:
  mostrar_nivel_1: true    # Mensaje + score
  mostrar_nivel_2: true    # Fortalezas y debilidades
  mostrar_nivel_3: true    # Desglose completo de 30 criterios
  razones_positivas: 3
  razones_negativas: 3
```

### Tiers (umbrales)
```yaml
tiers:
  reply_needed: 10
  review: 4
  reading_later: 0
  archive: -1
```

### Criterios epistémicos
Cada criterio se puede desactivar o ajustar individualmente:
```yaml
criterios_epistemicos:
  cambia_algo_concreto:
    activo: true
    core: true
    weight: 5
    question: "¿Mi mensaje contiene una acción o cambio concreto?"
```

### Telemetría (opcional)
Para registrar sesiones y detectar patrones en tu escritura:
```bash
mkdir -p ~/.bayesian-compose
```
El skill solo escribe si el directorio existe. No lo crea automáticamente.

## Ejemplo de uso

**Invocación:**
```
/bayesian-compose
```

**Pregunta 1 (gate):**
> ¿Qué quieres que el destinatario HAGA después de leer tu mensaje?

**Tu respuesta:**
> Que revise el diseño del dashboard antes del jueves y me diga si aprueba
> o quiere iterar.

**Pregunta 2:**
> ¿Cuál es la decisión real que este mensaje toca?

**Tu respuesta:**
> Si lanzamos el dashboard con el diseño actual o hacemos una ronda más.

*(...preguntas 3-5...)*

**Output:**
```
## Tu mensaje (Score: 22 · REPLY_NEEDED 🔴)

María,

El dashboard para el lanzamiento del viernes tiene el diseño cerrado
desde ayer. Necesito tu aprobación antes del jueves a las 14:00 para
que el equipo de front pueda integrarlo.

Los datos: el test de usabilidad con 12 usuarios dio un SUS de 78
(por encima del umbral de 68). El único punto débil fue la navegación
del filtro de fechas — lo documenté en DESIGN-847.

Opciones: (a) apruebas tal cual, (b) iteramos el filtro de fechas
y movemos el lanzamiento al lunes, (c) lanzamos sin el filtro y lo
mejoramos en v1.1.

¿15 min mañana para decidir?

## Fortalezas
+5  #1  Cambia algo concreto — aprobación o iteración con deadline
+4  #24 Hug the query — directo a la decisión lanzar/iterar
+3  #28 Entangled truths — SUS 78, 12 usuarios, ticket DESIGN-847, fecha

## Debilidades
 0  #7  Confusión productiva — no hay gap sorprendente aquí
 0  #15 Relevancia longitudinal — decisión táctica, no estratégica
+1  #29 Cached thought — el cierre "¿15 min?" es semi-enlatado
         → Proponer slot concreto: "¿mañana 10:30 o 16:00?"
```

## Troubleshooting

### El skill no aparece tras instalar
Cierra y reabre Claude Code/Cowork. Los skills se cargan al inicio de sesión.

### "No se encontró marketplace.json"
Asegúrate de añadir `novanoticia/bayesian-compose-plugin` (sin `https://github.com/`).

### El gate de la pregunta 1 es demasiado estricto
Cambia `entrevista.gate_estricto: false` en `config.yaml`. Claude advertirá
pero no bloqueará.

### Quiero ver solo el score, no el desglose completo
Cambia `output.mostrar_nivel_3: false` en `config.yaml`.

### Los scores parecen bajos para mensajes que creo buenos
Los scores son desde la perspectiva del **receptor**, no la tuya. Un mensaje
que a ti te parece valioso puede no serlo tanto para el receptor si ya
conoce la información, si no tiene acción concreta, o si la urgencia es
más tuya que suya.

## Scores de referencia

| Rango | Interpretación |
|-------|----------------|
| 25-55 | Excepcional — mensaje de alto impacto epistémico |
| 15-24 | Bueno — mensaje claro, accionable, bien fundamentado |
| 5-14 | Aceptable — cumple pero tiene margen de mejora |
| 0-4 | Bajo — el receptor probablemente lo postergaría |
| < 0 | El mensaje probablemente no debería enviarse así |

Score máximo teórico: +55. Score mínimo teórico: -62.

## Créditos

Diseñado por Pablo Rodríguez López ([mindandhealth.org](https://mindandhealth.org/))
con asistencia de Claude y **Vibe Code** (coautor en implementaciones de compatibilidad).

Criterios epistémicos basados en las [Sequences](https://www.lesswrong.com/rationality)
de Eliezer Yudkowsky (LessWrong).

## Licencia

Apache 2.0 — ver [LICENSE](./LICENSE).

## Enlaces

- [Repositorio en GitHub](https://github.com/novanoticia/bayesian-compose-plugin)
- [Issues](https://github.com/novanoticia/bayesian-compose-plugin/issues)
- [Plugin complementario: Email Triage](https://github.com/novanoticia/email-triage-plugin)
