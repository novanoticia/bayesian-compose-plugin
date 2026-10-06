# AGENTS.md

## Proyecto
`bayesian-compose`: compositor epistémico de mensajes con 30 criterios de racionalidad bayesiana. Se distribuye como plugin de Claude Code/Cowork (marketplace de este repo, publicado en el directorio de plugins de Claude) y como skill en .zip para Claude Chat, Perplexity y Mistral (GitHub Releases).
Solo hay Markdown, JSON y YAML. No hay código ejecutable, dependencias, build, tests ni CI, y no debe haberlos.

## Comandos de verificación
- Marketplace: `claude plugin validate .` → debe pasar (1 aviso conocido: falta `description` en marketplace).
- Plugin: `claude plugin validate plugins/bayesian-compose` → debe pasar sin avisos.
- JSON: `for f in $(git ls-files '*.json'); do jq empty "$f" || echo "FALLA $f"; done` → sin "FALLA".
- YAML: `ruby -ryaml -e 'ARGV.each{|f| YAML.load_file(f)}' $(git ls-files '*.yaml')` (o `python3 -c "import yaml,sys;[yaml.safe_load(open(f)) for f in sys.argv[1:]]" ...`) → sin error.
- Comando sincronizado: `diff commands/bayes.md plugins/bayesian-compose/commands/bayes.md` → sin salida.
- Copias sincronizadas: `diff -r skill plugins/bayesian-compose/skills/bayesian-compose` → la única salida permitida es `Only in skill: .skill.json`.
- Longitud de `description` del skill (≤ 500 caracteres y ≤ 1024 bytes):
  `python3 -c "import re;s=open('skill/SKILL.md',encoding='utf-8').read();d=re.search(r'description: >-\n((?:  .*\n)+)',s).group(1);d=' '.join(l.strip() for l in d.splitlines());print(len(d),len(d.encode()))"`
Si `claude`, `ruby` o PyYAML no están disponibles en tu entorno, dilo explícitamente en la entrega; no simules la salida.

## Estructura
- `.claude-plugin/marketplace.json`: catálogo; la entrada del plugin apunta a `./plugins/bayesian-compose`.
- `.claude-plugin/plugin.json`, `.claude-plugin/icon.png`: manifiesto raíz (incluye `privacyPolicyUrl`) e icono.
- `plugins/bayesian-compose/`: plugin instalable: `.claude-plugin/plugin.json`, `plugin.json` (Agent Plugins 1.0.0), `.mcp.json` (vacío a propósito), `skills/bayesian-compose/` (SKILL.md, config.yaml, references/).
- `skill/`: copia del skill que se empaqueta en el .zip (añade `.skill.json`). Debe ser idéntica a `plugins/bayesian-compose/skills/bayesian-compose/`.
- `commands/bayes.md`: comando `/bayes`.
- `plugins/bayesian-compose/commands/bayes.md`: comando `/bayes` que se instala con el plugin; copia idéntica de `commands/bayes.md`.
- `README.md`, `CHANGELOG.md`, `PRIVACY.md`, `LICENSE`.

## Convenciones
- Idioma del repositorio: español (los manifiestos JSON están en inglés). Commits en español, una línea descriptiva.
- `CHANGELOG.md`: Keep a Changelog en español + SemVer. Los cambios nuevos van bajo `## [Unreleased]`.
- Markdown: respetar el estilo existente (títulos `## PASO N — ...`, líneas de ~78 caracteres en SKILL.md, listas y tablas como las actuales).

## Internacionalización
- Mecanismo: sección «Idioma de la conversación» de `SKILL.md` y
  `usuario.idioma: "auto"` en `config.yaml`. Un código distinto de `"auto"`
  fija el idioma; con `"auto"` o sin configuración se usa el del primer
  mensaje del usuario, cambiándolo si lo pide. Si no se determina, español.
- Todo lo visible usa el idioma de interacción. El borrador usa el idioma
  indicado para el destinatario o, si no se indica, el de interacción.
- Ubicación de las traducciones: `references/i18n/<código>.md` en `skill/`
  y en `plugins/bayesian-compose/skills/bayesian-compose/`.
- Español: referencia canónica y fallback. Idiomas con tabla: `es`
  (canónico, en `SKILL.md`) y `en` (`references/i18n/en.md`). Si no existe
  tabla para otro idioma, se traduce fielmente sobre la marcha.
- Para añadir un idioma: crear `<código>.md` con la misma estructura que
  `en.md`, en ambas copias.
- Para añadir un texto nuevo: añadirlo en `SKILL.md` en español y su
  traducción en cada `<código>.md`, sincronizando ambas copias.

## No tocar sin aprobación explícita
- El `name` del plugin y del skill (`bayesian-compose`), y los nombres o rutas de carpetas y archivos existentes.
- `.claude-plugin/marketplace.json`, los tres `plugin.json`, `skill/.skill.json`, `.mcp.json`, `icon.png`.
- Cualquier campo `version` o número de versión (solo en el paso de release).
- El frontmatter de `SKILL.md` (`name`, `description`, `metadata`): límites de plataforma.
- `LICENSE`, `PRIVACY.md`, `.gitignore`.
- El sistema de puntuación: los 30 criterios, pesos, fórmula, umbrales e identificadores de tier.
- No añadir: binarios, archivos .zip, servidores MCP, conectores, scripts, llamadas de red, dependencias ni CI.

## Reglas de trabajo
- Cambios mínimos y limitados a la tarea; sin refactors, reformateos ni "mejoras" no pedidas.
- Todo cambio del skill se aplica idéntico en `skill/` y en `plugins/bayesian-compose/skills/bayesian-compose/`.
- Todo cambio en `/bayes` se aplica idéntico en `commands/bayes.md` y en `plugins/bayesian-compose/commands/bayes.md`.
- El comportamiento en español no cambia: no borrar ni reescribir texto existente en español salvo que la tarea lo pida.
- Telemetría: nunca registrar el texto del mensaje ni datos identificativos (ver `PRIVACY.md`).
- No eliminar código, archivos, textos ni configuración sin confirmación.
- Ejecutar todos los comandos de verificación antes de terminar e incluir su salida.
- Si algo es ambiguo o exige tocar la lista "No tocar": detenerse y preguntar.

## Definición de terminado
- [ ] Todos los comandos de verificación pasan (o se indica cuál no pudo ejecutarse y por qué).
- [ ] `diff -r` entre las dos copias del skill solo muestra `.skill.json`.
- [ ] `description` del skill ≤ 500 caracteres y ≤ 1024 bytes.
- [ ] El diff solo contiene archivos dentro del alcance de la tarea.
- [ ] `CHANGELOG.md` (`[Unreleased]`) actualizado si cambia algo visible para el usuario.
- [ ] `AGENTS.md` actualizado si cambia algo que describe.
