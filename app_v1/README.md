# app_v1

Como executar (desenvolvimento):

Prerequisitos: Docker e Docker Compose v2.

No PowerShell (a partir da pasta app_v1):

- Construir imagens:
  docker compose build

- Subir serviços em segundo plano:
  docker compose up -d

- Logs:
  docker compose logs -f

- Parar e remover:
  docker compose down

Boas práticas e notas:
- As imagens usam python:3.11-slim e pip com --no-cache-dir.
- Containers não rodam como root (usuário appuser UID 1000).
- Em desenvolvimento usamos bind mounts (volumes) para hot-reload.
- Variáveis de ambiente para conectar ao Postgres e backend estão declaradas no docker-compose.
- Arquivo .dockerignore exclui arquivos sensíveis/ocasionais incluindo .env.
