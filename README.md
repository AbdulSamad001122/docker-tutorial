# Docker Tutorial Projects

A collection of small projects for learning how to package and run Node.js and React applications with Docker. Each folder is a separate example, so you can build and run them independently.

## Projects

| Project | What it demonstrates | Local URL |
| --- | --- | --- |
| [`Docker-Express-App`](./Docker-Express-App/) | Containerizing a simple Express server | <http://localhost:3000> |
| [`Docker-Multistage-Building`](./Docker-Multistage-Building/) | Building an Express image with multiple Docker stages | <http://localhost:3000> |
| [`Dockerized-React-App`](./Dockerized-React-App/) | Running a React app with Vite in a container | <http://localhost:5173> |
| [`FullStack-Docker`](./FullStack-Docker/) | Running a React frontend, Express API, and PostgreSQL database with Docker Compose | <http://localhost:3000> |

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) or Docker Engine
- Docker Compose v2 (`docker compose`)
- Git, to clone the repository

Node.js is only needed if you want to run a project's development scripts directly on your computer instead of using Docker.

## Run the examples

Run these commands from the repository root.

### Express app

Build and start the container:

```sh
docker build -t docker-express-app ./Docker-Express-App
docker run --rm -p 3000:3000 docker-express-app
```

Open <http://localhost:3000>. The app responds with a greeting.

### Multi-stage Express build

Build and start the multi-stage example:

```sh
docker build -t docker-multistage-app ./Docker-Multistage-Building
docker run --rm -p 3000:3000 docker-multistage-app
```

Open <http://localhost:3000>. Stop either Express container with **Ctrl+C**.

### React app

Build and start the Vite development server:

```sh
docker build -t dockerized-react-app ./Dockerized-React-App
docker run --rm -p 5173:5173 dockerized-react-app
```

Open <http://localhost:5173>. The app uses Vite's development server and supports hot module replacement.

### Full-stack app with Docker Compose

Build and start the frontend, backend, and PostgreSQL database:

```sh
docker compose -f FullStack-Docker/docker-compose.yml up --build
```

- Frontend: <http://localhost:3000>
- Backend: <http://localhost:5001>
- Database check: <http://localhost:5001/db>

Stop the services with **Ctrl+C**, then remove the containers and network:

```sh
docker compose -f FullStack-Docker/docker-compose.yml down
```

PostgreSQL data is stored in the `pgdata` named volume and remains after `down`. To also delete that data, use:

```sh
docker compose -f FullStack-Docker/docker-compose.yml down --volumes
```

> **Note:** The Compose file uses a simple hard-coded PostgreSQL password for local learning. Do not use these credentials or this setup as-is for a public or production deployment.

## Run without Docker

For either React project, install dependencies and start Vite from that project's directory:

```sh
npm install
npm run dev
```

For either standalone Express project, install dependencies and start the server from its directory:

```sh
npm install
npm run dev
```

The full-stack backend can also be started from `FullStack-Docker/backend` with `npm install` and `npm start`; it expects a PostgreSQL database configured through the `DB_HOST`, `DB_USER`, `DB_PASS`, and `DB_NAME` environment variables.

## Repository notes

- Each project has its own `package.json` and dependency lockfile.
- `.gitignore` excludes dependencies, generated output, local environment files, and common temporary files from Git.
- `.dockerignore` files keep unnecessary files out of the Express Docker build contexts.
