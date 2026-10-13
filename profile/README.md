# MechaDelta

> **Long-horizon indoor robot memory under a tight RAM budget** — store object transitions, keep heavy 3D evidence on disk until a question needs it.

MechaDelta is a unified platform for patrol-scale service robots: observe what moves, remember transitions cheaply, answer historical questions with evidence, and operate the whole stack from a single web workspace.

## Components

| Component | Repository | What it does |
|---|---|---|
| ROS Pipeline Simulation | [MechaDelta-ros-pipeline-sim](https://github.com/MechaDelta/MechaDelta-ros-pipeline-sim) | ROS 2 / Gazebo feasibility prototype for transition-centric object history and RAM evidence cache |
| Backend Server | [MechaDelta-backend-server](https://github.com/MechaDelta/MechaDelta-backend-server) | FastAPI backend for Operations (MVC, SQLite/Postgres, ROS bridge, LiveKit) |
| Frontend | [MechaDelta-frontend](https://github.com/MechaDelta/MechaDelta-frontend) | Next.js app: Robot Operations + Research Lab workspaces |
| Vision Pipeline & ReID | [MechaDelta-vision-reid-pipeline](https://github.com/MechaDelta/MechaDelta-vision-reid-pipeline) | YOLO person ReID pipeline and embodied AI cup-memory POC |

The [organizer repository](https://github.com/MechaDelta/MechaDelta) links every component as a git submodule and tracks each component's `main`.

## Getting started

```bash
git clone --recurse-submodules https://github.com/MechaDelta/MechaDelta.git
cd MechaDelta
```

See [MechaDelta/MechaDelta](https://github.com/MechaDelta/MechaDelta) for setup and [AGENT_HANDOVER.md](https://github.com/MechaDelta/MechaDelta/blob/main/AGENT_HANDOVER.md) for the contribution workflow (branch in a component repo, open a PR against its `main`).

## Team

- `Red0MFHA` — owner
- `raahim-ibrar`
- `basitkhvn`
