# Standard Response — Start Here

This is the complete source bundle recovered from the earlier chat, organized in its existing project folders. Application source and original documentation are preserved byte for byte. This package adds this guide, a folder map, configuration templates, and a file checksum manifest.

## 1. Extract the ZIP

Use “Extract All” on Windows. Open the extracted `standard-response` folder in VS Code, then open Terminal → New Terminal. Run all root-level commands from the folder containing `package.json`.

## 2. Start the simulated demo

Install Node.js 22 (the version used by the included voice Dockerfile), npm, and Git if needed. A separate Convex development deployment is required for database functions and live updates.

In the first terminal:

```sh
npm ci
npx convex dev
```

Follow the Convex CLI setup prompts to create your own development deployment. Keep this terminal running. It generates the backend configuration and normally writes the deployment URL to `.env.local`.

If `NEXT_PUBLIC_CONVEX_URL` is missing, add the development deployment's URL to `.env.local`; `.env.example` shows the variable name. Preserve any variables the CLI already wrote.

In a second terminal, in the same folder:

```sh
npm run dev
```

Open the localhost address printed in the terminal, normally `http://localhost:3000/dashboard`. The rescue map is at `/map`, the driver interface at `/driver`, and preparedness enrollment at `/ready`.

Use the interface's simulation/stand-in controls for a demo. Start with the Ready Check, then the evacuation warning workflow. A new backend may need demo initialization through the app controls; this archive contains source, not a copy of the running database. See `convex/control.ts` and the original `README.md` for the simulation controls.

The simulated workflow does not require a paid phone provider. Real calls require the separate configuration below.

## 3. Optional real phone calls

The phone server source is in `voice/`. Use `.env.voice.example` as a reference and add your own provider credentials to `.env.local`; do not overwrite the Convex configuration already there.

The default carrier is Twilio. Its REST API uses an API key SID and API key secret in addition to the account SID and webhook auth token. Speech uses Cartesia, and the interpreter uses Anthropic. Choose voice IDs and a model available in your provider accounts; check `voice/env.ts` for all settings and source defaults.

The server must have a reachable HTTPS URL in `VOICE_PUBLIC_URL` for phone-provider callbacks. Add only your own test numbers to `DIAL_ALLOWLIST` when testing.

```sh
npm run dev:voice
```

A production service can run `npm run voice` with variables injected by its host. Configure the corresponding backend and UI stand-in switches for real integrations only after those services are ready. Real phone service was not exercised while packaging this ZIP.

## 4. Optional Python dispatch service

The Python optimizer is in `dispatch/`, with its own `pyproject.toml`, `uv.lock`, and Dockerfile. It is separate from the web app.

With uv installed:

```sh
cd dispatch
uv sync
uv run python server.py
```

It listens on port 8799 by default and exposes `/health` and `/solve`. A hosted backend needs a reachable solver endpoint; a backend in the cloud cannot reach the solver at your laptop's localhost. Configure `SOLVER_URL` and the matching `SOLVER_TOKEN` in the backend environment when using the external solver. See `dispatch/server.py` and `RAILWAY-SETUP.md`.

## 5. Production and Railway

Read `RAILWAY-SETUP.md` for the deployment architecture from the previous chat. The web build/start commands are:

```sh
npm run build
npm run start
```

Set `NEXT_PUBLIC_CONVEX_URL` before building the web app. The Convex backend, voice service, and Python solver are separate components; the ZIP is not a database backup or a one-command clone of the running Railway environment.

## 6. Code and verification

- `CODE-STRUCTURE.md`: folder map and important files.
- `README.md`: original technical description, results, and commands.
- `RAILWAY-SETUP.md`: previous deployment/recovery notes.
- `PACKAGE-MANIFEST.json`: SHA-256 checksums for every included file except the manifest itself.

The package was checked for ZIP integrity, required source folders, and byte-for-byte preservation of the original files. Dependency installation, builds, and live integrations were not rerun for this packaging request. Existing test scripts remain in `package.json`.
