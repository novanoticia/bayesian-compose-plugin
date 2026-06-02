# Los 30 criterios invertidos para emisión (catálogo completo)

> Referencia de `bayesian-compose` · PASO 4 (Diagnóstico epistémico).
> Cargar este archivo antes de puntuar un borrador.

### Los 30 criterios invertidos para emisión

---

#### GRUPO A — CRITERIO BASE (Valor de información)

##### #1 — Cambia algo concreto
- **Peso**: 5
- **Core**: SÍ (siempre se evalúa)
- **Pregunta de emisión**: "¿Mi mensaje contiene una acción o cambio concreto
  para el destinatario?"
- **Escala**:
  - Acción/cambio explícito y claro: **+5**
  - Acción implícita pero deducible: **+2**
  - Puramente informativo sin acción: **-5**
- **Qué buscar**: ¿Hay un verbo imperativo o una petición clara? ¿El
  destinatario sabe qué hacer después de leer? Si el mensaje termina y el
  receptor piensa "¿y qué hago con esto?", puntúa bajo.

---

#### GRUPO B — ACTUALIZACIÓN BAYESIANA

##### #2 — Cambio de predicciones
- **Peso**: 4
- **Core**: SÍ
- **Pregunta de emisión**: "¿Mi mensaje contiene información que actualizaría
  el modelo de realidad del destinatario?"
- **Escala**:
  - Información genuinamente nueva para el receptor: **+4**
  - Parcialmente nuevo: **+1**
  - Todo ya conocido por el receptor: **-3**
- **Qué buscar**: ¿El receptor ya sabe esto? Si podrías haber no enviado
  el mensaje y el receptor tendría exactamente las mismas creencias y
  planes... el cambio de predicciones es cero.

##### #3 — Sorpresa bayesiana
- **Peso**: 3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Le estoy diciendo al destinatario algo que
  probablemente NO esperaba?"
- **Escala**:
  - Alta (información inesperada): **+3**
  - Media (parcialmente esperado): **+1**
  - Baja (completamente predecible): **-2**
- **Qué buscar**: si el receptor pudiera haber predicho el contenido de tu
  mensaje antes de abrirlo, su valor informativo es cero. No se trata de ser
  dramático — se trata de que la información sea genuinamente no-obvia.

##### #4 — Evidencia filtrada
- **Peso**: -3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Estoy incluyendo TODA la evidencia relevante,
  o solo la que favorece mi posición?"
- **Escala**:
  - Equilibrado (incluye evidencia a favor y en contra): **0**
  - Selectivamente persuasivo (omite lo incómodo): **-2**
  - Unilateral (solo lo que me favorece): **-3**
- **Qué buscar**: contrastar con la respuesta a la pregunta 4 de la
  entrevista. Si el usuario admitió que había algo incómodo y no aparece
  en el borrador, es evidencia filtrada. También buscar: ¿se presentan solo
  los datos positivos? ¿Se omiten riesgos conocidos? ¿Se citan solo las
  opiniones favorables?

##### #5 — Forward/Backward Flow
- **Peso**: 3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Estoy explorando hacia adelante o buscando
  confirmación para algo que ya decidí?"
- **Escala**:
  - Forward (exploración genuina, busca información): **+3**
  - Mixto: **0**
  - Backward (busca validación de decisión tomada): **-2**
- **Qué buscar**: si el mensaje dice "creo que deberíamos hacer X, ¿qué
  opinas?" pero el tono o contexto sugiere que X ya está en marcha... es
  backward disfrazado de forward. El test: si el receptor dijera "no, mejor
  Y", ¿cambiarías realmente de rumbo?

---

#### GRUPO C — DISEÑO ATENCIONAL Y UTILIDAD

##### #6 — Retorno atencional
- **Peso**: 2
- **Core**: NO
- **Pregunta de emisión**: "¿El tiempo que el destinatario invierte en leer
  esto está bien empleado?"
- **Escala**:
  - Alto (cada segundo de lectura aporta valor): **+2**
  - Medio: **0**
  - Bajo (el receptor perderá tiempo): **-2**
