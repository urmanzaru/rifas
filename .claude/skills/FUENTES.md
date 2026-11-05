# Skills de terceros

Copiadas tal cual desde sus repositorios. Para actualizarlas, vuelve a copiar la carpeta desde la versión nueva.

| Skill | Repositorio | Commit | Licencia |
| --- | --- | --- | --- |
| `ui-ux-pro-max` | https://github.com/nextlevelbuilder/ui-ux-pro-max-skill (`.claude/skills/ui-ux-pro-max`) | `ccce51cba388476d4f403091ddb91636d5cd9fed` | MIT |
| `impeccable` | https://github.com/pbakaus/impeccable (`.claude/skills/impeccable`) | `83dc1bbe4c37636632e72a7752e9cc433e9a9901` | Apache 2.0 |

## Notas

- **impeccable** descarga un ejecutable propio la primera vez que se usa, desde los releases de GitHub del autor. Lo verifica contra las sumas SHA-256 de `impeccable/scripts/engine-checksums.txt`. Si la red no lo permite, la skill sigue funcionando leyendo los archivos directamente.
- **impeccable** puede instalar un hook que revisa el diseño después de cada edición, pero solo si alguien corre `/impeccable hooks on`. No viene activado.
- **ui-ux-pro-max** usa Python 3 sin dependencias. Su buscador está en `ui-ux-pro-max/scripts/search.py`.
- `frontend-design` no está aquí: es un plugin oficial de Anthropic y se instala desde el directorio de plugins de claude.ai.
