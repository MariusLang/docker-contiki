# docker-contiki

[Contiki](https://github.com/contiki-os/contiki) Docker image for a university course on networked embedded systems. Supports msp430 and simulations via Cooja.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/)

## Setup

1. Clone this repository
2. Create a `src` directory (it will be mounted in the container at `/home/user/src`)

```bash
mkdir src
```

## Running Cooja

### macOS

1. Install and open [XQuartz](https://www.xquartz.org/)
2. Go to **Preferences -> Security** and enable **"Allow connections from network clients"**
3. Restart XQuartz
4. Allow connections:
   ```bash
   xhost +localhost
   ```
5. Start Cooja:
   ```bash
   docker compose up
   ```

### Linux (Debian/Ubuntu)

1. Allow X11 connections from Docker:
   ```bash
   xhost +local:docker
   ```
2. Start Cooja:
   ```bash
   docker compose -f docker-compose.linux.yml up
   ```

## Development

### Building from Source

```bash
docker compose -f docker-compose.build.yml build
```

### Publishing to Docker Hub

```bash
# Create buildx builder (one-time setup)
docker buildx create --name multiarch --driver docker-container --use

# Build and push multi-platform image
docker buildx build --platform linux/amd64,linux/arm64 \
  -t mariuslang/contiki:latest \
  --push .
```