- **Qué buscar**: ratio información/longitud. Un mensaje de 3 párrafos que
  podría ser una frase tiene retorno atencional bajo. También: ¿hay
  repeticiones? ¿Contexto innecesario que el receptor ya conoce?

##### #7 — Confusión productiva
- **Peso**: 4
- **Core**: NO
- **Pregunta de emisión**: "¿Mi mensaje hace visible una tensión productiva
  que vale la pena examinar?"
- **Escala**:
  - Sí (revela un gap real entre lo esperado y lo actual): **+4**
  - No (no hay tensión productiva): **0**
- **Qué buscar**: discrepancias entre planes y realidad, entre lo que un
  equipo cree y lo que los datos muestran, entre lo prometido y lo entregado.
  No se trata de confundir — se trata de hacer visible algo que nadie
  estaba viendo. Ej: "El roadmap dice Q3 pero el equipo planifica para Q4
  — ¿cuál es la versión correcta?"

##### #8 — Impacto causal real
- **Peso**: 4
- **Core**: SÍ
- **Pregunta de emisión**: "Si el destinatario actúa sobre mi mensaje,
  ¿cuánto cambia realmente el resultado?"
- **Escala**:
  - Alto (la acción cambia significativamente el outcome): **+4**
  - Medio (cambia algo pero marginal): **+2**
  - Bajo (da igual si actúa o no): **0**
- **Qué buscar**: la diferencia entre "estaría bien que revisaras esto"
  (bajo impacto — si no lo revisa, pasa igualmente) y "si no revisas esto
  antes del deploy, el bug en producción afecta a 12k usuarios" (alto
  impacto — la acción cambia un resultado real).

##### #9 — Ruido social
- **Peso**: -3
- **Core**: NO
- **Pregunta de emisión**: "¿Escribo porque tengo contenido real o porque
  me siento socialmente obligado a responder?"
- **Escala**:
  - Contenido real (escribo porque hay información/acción que transmitir): **0**
  - Mixto (algo de contenido + algo de obligación): **-1**
  - Ritual (escribo para que conste, para quedar bien, por cortesía vacía): **-3**
- **Qué buscar**: el "gracias por tu email, quedo a tu disposición" puro.
  El reply-all que no añade nada. El CC preventivo. El "solo quería
  confirmar que recibí tu mensaje" cuando no se pidió confirmación. Si tu
  motivación para escribir es "que conste" o "quedar bien", es ruido social.

##### #10 — Abre opciones
- **Peso**: 3
- **Core**: NO
- **Pregunta de emisión**: "¿Mi mensaje le da al destinatario una
  posibilidad nueva que no tenía?"
- **Escala**:
  - Sí (abre una puerta nueva): **+3**
  - No: **0**
- **Qué buscar**: no es "te doy más trabajo" — es "te doy una puerta que
  no sabías que existía". Ej: "No sé si sabes que el equipo de infra tiene
  un endpoint que resuelve exactamente esto." Compartir un recurso, un
  contacto, una herramienta o una posibilidad que el receptor no tenía.

##### #11 — Distancia inferencial
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿He calibrado la complejidad al nivel de
  conocimiento del destinatario?"
- **Escala**:
  - Baja (bien calibrado al receptor): **0**
  - Media (requiere algo de esfuerzo extra): **-1**
  - Alta (requiere conocimiento que el receptor no tiene): **-2**
- **Qué buscar**: si le hablas a un diseñador en jerga de Kubernetes sin
  contexto, la distancia inferencial es máxima. Si usas acrónimos internos
  con alguien externo, igual. No es que seas inteligente — es que estás
  imponiendo trabajo cognitivo innecesario. Usar la respuesta a la pregunta
  6 (si se hizo) para calibrar.

##### #12 — Agente estratégico
- **Peso**: -3
- **Core**: NO
- **Pregunta de emisión**: "¿Escribo para informar o para manipular? ¿Mi
  intención es transparente?"
- **Escala**:
  - Verdad (intención transparente): **0**
  - Quizá (parcialmente estratégico): **-1**
  - Influencia (optimizo para que el receptor llegue a MI conclusión): **-3**
