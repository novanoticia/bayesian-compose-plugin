# Changelog

Todos los cambios relevantes del plugin/skill `bayesian-compose` se documentan aquí. Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/); versionado [SemVer](https://semver.org/lang/es/) (mayor = ruptura, menor = ampliación, parche = correcciones).

## [1.3.0] — 2026-10-06

### Añadido
- Soporte en francés con `references/i18n/fr.md` en ambas copias del skill.
- Traducción de la documentación en `README.fr.md`.
- Reconocimiento a Codex de OpenAI (ChatGPT) en los créditos de ambos README.

### Corregido
- El comando `/bayes` ahora se incluye en el plugin instalable.
- Eliminado el párrafo duplicado de `SKILL.md`.
- Eliminadas las referencias de versión desfasadas en `marketplace.json` y `config.yaml`.

## [1.2.0] — 2026-10-06

### Añadido
- Soporte multiidioma en español (`es`) e inglés (`en`), ampliable a otros idiomas.
- Selección automática del idioma de interacción con `idioma: "auto"`.
- Tabla de equivalencias al inglés en `references/i18n/en.md`.
- Traducción completa de la documentación en `README.en.md`.

### Cambiado
- Valor por defecto de `idioma` de `"es"` a `"auto"`, sin cambio para quien escribe en español.

## [1.1.0] — 2026-06-10

### Añadido
- Compatibilidad de instalación con **Mistral AI** (espacio *Work*): descomprimir el bundle y seleccionar la carpeta `bayesian-compose/`. Documentada en el README.

### Cambiado
- **`SKILL.md` — `description` reducida a 434 caracteres / 446 bytes** (antes 603) para cumplir el límite de 500 caracteres que aplica Mistral, conservando la inversión epistémica y los gatillos de activación. Bundle `bayesian-compose.zip` regenerado.
- README: nota técnica actualizada con los límites por plataforma (Perplexity 1024 bytes, Mistral 500 caracteres).

### Notas
- Sin cambios de comportamiento del skill; el salto refleja la ampliación de plataformas soportadas.

## [1.0.0] — versión inicial

### Añadido
- Skill de composición epistémica de mensajes: entrevista socrática, 30 criterios de racionalidad bayesiana (LessWrong) invertidos para emisión y scoring en tres niveles. Disponible como plugin de Claude Code y como bundle subible a Claude.ai y Perplexity.
