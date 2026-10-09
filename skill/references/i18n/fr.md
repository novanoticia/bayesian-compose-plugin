# Equivalencias de textos fijos — francés

Este archivo es solo una traducción de los textos fijos. Ante cualquier
discrepancia, manda `SKILL.md`, cuya versión española es la referencia
canónica. No añade reglas ni modifica los criterios o la puntuación.

## Configuración personal — PASO 0

| Español | Français |
| --- | --- |
| He encontrado solo la plantilla. ¿Quieres que cree tu configuración personal editable en `~/.bayesian-compose/config.yaml` para que sobreviva a las actualizaciones? | Je n’ai trouvé que le modèle. Veux-tu que je crée ta configuration personnelle modifiable dans `~/.bayesian-compose/config.yaml` pour qu’elle soit conservée lors des mises à jour ? |

## Preguntas de la entrevista — PASO 2

| Pregunta | Español | Français |
| --- | --- | --- |
| #1 | ¿Qué quieres que el destinatario HAGA después de leer tu mensaje? | Que veux-tu que le destinataire FASSE après avoir lu ton message ? |
| #2 | ¿Cuál es la decisión real que este mensaje toca? | Quelle est la décision réelle que ce message concerne ? |
| #3 | ¿Qué hechos verificables respaldan lo que vas a decir? | Quels faits vérifiables étayent ce que tu vas dire ? |
| #4 | ¿Hay algo que deberías incluir pero preferirías no hacerlo? | Y a-t-il quelque chose que tu devrais inclure mais que tu préférerais omettre ? |
| #5 | ¿Qué pasa concretamente si el destinatario lo lee mañana en vez de ahora? | Que se passe-t-il concrètement si le destinataire le lit demain plutôt que maintenant ? |
| #6 | ¿Quién recibe esto y qué sabe ya sobre el tema? | Qui reçoit ce message et que sait déjà cette personne sur le sujet ? |

## Aclaraciones y reformulaciones — PASO 2

| Español | Français |
| --- | --- |
| (No el tema general — la decisión concreta que alguien tiene que tomar) | (Pas le sujet général — la décision concrète que quelqu’un doit prendre) |
| (Fechas, métricas, tickets, nombres, enlaces, datos concretos) | (Dates, indicateurs, tickets, noms, liens, données concrètes) |
| (Un dato incómodo, un riesgo que conoces, una objeción legítima que estás evitando mencionar) | (Un fait gênant, un risque que tu connais, une objection légitime que tu évites de mentionner) |
| (Rol, relación contigo, nivel de contexto previo) | (Rôle, relation avec toi, niveau de contexte préalable) |
| "Dices que el tema es X. Pero ¿cuál es la decisión que depende de este mensaje? ¿Qué se elige, se aprueba, se rechaza o se cambia?" | "Tu dis que le sujet est X. Mais quelle décision dépend de ce message ? Que choisit-on, approuve-t-on, rejette-t-on ou change-t-on ?" |
| "Tu mensaje se sostiene solo con tu opinión o autoridad. Eso no lo invalida, pero el receptor podría percibirlo como menos confiable. ¿Hay algún dato que puedas incluir para anclar tu argumento?" | "Ton message repose uniquement sur ton opinion ou ton autorité. Cela ne l’invalide pas, mais le destinataire pourrait le percevoir comme moins fiable. Y a-t-il une donnée que tu pourrais inclure pour étayer ton argument ?" |

## Mensaje del gate — PASO 2

| Español | Français |
| --- | --- |
| Tu mensaje no tiene una acción concreta para el destinatario. Eso no significa que no debas enviarlo, pero sí que probablemente caería en los tiers READING_LATER o ARCHIVE si el receptor usara un filtro epistémico.<br><br>¿Quieres:<br>a) Repensar qué cambiaría concretamente para el receptor<br>b) Continuar sabiendo que será un mensaje informativo (score esperado bajo)<br>c) No enviarlo aún y resolver primero lo que necesitas resolver | Ton message ne propose aucune action concrète au destinataire. Cela ne signifie pas que tu ne dois pas l’envoyer, mais qu’il relèverait probablement des tiers READING_LATER ou ARCHIVE si le destinataire utilisait un filtre épistémique.<br><br>Veux-tu :<br>a) Repenser ce qui changerait concrètement pour le destinataire<br>b) Continuer en sachant qu’il s’agira d’un message informatif (Score attendu faible)<br>c) Ne pas l’envoyer pour l’instant et résoudre d’abord ce que tu dois résoudre |