- **Qué buscar**: la autodetección más incómoda. Si estás eligiendo qué
  decir y cómo decirlo para que el receptor llegue a TU conclusión en vez
  de a la MEJOR conclusión... eres un agente estratégico. El test: si
  alguien leyera tu email y tus notas internas sobre por qué lo escribiste,
  ¿se sentiría manipulado?

##### #13 — Densidad informativa
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Cada frase de mi mensaje aporta información
  nueva, o estoy rellenando?"
- **Escala**:
  - Alta (cada frase es nueva información): **+1**
  - Media (algunas frases son relleno): **0**
  - Baja (mucho padding, saludos extensos, repetición): **-2**
- **Qué buscar**: saludos extensos, repetición de contexto que el receptor
  ya tiene, disclaimers innecesarios, "como comentamos en la reunión del
  lunes pasado" cuando ambos estuvieron ahí. Cada frase que no aporta
  información nueva reduce la densidad.

##### #14 — Urgencia real vs fabricada
- **Peso**: 3
- **Core**: SÍ
- **Pregunta de emisión**: "Si transmito urgencia, ¿está respaldada por
  consecuencias reales y verificables?"
- **Escala**:
  - Real (urgencia con consecuencia verificable): **+3**
  - Neutral (no se transmite urgencia): **0**
  - Fabricada (urgencia sin consecuencia concreta): **-3**
- **Qué buscar**: "URGENTE" en el asunto sin consecuencia concreta =
  fabricada. "El certificado SSL expira el viernes a las 18:00 y no hay
  rollback" = real. Contrastar con la respuesta a la pregunta 5 de la
  entrevista: si el usuario dijo que "no pasa nada si lo lee mañana" pero
  el borrador usa lenguaje de urgencia, hay discrepancia.

##### #15 — Relevancia longitudinal
- **Peso**: 4
- **Core**: NO
- **Pregunta de emisión**: "¿El destinatario valorará este mensaje dentro
  de un mes, o es completamente efímero?"
- **Escala**:
  - Sí (referenciable en el futuro): **+4**
  - Quizá: **+1**
  - No (efímero, valor instantáneo): **0**
- **Qué buscar**: no todo mensaje necesita ser trascendente. Pero si el
  contenido incluye una decisión arquitectónica, un acuerdo, datos de
  referencia o un análisis reutilizable, tiene relevancia longitudinal.
  Un "ok, entendido" no la tiene.

---

#### GRUPO D — ANTI-SESGO Y CALIDAD ARGUMENTAL

##### #16 — Motivated stopping
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Estoy empujando al destinatario a cerrar una
  decisión antes de que debería?"
- **Escala**:
  - Sí (presiono por cierre prematuro): **-2**
  - No: **0**
- **Qué buscar**: "Creo que con esto ya podemos cerrar el tema" cuando hay
  cabos sueltos sin resolver. Presionar por cierre para tu conveniencia,
  no porque el análisis esté completo. El test: ¿hay preguntas legítimas
  sin responder que tu mensaje ignora o descarta?

##### #17 — Motivated continuation
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Estoy manteniendo abierto algo que debería
  cerrarse?"
- **Escala**:
  - Sí (prolongo artificialmente): **-2**
  - No: **0**
- **Qué buscar**: pedir "una ronda más de feedback" cuando ya hay consenso,
  porque el resultado no te gusta. Abrir nuevas dudas cuando la decisión ya
  se tomó con suficiente información. El reverso de motivated stopping:
  mantener abierto lo que debería cerrarse.

##### #18 — True rejection
- **Peso**: 2
- **Core**: NO
- **Pregunta de emisión**: "Si planteo objeciones, ¿son sustantivas o son
  estéticas/políticas?"
- **Escala**:
  - Real (objeción sustantiva con fundamento): **+2**
  - Mixta: **0**
  - Superficial (excusa elegante): **-2**
- **Qué buscar**: "No me convence el approach" sin decir por qué
  concretamente = false rejection. "El approach asume que la API responde en
  <200ms pero nuestro p95 es 800ms" = true rejection. Si planteas una
  objeción, ¿podrías defenderla con datos si te lo pidieran?
