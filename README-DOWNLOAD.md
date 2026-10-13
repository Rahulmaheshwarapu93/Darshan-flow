# DarshanFlow full-stack export

This folder preserves the pnpm workspace layout required by the project.

## Requirements

- Node.js 20 or newer
- pnpm 9 or newer
- PostgreSQL 14 or newer
- VS Code, Google Antigravity, or any editor with a terminal works

## Install

```bash
cd darshanflow
corepack enable
corepack prepare pnpm@latest --activate
pnpm install
```

## Configure the database and session secret

Set these environment variables in the terminal before starting the API. The server does not automatically load a `.env` file:

```bash
export DATABASE_URL=postgresql://USER:PASSWORD@localhost:5432/darshanflow
export SESSION_SECRET=replace-with-a-long-random-local-secret
```

## Initialize the database

```bash
pnpm --filter @workspace/db run push
```

## Start the backend

In terminal 1:

```bash
PORT=8080 pnpm --filter @workspace/api-server run dev
```

## Start the frontend

In terminal 2:

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/darshanflow run dev
```

Open http://localhost:5173.

The Vite development proxy forwards `/api` and `/socket.io` to the backend at http://localhost:8080.

## Windows PowerShell

```powershell
$env:DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/darshanflow"
$env:SESSION_SECRET="replace-with-a-long-random-local-secret"
pnpm install
pnpm --filter @workspace/db run push
$env:PORT="8080"; pnpm --filter @workspace/api-server run dev
```

Open a second PowerShell terminal, set the same database variables, then run:

```powershell
$env:PORT="5173"; $env:BASE_PATH="/"; pnpm --filter @workspace/darshanflow run dev
```

Do not commit real secrets or production database credentials.
