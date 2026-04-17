# WellAI Bot - Smart Health Connect

## Setup

### Prerequisites

- Docker
- Git

### Clone with submodules

```sh
git clone --recurse-submodules <repository-url>
cd wellai-bot
```

If you already cloned the repository without submodules:

```sh
git submodule update --init --recursive
```

### Configure environment variables

Copy the root environment template and fill in your WhatsApp credentials:

```sh
cp .env.example .env
```

For WhatsApp environment setup details, read the README for the bot service.

Set `WHATSAPP_HTTP_PORT` in `.env` if you want to expose the webhook on a different local port (default: `5000`).

Use ngrok or a similar tool to create a public URL for the webhook and set that in your WhatsApp Cloud API configuration.

### Build and start services

```sh
docker compose up --build
```

This starts:

- `agent` gRPC service on internal Docker network port `50052`
- `bot` gRPC service on internal Docker network port `50051`
- `bot` WhatsApp webhook HTTP service exposed to host on `WHATSAPP_HTTP_PORT` (default: `5000`)

### Check service health

```sh
docker compose ps
```

Use the status output to confirm both containers are running.

### Inspect service logs

Stream logs from both services:

```sh
docker compose logs -f agent bot
```

Stream logs for a single service:

```sh
docker compose logs -f agent
docker compose logs -f bot
```

### Stop services

```sh
docker compose down
```
