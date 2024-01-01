---

# Docker Compose Configuration

## `docker-compose.yml`

```yaml
version: "3.8"

services:
  package:
    image: node:16
    tty: true
    stdin_open: true
    working_dir: /home/package
    environment:
      - MEILISEARCH_URL=http://meilisearch:7700
    depends_on:
      - meilisearch
    links:
      - meilisearch
    volumes:
      - ./:/home/package

  meilisearch:
    image: getmeili/meilisearch:latest
    ports:
      - "7700"
    environment:
      - MEILI_MASTER_KEY=masterKey
      - MEILI_NO_ANALYTICS=true
```

## Service Descriptions

### 1. `package` Service

- **Image:** `node:16`
- **Options:**
  - TTY and stdin open for debugging and interaction.
  - Working directory set to `/home/package` inside the container.
- **Environment Variables:**
  - `MEILISEARCH_URL` set to `http://meilisearch:7700`.
- **Dependencies:**
  - Depends on the `meilisearch` service.
- **Links:**
  - Links to the `meilisearch` service.
- **Volumes:**
  - Mounts the current directory (`.`) to `/home/package` inside the container.

### 2. `meilisearch` Service

- **Image:** `getmeili/meilisearch:latest`
- **Ports:**
  - Exposes port `7700`.
- **Environment Variables:**
  - `MEILI_MASTER_KEY` set to "masterKey".
  - `MEILI_NO_ANALYTICS` set to "true".

## How to Run

```bash
docker-compose up
```

This command will start the defined services and set up the specified configurations.

---

Feel free to customize this documentation further based on your specific needs.
