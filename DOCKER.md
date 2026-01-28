# Docker Compose Setup

This project is set up to run within a Docker container using a generic Node.js LTS image.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1.  **Start the container:**

    ```bash
    docker compose up -d
    ```

2.  **Attach to the container shell:**

    ```bash
    docker compose exec antigravity bash
    ```

    *Note: The container automatically runs `npm install`, `npm run build`, and `npm link` on startup.*

## Persistence

Authentication tokens and configuration are persisted in a Docker volume named `antigravity_config`. This ensures your login state is maintained even if you restart or recreate the container.

## Authentication

To log in with Google, you must use the exposed port `8765` and disable the automatic browser opening (since the container is headless).

Run this command inside the container:

```bash
antigravity-usage login --no-browser
```

1.  The CLI will print an authentication URL.
2.  Open that URL in your host machine's browser.
3.  Complete the login flow.
4.  You will be redirected to `http://127.0.0.1:8765/callback...`. Since port 8765 is forwarded, this request will reach the container and complete the login process.

## Usage

Once logged in, you can run commands as usual:

```bash
antigravity-usage quota --all
```