# GVP-Guard: NightEye AI

> Turning suspected night-time dumping events into review-ready evidence and faster municipal action.

**Problem Statement:** PS000048 | **Team:** TM004162 | **Institution:** P. P. Savani University, Surat, Gujarat
**Project Lead:** Omkar Solat

![Status](https://img.shields.io/badge/status-proof%20of%20concept-orange)
![Round](https://img.shields.io/badge/round-online%20PPT%20%2B%20demo-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## Overview

GVP-Guard: NightEye AI is a **human-reviewed illegal-dumping incident and evidence platform**. It helps municipal officers convert suspicious night-time activity at *Garbage Vulnerable Points (GVPs)* into a structured incident containing:

- Visual evidence (before, during and after)
- A number-plate candidate, when available
- Time and location
- An officer decision

> **The platform never automatically declares a person or vehicle guilty.** A vehicle stop only creates a *suspected* event. Supporting visual cues and a final human review are required before any municipal action.

## The Problem

Gandhidham is a logistics, timber-transit and warehousing hub. Commercial packaging, timber scrap and mixed waste are often dumped at night on open plots, service lanes and peripheral roads, and repeat dumping turns these places into chronic GVPs.

- Sanitation squads cannot patrol every dispersed industrial location overnight.
- Existing CCTV is mostly passive and needs hours of manual review.
- Glare, blur, dust and camera angle make plate reading unreliable.
- Waste often stays until a complaint triggers cleanup.
- Waste may already be present before a vehicle arrives, so vehicle presence alone is not proof of dumping.

**Core challenge:** detecting a vehicle is easy; showing that an event is *probably* dumping, without falsely accusing anyone, is hard.

## How It Works

1. **Video input**: recorded footage now; live webcam/CCTV planned.
2. **GVP zone**: only a configured area of the camera view is monitored.
3. **Track and halt**: a vehicle or person is tracked; stop time creates a *suspected* event.
4. **Dumping cues**: person movement, object transfer, before/after scene change.
5. **Evidence extraction**: before, during and after frames plus the relevant clip.
6. **ANPR attempt**: best plate frames are selected and OCR proposes a candidate.
7. **Incident generation**: ID, time, location, evidence, plate candidate and confidence.
8. **Officer review**: approve, reject or request cleanup.
9. **History and GVP update**: decisions are retained for monitoring.

> **Decision rule:** Stop time is only a trigger, not proof.

### Event States

| State | Meaning | System action |
|---|---|---|
| Normal | No suspicious evidence | No incident created |
| Suspicious halt | Stop threshold crossed | Continue checking cues |
| Probable event | Multiple visual cues agree | Create evidence for review |
| Low confidence | Insufficient evidence | Route to manual review |
| Approved | Officer accepts incident | Official follow-up |
| Rejected | Evidence insufficient | Close with audit result |

## Current Prototype Status

This is a **browser-based workflow proof of concept** using controlled recorded footage. **No field accuracy is claimed.**

| Module | Status | Capability |
|---|---|---|
| Video | ✅ Working | Upload and playback of a controlled clip |
| Evidence | ✅ Working | Before, during and after frame extraction |
| Scene comparison | ✅ Working | Pixel-based before/after change percentage |
| Incident record | ✅ Working | Incident ID, timestamp, editable plate field, decision |
| Dashboard | ✅ Working | Approve, reject, request cleanup |
| History | ✅ Working | Local incident history and audit result |
| GVP map | ✅ Working | Illustrative priority zones and incident counts |
| Export | ✅ Working | Downloadable structured JSON incident record |
| Vehicle AI | 🟡 Demo stage | Visual tracking workflow; model integration pending |
| ANPR | 🟡 Demo stage | Editable candidate; real multi-frame OCR pending |
| Dumping model | 🔵 Planned | Needs multiple cues and controlled training/testing data |
| GMC pilot | ⚪ Future | Needs official footage, sites and permissions |

## System Architecture

Six connected layers:

1. **Video Input**: recorded video (MVP); webcam / IP camera / RTSP (next).
2. **Event Intelligence**: tracking, zone entry, stop-time trigger, object-transfer cues, scene comparison.
3. **Vehicle Identification**: plate-region detection, best-frame selection, enhancement, OCR, multi-frame agreement, manual correction.
4. **Evidence Preparation**: incident ID, timestamp, location, before/during/after images, clip, plate crop, confidence.
5. **Municipal Workflow**: alerts, evidence review, approve/reject, cleanup request, comments, audit status.
6. **GVP Monitoring**: repeat-location history, time patterns, response delay, cleanup status, transparent priority score, map.

*Future edge concept:* an edge device filters frames and uploads only triggered clips. Camera capacity and cost must be benchmarked before any scale claims.

## Proposed Technology Stack

> These are **proposed next-stage choices**, not claims of completed integration.

| Component | Proposed choice |
|---|---|
| Video processing | Python, OpenCV |
| Vehicle detection | YOLO11 nano/small or another lightweight detector |
| Tracking | ByteTrack (simple IoU tracker as MVP fallback) |
| ANPR | Plate detector + EasyOCR (PaddleOCR as backup) |
| Backend | FastAPI |
| Database | Supabase PostgreSQL |
| Evidence storage | Supabase Storage or controlled local storage |
| Dashboard | Next.js / React with Tailwind CSS |
| Map | Leaflet with OpenStreetMap |

## Night ANPR Approach

One OCR call on one frame is not enough. The planned pipeline:

1. Detect vehicle and plate region
2. Track the plate across frames
3. Score frames (sharpness, brightness, glare, size, angle)
4. Select the best 3-5 frames
5. Crop, perspective-correct and enhance for low light
6. Run OCR on each selected frame
7. Use majority agreement on characters
8. Validate against Indian registration formats
9. Show confidence and allow officer correction

**The system never invents a registration number.** If a plate is unreadable, the incident remains valid for cleanup and review.

## Getting Started

> The repository structure below is the planned layout. Update it to match your actual folders.

```bash
# Clone the repository
git clone https://github.com/<your-username>/gvp-guard-nighteye-ai.git
cd gvp-guard-nighteye-ai
```

**Run the browser prototype**

```bash
# If it is a static prototype, simply open index.html in a browser,
# or serve it locally:
python -m http.server 8000
# then visit http://localhost:8000
```

**Planned backend (next stage)**

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### Planned Repository Structure

```
gvp-guard-nighteye-ai/
├── prototype/        # Browser-based workflow demo
├── backend/          # FastAPI incident and evidence APIs (planned)
├── ml/               # Vehicle tracking, event cues, ANPR (planned)
├── dashboard/        # Next.js officer dashboard (planned)
├── docs/             # Handbook, slides, diagrams
├── data/             # Controlled test data (not committed)
└── README.md
```

## Testing and KPIs

Testing uses controlled recordings made in permitted locations with clean boxes or bags, plus legally usable public footage. Gandhidham-specific tuning requires GMC-approved footage.

**Scenarios:** normal stop, long stop without dumping, controlled deposit, waste already present, poor lighting/glare, partial or unreadable plate, person-only and vehicle events.

**Pilot KPIs:** correct plate-read rate, false alerts per camera-hour, dumping-event precision, alert-to-action time, evidence completeness, repeat incidents per GVP.

> Accuracy or impact percentages are published only when backed by documented tests. Pilot targets are labelled as targets, not achievements.

## Roadmap

| Stage | Focus |
|---|---|
| 1. Online Round | Controlled-video workflow, evidence, scene comparison, dashboard, PPT and demo video |
| 2. Next Prototype | Live webcam/CCTV input, vehicle tracking, better dumping cues, multi-frame ANPR |
| 3. Pilot Preparation | GMC-approved footage, camera assessment, privacy/retention rules, two pilot sites |
| 4. Two-Site GMC Pilot | Tune for local night conditions; measure false alerts, plate reads, response time |
| 5. Validated Expansion | Add GVP zones only after targets, cost, privacy and capacity are accepted |

## Privacy and Responsible Use

- Human approval before any enforcement
- Role-based access in a production dashboard
- Audit log of decisions and status changes
- Policy-approved evidence-retention period
- Upload only triggered clips where practical
- Clear display of uncertainty and confidence
- Manual review for unreadable plates and ambiguous events
- Official permission before any registry or e-challan integration

### What this project does **not** claim

- Automatic guilt or automatic fines
- Guaranteed identification of every vehicle
- Legally admissible evidence
- Measured Gandhidham field accuracy
- Real vehicle-registry access
- Citywide production readiness
- Autonomous drone verification
- Accurate prediction of future dumping

## Team Roles

| # | Role | Output |
|---|---|---|
| 1 | Team Lead & Integration | Consistent product, deck and demo |
| 2 | Vehicle Detection & Tracking | Tracked vehicle video |
| 3 | Event Detection & Dataset | Event logic and test data |
| 4 | ANPR & Image Processing | Reviewed plate candidate pipeline |
| 5 | Backend & Evidence | Stored/retrievable incident record |
| 6 | Dashboard & UX | Officer-facing dashboard |
| 7 | Testing & Civic Research | Evaluation report |
| 8 | Video, PPT & Pitch | Submission package |

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and our [Code of Conduct](CODE_OF_CONDUCT.md). To report a vulnerability, see [SECURITY.md](SECURITY.md).

## License

Released under the [MIT License](LICENSE).

---

**GVP-Guard does not replace municipal officers.** It helps them find, review and act on suspected dumping incidents faster and more consistently.