- **n/a**: si el mensaje no contiene objeciones.

##### #19 — Third alternative
- **Peso**: 3
- **Core**: NO
- **Pregunta de emisión**: "¿He considerado y presentado opciones más allá
  del binario obvio?"
- **Escala**:
  - Sí (presenta una tercera opción real): **+3**
  - No (solo A o B): **0**
- **Qué buscar**: si tu mensaje dice "deberíamos hacer A o B", pregúntate
  si hay un C que no estás viendo. No siempre lo hay — pero el ejercicio de
  buscarlo es el valor. También: ¿estás presentando un falso dilema?
- **n/a**: si el mensaje no presenta opciones o decisiones.

##### #20 — Privileging the hypothesis
- **Peso**: -3
- **Core**: NO
- **Pregunta de emisión**: "¿Presento mi opción preferida como si fuera la
  obvia sin suficiente evidencia?"
- **Escala**:
  - Sí (presenta preferencia como hecho): **-3**
  - No: **0**
- **Qué buscar**: "Claramente la mejor opción es migrar a Postgres" — ¿es
  "claro" según qué datos? Si no puedes respaldarlo con evidencia concreta,
  estás privilegiando tu hipótesis. Palabras señal: "claramente",
  "obviamente", "sin duda", "la única opción real es".

##### #21 — Proper humility
- **Peso**: 3
- **Core**: NO
- **Pregunta de emisión**: "Cuando expreso incertidumbre, ¿ofrezco formas
  concretas de verificar o mitigar?"
- **Escala**:
  - Humildad operativa (duda + plan de verificación): **+3**
  - Neutral: **0**
  - Duda vaga (incertidumbre sin acción): **-2**
- **Qué buscar**: "No estoy seguro de que funcione" = duda vaga (no aporta
  nada). "No estoy seguro de que funcione — propongo un spike de 2 días
  antes de commitear al approach, midiendo X e Y" = humildad operativa (útil
  y accionable).
- **n/a**: si el mensaje no expresa incertidumbre.

##### #22 — Positive bias
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Solo presento evidencia que apoya mi posición,
  ignorando la contraria?"
- **Escala**:
  - Sí (solo evidencia favorable): **-2**
  - No (incluye evidencia contraria): **0**
- **Qué buscar**: gemelo del criterio #4 (evidencia filtrada) pero enfocado
  en los ejemplos concretos. Si das 3 casos de éxito y omites los 2 fracasos
  que conoces... positive bias. La diferencia con #4: evidencia filtrada es
  sobre la selección general de información; positive bias es sobre los
  ejemplos y datos específicos que citas.

##### #23 — Argument screens off authority
- **Peso**: 3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Sustento mi posición con argumentos y
  evidencia, o con mi puesto/experiencia?"
- **Escala**:
  - Argumento fuerte (evidencia verificable): **+3**
  - Mixto (argumento + autoridad): **0**
  - Solo autoridad (posición, antigüedad, título): **-2**
- **Qué buscar**: "Como lead del equipo, creo que deberíamos hacer X" — el
  argumento es tu título. "Los últimos 3 deploys con este pattern causaron
  rollback (links), propongo X" — el argumento es evidencia. El título
  sobra cuando la evidencia habla.

##### #24 — Hug the query
- **Peso**: 4
- **Core**: SÍ
- **Pregunta de emisión**: "¿Cada parte de mi mensaje es directamente
  relevante a la pregunta/decisión central?"
- **Escala**:
  - Directo (todo el mensaje va al punto): **+4**
  - Adyacente (algo de contexto tangencial): **+1**
  - Tangencial (se pierde en contexto antes de llegar al punto): **-2**
- **Qué buscar**: si tu mensaje empieza con 2 párrafos de contexto antes de
  llegar al punto, esos 2 párrafos son tangenciales. Regla: pon el punto
  primero, contexto después (si hace falta). El receptor debería entender la
  acción/decisión en las primeras 3 líneas.

