# 🛡 Sentinel Grid — Disaster Intelligence UI / UX Platform

> **Live Disaster Intelligence & Emergency Response Dashboard**  
> Built for the **IBM BOB National Hackathon Grand Finale 2026** (Problem Statement 1: AI-Powered Disaster Early Warning & Rescue Intelligence).

---

## 🌟 Overview

The **Sentinel Grid Frontend** is a control-room grade GIS dashboard engineered for district disaster controllers, NDRF commanders, and municipal emergency teams during severe monsoon inundation events.

### Core Capabilities:
1. **Interactive 4-Mandate Decision Engine**:
   - `1. 🗺 WHERE Risk` — Visualizes 17 RED hazard zones, 8 GREEN safe havens, and 8 BLUE epistemic uncertainty sectors.
   - `2. 👥 WHO & WHAT` — Pins critical assets (hospitals, power substations) and flags chokepoints like the submerged Noyyal River Bridge (2.1m overtopped).
   - `3. ⚡ WHICH First` — Displays triage rankings calculated using survivability decay:
     $$S(t) = \exp(-t / \tau)$$
   - `4. 🚶 SAFEST Route` — Renders 300+ turn-by-turn road waypoints along Avinashi Rd, Trichy Rd, and Pollachi Hwy safely detouring flooded river corridors to Annur and Sulur relief centers.
2. **Interactive Storm Simulation Console**:
   - Live sliders for **Noyyal River Gauge Level** (0 to 6m), **Precipitation** (0 to 250mm), and **SAR Satellite Pass Staleness** (0 to 24h) that trigger real-time AI reclassification.
3. **Multi-Modal Survivor Detection & Bio-Radar Trace**:
   - Displays fused telemetry (Thermal Infrared, Optical rPPG Pulse, Acoustic Distress) and an oscilloscope-style bio-radar vital waveform (BPM and Respiration RPM).
4. **Machine Learning Model Cards**:
   - Built-in verification tab showing validation benchmarks for trained XGBoost ($91.72\%$ accuracy, $0.9777$ ROC-AUC) and LightGBM models.
5. **NDRF Incident Action Plan (IAP) Generator**:
   - One-click exportable operational order formatted to official NDRF / SDMA response standards.

---

## 🚀 Quick Start (Running Locally)

### Option 1: Python Built-in Server (Zero Dependencies)
```bash
cd sentinel-grid-frontend
python3 -m http.server 8000
```
Open your browser at: **`http://localhost:8000`**

### Option 2: Node.js / npx
```bash
cd sentinel-grid-frontend
npx serve . -p 8000
```

---

## 🔌 Connecting to a Backend API

The frontend connects to the following REST endpoints (relative path or configure in `app.js`):

| Endpoint | Method | Description |
| :--- | :---: | :--- |
| `/api/zones` | `GET` | Returns 30 municipal wards with hazard $X$, uncertainty $U$, suitability $G$, and asset markers |
| `/api/priority` | `GET` | Ranked rescue units with ETA and road geometry coordinates |
| `/api/evacuation` | `GET` | Evacuation flows, road corridors, and shelter utilization meters |
| `/api/model/metrics` | `GET` | Machine learning model card with quantitative validation benchmarks |
| `/api/simulate` | `POST` | Live what-if storm simulation payload (`river_gauge_m`, `rain_intensity`, `sar_staleness_h`) |
| `/api/export/incident_action_plan` | `GET` | Formatted NDRF Incident Action Plan text |

*Note: If no backend is running, the frontend gracefully falls back to cached simulation data so it remains 100% interactive and pitch-ready!*

---

## 📁 Repository Structure

```
sentinel-grid-frontend/
├── index.html        # Main tactical dashboard UI
├── style.css         # Tactical dark operations center theme
├── app.js            # Core map logic, live simulation sliders, and data wiring
├── vendor/
│   └── leaflet/      # Bundled offline Leaflet JS & CSS (Zero CDN dependence)
└── README.md         # Documentation & deployment guide
```

---

## 💻 Tech Stack
- **HTML5 & CSS3**: Pure, vanilla CSS design system with glassmorphism, responsive grid, and custom dark mode palette.
- **JavaScript (ES6+)**: Zero framework bloat, sub-second initial render time.
- **Leaflet GIS**: Interactive vector layer management, polylines, custom SVG div-markers.
- **Offline Ready**: Bundled dependencies allow this app to be projected in command centers with the internet cable disconnected.