## Encabezados y etiquetas del output — PASO 5

| Español | Français |
| --- | --- |
| Tu mensaje | Ton message |
| Score | Score |
| TIER | TIER |
| [Texto del borrador] | [Texte du brouillon] |
| Fortalezas | Points forts |
| Debilidades | Points faibles |
| Desglose completo | Détail complet |
| TOTAL | TOTAL |
| n/a | n/a |
| Forward/Backward flow | Forward/Backward flow |
| Argument screens off auth. | Argument screens off auth. |
| pides [acción específica del mensaje] | tu demandes [action précise du message] |
| directo a [decisión específica] sin rodeos | tu vas directement à [décision précise] sans détour |
| [hechos verificables presentes en el mensaje] | [faits vérifiables présents dans le message] |
| [problema específico] | [problème précis] |
| [sugerencia concreta] | [suggestion concrète] |
| [frase específica que es template] | [phrase précise qui est une formule toute faite] |
| [alternativa específica] | [autre possibilité précise] |
| [oportunidad perdida] | [occasion manquée] |
| [alternativa específica que podría mencionarse] | [autre possibilité précise qui pourrait être mentionnée] |
| tu mensaje generaría respuesta | ton message susciterait une réponse |
| tu mensaje sería leído con atención | ton message serait lu avec attention |
| tu mensaje se leería "cuando pueda" | ton message serait lu « quand je pourrai » |
| tu mensaje sería archivado o ignorado | ton message serait archivé ou ignoré |

## Significado de tiers — Apéndice A

| Tier | Score | Significado en emisión | Signification à l'envoi |
| --- | --- | --- | --- |
| REPLY_NEEDED 🔴 | ≥ 10 | Tu mensaje generaría respuesta activa | Ton message susciterait une réponse active |
| REVIEW 🟡 | 4–9 | Tu mensaje sería leído con atención | Ton message serait lu avec attention |
| READING_LATER 🔵 | 0–3 | Tu mensaje se leería "cuando pueda" | Ton message serait lu « quand je pourrai » |
| ARCHIVE ⚪ | < 0 | Tu mensaje sería ignorado o archivado | Ton message serait ignoré ou archivé |

## Nombres de los 30 criterios

| Criterio | Español | Français |
| --- | --- | --- |
| #1 | Cambia algo concreto | Change quelque chose de concret |
| #2 | Cambio de predicciones | Changement des prédictions |
| #3 | Sorpresa bayesiana | Surprise bayésienne |
| #4 | Evidencia filtrada | Preuves filtrées |
| #5 | Forward/Backward Flow | Forward/Backward Flow |
| #6 | Retorno atencional | Retour sur l’attention |
| #7 | Confusión productiva | Confusion productive |
| #8 | Impacto causal real | Impact causal réel |
| #9 | Ruido social | Bruit social |
| #10 | Abre opciones | Ouvre des possibilités |
| #11 | Distancia inferencial | Distance inférentielle |
| #12 | Agente estratégico | Agent stratégique |
| #13 | Densidad informativa | Densité informationnelle |
| #14 | Urgencia real vs fabricada | Urgence réelle ou fabriquée |
| #15 | Relevancia longitudinal | Pertinence à long terme |
| #16 | Motivated stopping | Motivated stopping |
| #17 | Motivated continuation | Motivated continuation |
| #18 | True rejection | True rejection |
| #19 | Third alternative | Third alternative |
| #20 | Privileging the hypothesis | Privileging the hypothesis |
| #21 | Proper humility | Proper humility |
| #22 | Positive bias | Positive bias |
| #23 | Argument screens off authority | Argument screens off authority |
| #24 | Hug the query | Hug the query |
| #25 | Semantic stopsigns | Semantic stopsigns |
| #26 | Fake justification | Fake justification |
| #27 | Fake optimization criteria | Fake optimization criteria |
| #28 | Entangled truths | Entangled truths |
| #29 | Cached thought | Cached thought |
| #30 | Absence of expected evidence | Absence of expected evidence |