##### #25 — Semantic stopsigns
- **Peso**: -3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Uso buzzwords, jerga o etiquetas que cierran
  el pensamiento en vez de abrirlo?"
- **Escala**:
  - Sí (usa stopsigns): **-3**
  - No: **0**
- **Qué buscar**: "Necesitamos sinergia entre equipos", "hay que alinear
  stakeholders", "es una cuestión de mindset", "tenemos que ser más ágiles".
  Suenan a algo pero no dicen nada concreto. Cierran la conversación sin
  resolver nada. El test: si reemplazas la frase por "necesitamos hacer
  [cosa concreta]", ¿cambia el significado? Si no puedes hacer ese reemplazo,
  es un stopsign.

##### #26 — Fake justification
- **Peso**: -3
- **Core**: NO
- **Pregunta de emisión**: "¿Decidí primero y luego construí el
  razonamiento para justificarlo?"
- **Escala**:
  - Sí (conclusión precede al razonamiento): **-3**
  - No: **0**
- **Qué buscar**: si escribiste la conclusión del email antes que el cuerpo,
  probablemente es fake justification. El orden natural es: evidencia →
  análisis → conclusión. Si invertiste ese orden mentalmente, el mensaje
  lo refleja. También: si cambias una premisa, ¿cambiaría tu conclusión?
  Si no, el razonamiento es decorativo.

##### #27 — Fake optimization criteria
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Elijo los criterios de evaluación para que mi
  opción preferida gane?"
- **Escala**:
  - Sí (criterios oportunistas): **-2**
  - No: **0**
- **Qué buscar**: "Evaluando por coste, la opción A es mejor" — ¿por qué
  elegiste coste como criterio y no velocidad de entrega, donde A pierde?
  Si cambiaste el criterio de evaluación para que gane tu favorita, es fake
  optimization. El test: ¿elegirías los mismos criterios si no tuvieras
  preferencia?
- **n/a**: si el mensaje no compara opciones con criterios.

##### #28 — Entangled truths
- **Peso**: 3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Mi mensaje está anclado a hechos específicos
  y verificables — fechas, números, tickets, nombres, métricas?"
- **Escala**:
  - Alto (múltiples anclas verificables): **+3**
  - Medio (alguna): **+1**
  - Flotante (ningún hecho verificable): **-2**
- **Qué buscar**: la diferencia entre "el rendimiento bajó últimamente" y
  "el p95 de latencia subió de 200ms a 450ms entre el 3 y el 10 de abril
  (dashboard link)". Misma información, diferente verificabilidad. Contar:
  ¿cuántas afirmaciones del mensaje podrían verificarse independientemente?

##### #29 — Cached thought
- **Peso**: -2
- **Core**: NO
- **Pregunta de emisión**: "¿Estoy escribiendo pensamiento original o
  reciclando una respuesta estándar?"
- **Escala**:
  - Original (pensado específicamente para esta situación): **+1**
  - Mixto: **0**
  - Enlatado (plantilla/template reutilizada): **-2**
- **Qué buscar**: si podrías haber enviado exactamente el mismo texto a 5
  personas diferentes sin cambiar nada... es cached thought. No hay
  pensamiento específico para este receptor y esta situación. También aplica
  a frases hechas: "quedo a tu disposición", "no dudes en contactarme",
  "espero tu respuesta" — relleno enlatado.

##### #30 — Absence of expected evidence
- **Peso**: -3
- **Core**: SÍ
- **Pregunta de emisión**: "¿Hay información que el destinatario esperaría
  encontrar en un mensaje de esta importancia y que NO estoy incluyendo?"
- **Escala**:
  - Sí (falta algo esperable): **-3**
  - No (todo lo esperable está presente): **0**
- **Qué buscar**: si dices "esto es crítico para el lanzamiento" pero no
  incluyes ni fecha de lanzamiento, ni scope afectado, ni quién es
  responsable... la ausencia de esa evidencia contradice la importancia que
  declaras. El test: si un tercero leyera tu mensaje, ¿preguntaría "¿y
  dónde está [X]?" donde X es algo que debería estar.

---

