# Code structure

Open `START-HERE.md` first. Keep the existing folder names: source imports and Dockerfiles depend on them.

| Path | Purpose |
| --- | --- |
| `app/` | Next.js routes, pages, global styling, and metadata |
| `components/` | Dashboard, map, driver, preparedness, and shared UI components |
| `lib/` | Shared TypeScript utilities, map rendering, simulation, and domain logic |
| `convex/` | Real-time backend schema, queries, mutations, workflows, simulation, and generated bindings |
| `voice/` | Phone server, conversation agent, speech integrations, callbacks, and voice tests |
| `dispatch/` | Python routing optimizer, HTTP solver service, simulations, and tests |
| `modeling/` | Python population and risk modeling tools |
| `public/` | Static images, maps, graphics, and presentation assets |
| `data/` | Bundled sample/synthetic data and upstream evaluation outputs |
| `tests/` | Workflow and incident integration tests |
| `scripts/` | Evaluation, data preparation, stress testing, recording, and operational scripts |
| `apify/` | Evacuation-status ingestion Actor |
| `video/` | Remotion presentation/video project, with its own dependencies |
| `deploy/` | Non-secret Railway resource configuration reference |
| `docs/` | Additional architecture and feature documentation |
| `package.json`, `package-lock.json` | Web/voice dependencies, pinned dependency tree, and npm commands |
| `.env.example` | Minimal web app environment variable template |
| `.env.voice.example` | Separate optional voice-service variable template |
| `README.md` | Original project README and credits |
| `RAILWAY-SETUP.md` | Previous chat's Railway deployment and recovery notes |
| `AGENTS.md`, `PLAN.md`, `HANDOFF.md` | Preserved upstream development and handoff documentation |

## Important entry points

| Feature | Entry point |
| --- | --- |
| Call dashboard | `app/dashboard/page.tsx` |
| Rescue map | `app/map/page.tsx` |
| Driver page | `app/driver/page.tsx` |
| Household preparedness | `app/ready/page.tsx` |
| Shared backend schema | `convex/schema.ts` |
| Simulation control | `convex/control.ts` |
| Dispatch coordination | `convex/dispatch.ts` |
| Voice HTTP server | `voice/server.ts` |
| Voice configuration | `voice/env.ts` |
| Python solver HTTP server | `dispatch/server.py` |
| Optimizer | `dispatch/alns.py`, `dispatch/solver.py`, `dispatch/heuristic.py` |

Frontend, voice server, and solver use the same backend state. Run the web app with a configured Convex deployment before enabling optional external integrations.
