<h1 align="center">MechaDelta</h1>

<p align="center">
  <b>Long-horizon memory for indoor service robots under a tight RAM budget.</b><br/>
  Remember what moved. Keep the heavy evidence on disk. Answer <i>"where was it before?"</i> with proof.
</p>

<p align="center">
  <img alt="ROS 2" src="https://img.shields.io/badge/ROS%202-Gazebo%20%2B%20Nav2-22314E?logo=ros">
  <img alt="FastAPI" src="https://img.shields.io/badge/API-FastAPI-009688?logo=fastapi&logoColor=white">
  <img alt="Next.js" src="https://img.shields.io/badge/UI-Next.js%2016-000000?logo=nextdotjs">
  <img alt="YOLOE" src="https://img.shields.io/badge/vision-YOLOE%20%C2%B7%20OSNet%20%C2%B7%20Qdrant-7F8CF9">
  <img alt="Final year project" src="https://img.shields.io/badge/final%20year%20project-4EBE7D">
</p>

---

## Why MechaDelta

A patrol robot sees objects move over hours and days. Logging "cup on table" every frame is wasteful, and keeping every RGB-D crop in RAM is impossible. MechaDelta makes **the transition the unit of memory**:

- 🧠 a confirmed `Table-A → Table-B` event, with time bounds and a cause that stays `unknown` unless it was observed;
- 🗃️ light object state and history in SQLite, heavy RGB-D evidence **on disk**, loaded only when a question needs it;
- ❓ historical questions answered from retained records plus evidence;
- 📏 a research lab that **measures** the accuracy-versus-storage/RAM trade-off against baselines instead of assuming it.

We are careful about what we claim: the transition ledger is our own proposal (not LT-Mem), the payload cache is PORTER-inspired (not PORTER), and the RGB-D baselines are adaptations of ReMEmbR and ConceptGraphs, not reproductions.

## Any camera, one pipeline

Every live camera runs through YOLOE and the same appearance re-ID, so a cup keeps its identity whichever camera sees it. What the system may *claim* depends on the camera:

| | RGB — phone, IP camera, webcam | RGB-D — simulator, depth camera |
|---|---|---|
| Identity | `CUP-001` | `CUP-001` |
| Position | **none, never estimated** | measured from depth |
| Support | surface class: `@ table`, `@ chair` | named table: `@ Table-A` |

## Repositories

| | Repository | What it is |
|---|---|---|
| 🧭 | [**MechaDelta**](https://github.com/MechaDelta/MechaDelta) | The organizer: links every component as a git submodule, holds the research write-ups |
| 🤖 | [**ros-pipeline-sim**](https://github.com/MechaDelta/MechaDelta-ros-pipeline-sim) | ROS 2 / Gazebo prototype: perception, re-ID, transition ledger, RAM cache, RGB-D recorder |
| ⚙️ | [**backend-server**](https://github.com/MechaDelta/MechaDelta-backend-server) | FastAPI Operations API, sensor feeds, ROS bridge and the Research Lab engine |
| 🖥️ | [**frontend**](https://github.com/MechaDelta/MechaDelta-frontend) | Next.js app: Robot Operations and Research Lab |
| 👁️ | [**vision-reid-pipeline**](https://github.com/MechaDelta/MechaDelta-vision-reid-pipeline) | Person re-ID (YOLO · OSNet · Qdrant) and the cup-memory POC |
| 📷 | [**camera-onboarding**](https://github.com/MechaDelta/MechaDelta-camera-onboarding) | Phone / IP camera capture with health telemetry and a ROS 2 publisher |
| 🧩 | [**memory-core**](https://github.com/MechaDelta/MechaDelta-memory-core) | ROS-independent interval-consolidated object memory shared by the backend and ROS |

```text
 cameras ─► camera-onboarding ─► ros-pipeline-sim ─► backend-server ─► frontend
                                   YOLOE · re-ID        feeds · lab       operations · research
                                   ledger · RAM cache        ▲
                                                       memory-core
```

## Research in the open

The Research Lab replays controlled and recorded workloads through different memory representations, residency policies and storage budgets, and keeps the measured results reproducible: transition-memory v2, a thirty-minute long-horizon study and the evidence bundles are in the [organizer's `docs/`](https://github.com/MechaDelta/MechaDelta/tree/main/docs).

## Get started

```bash
git clone --recurse-submodules https://github.com/MechaDelta/MechaDelta.git
cd MechaDelta
backend-server/START_STACK.sh start      # simulation, bridge, API, worker, phone mirror, YOLO, UI
```

Then open <http://localhost:3000> (mock sign-in `demo@mechadelta.lab` / `mechadelta`). Each repository's README has its own setup.

## How we work

- 🌿 one concern per branch — `feat/…`, `fix/…`, `docs/…`, `chore/…` — opened as a PR against the component's `main`
- ✍️ [Conventional Commits](https://www.conventionalcommits.org) with a component scope: `feat(backend): …`
- 🔀 merges use `--no-ff` and branches are kept, so the history stays readable
- 🤖 pushing to a component's `main` re-points the organizer's submodule automatically

## Team

| | |
|---|---|
| **Red0MFHA** | owner |
| **Raahim Ibrar** | Research Lab, memory evaluation, interval memory |
| **basitkhvn** | contributor |
