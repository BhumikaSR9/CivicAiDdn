# 🏛️ CivicAI — Smart Public Grievance Management Platform

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue.svg)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688.svg)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/React-18-61DAFB.svg)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.6-blue.svg)](https://www.typescriptlang.org)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.4-38B2AC.svg)](https://tailwindcss.com)
[![Status](https://img.shields.io/badge/Production-Ready-emerald.svg)]()

**CivicAI** is an AI-powered, multi-tenant, white-label civic redressal and SLA enforcement command platform built for modern municipal corporations. Tested and calibrated for **Dehradun Municipal Corporation (Uttarakhand)** across 12 wards and 8 departments.

---

## ⚡ 5-Command Quickstart

```bash
# 1. Clone & Enter Directory
cd CivicAI

# 2. Setup Python Virtual Environment & Dependencies
python -m venv .venv
source .venv/bin/activate  # Or on Windows: .venv\Scripts\activate
pip install -r backend/requirements.txt

# 3. Seed 800 Historical Complaints & Demo Accounts
python scripts/seed.py
# The development API uses this repository-root civicai.db regardless of its working directory.

# 4. Start Backend API Server (Port 8000)
cd backend && uvicorn app.main:app --reload --port 8000

# 5. Start Frontend Development Server (Port 5173) in a second terminal
cd frontend && npm install && npm run dev
```

---

## 🔑 Demo Personas & Credentials

All test accounts use the password: `password123`

| Persona | Role | Email | Capabilities |
| :--- | :--- | :--- | :--- |
| **City Admin** | `admin` | `admin@civicai.gov.in` | GIS Command Center, Heatmaps, Hotspots, SLA Escalation Rules, PDF Reports |
| **Nodal Officer** | `officer` | `officer@civicai.gov.in` | Kanban Triage, Mandatory Reassignment Reason, Retraining AI Corrections |
| **Field Worker** | `field_worker` | `worker@civicai.gov.in` | Mobile PWA View, GPS Turn-by-Turn, Camera After-Photo Resolution |
| **Citizen** | `citizen` | `citizen@civicai.gov.in` | 3-Step Wizard, Voice-to-Text, Delivery Timeline, Verification 1-5★ Rating |

---

## 🚀 Key Feature Matrix

### Citizen Experience
- **F1: 3-Step Grievance Wizard (Snap, Locate, Confirm)**: Client-side WebWorker image compression, EXIF GPS coordinate extraction and privacy-preserving metadata stripping, Web Speech voice-to-text input, and unique alphanumeric tracking IDs (`CVC-YYYY-XXXXXX`) with downloadable QR codes.
- **F2: Real-time Animated AI Chips**: Sub-3-second CPU inference predicting category, department routing, and priority rating before final submission.
- **F3: Geospatial Precision**: Draggable Leaflet pin, 'Use my GPS' geolocate, Nominatim reverse geocoding with rate-limiting cache, Point-in-Polygon ward auto-detection (`shapely`), and >300m EXIF GPS mismatch alert.
- **F4: Multimodal Duplicate Detection**: 150m spatial query combined with multimodal similarity (0.5 text Jaccard + 0.3 image pHash + 0.2 distance decay). High duplicates (>0.82) auto-link; near-duplicates (0.65-0.82) prompt citizens to "Me Too" upvote.
- **F6: Delivery-Style Live Tracking**: Transparent timeline stages (*Submitted* → *Triaged* → *Assigned* → *In Progress* → *Resolved* → *Verified*), SLA countdown timer, before/after interactive image comparison slider, and 1-5 star citizen closure confirmation (+15 Civic Points).

### Operational & Command Center
- **F5: Department Routing & Officer Workflow**: Category-to-department matrix, ward-based officer assignment, mandatory reassignment audit reason, and immutable event logs.
- **F7: Spatial Hotspot Clustering**: HDBSCAN/DBSCAN spatial clustering on Haversine distance generating Shapely convex hull polygons and priority-weighted severity scores.
- **F8: Geo Command Center**: Fullscreen GIS map featuring ward choropleths, HDBSCAN cluster polygons, pulsing coral SLA-breach pins, KPI performance counters, slide-over complaint drawers, and AI daily briefings (E9).
- **F9: Executive Reporting Engine**: Automated monthly and on-demand report exports in PDF (ReportLab), CSV, and responsive HTML format.

### Platform Extras (E1 - E15)
- **E1**: Full Hindi (हिन्दी) & English bilingual localization via `i18next`.
- **E2**: "Me Too" duplicate upvote counters amplifying high-density neighborhood issues.
- **E3**: Explainable AI priority decision cards (Top-3 reasons).
- **E4**: Officer feedback loop tracking AI corrections (`scripts/retrain.py`).
- **E5**: Automated 3-tier SLA escalation engine (L1 → L2 → L3).
- **E6**: Interactive split before/after verification slider.
- **E7**: Gamification with Civic Points and badges (*Clean Warden*, *Civic Guardian*).
- **E8**: Public transparency portal with live city KPIs and resolution showcase.
- **E9**: Daily AI executive operational narrative brief.
- **E10**: Monsoon-aware Himalayan ETA prediction model (July-September regression boost).
- **E11**: 'Ask CivicAI' interactive floating assistant answering tracking IDs and FAQs.
- **E12**: Multi-city white-label tenant architecture configured via `config/city.json`.
- **E13**: External developer API keys with scoped HMAC authorization.
- **E14**: Immutable audit log table recording every administrative action.
- **E15**: WCAG AA accessible dark mode with mission control styling.

---

## 🧪 Testing & Validation

Backend includes 36 unit and integration tests covering auth, filing, ML inference, SLA escalations, geo PIP, and report generation:

```bash
# Run backend test suite
pytest backend/tests/ -v

# Run frontend production build
cd frontend && npm run build
```

---

## 🏛️ City Customization & White-Labeling

To adapt CivicAI to any new city, edit `config/city.json`:

```json
{
  "city_name": "Dehradun",
  "state": "Uttarakhand",
  "center": [30.3165, 78.0322],
  "zoom": 12,
  "tenant_slug": "dehradun",
  "branding": {
    "primary_color": "#0B1220",
    "accent_color": "#F59E0B"
  }
}
```
GeoJSON boundary and ward files are stored in `data/geojson/`.

---

## 📦 Docker Deployment

```bash
# Launch PostgreSQL, FastAPI, and Nginx Web with one command:
docker-compose up -d --build
```
Web app will be available at `http://localhost:3000` and API documentation at `http://localhost:8000/docs`.
